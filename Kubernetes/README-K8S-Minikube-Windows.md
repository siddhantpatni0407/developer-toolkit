# Kubernetes & Minikube Setup (Windows)

This guide explains how to set up **Kubernetes locally on Windows** using **Minikube**, deploy a **generic containerized application**, and clean up resources. It is intended for developers who want a **local Kubernetes environment** for testing, learning, and experimenting with container orchestration.

---

## Table of Contents

- [Kubernetes \& Minikube Setup (Windows)](#kubernetes--minikube-setup-windows)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Install Minikube on Windows](#install-minikube-on-windows)
    - [Option 1: Using Chocolatey (Recommended)](#option-1-using-chocolatey-recommended)
    - [Option 2: Manual Installation](#option-2-manual-installation)
  - [Install kubectl](#install-kubectl)
    - [Option 1: Using Chocolatey](#option-1-using-chocolatey)
    - [Option 2: Manual Installation](#option-2-manual-installation-1)
  - [Start Minikube](#start-minikube)
  - [Access Minikube Dashboard](#access-minikube-dashboard)
  - [Build Docker Image in Minikube](#build-docker-image-in-minikube)
  - [Deploy Application to Kubernetes](#deploy-application-to-kubernetes)
  - [Verify Deployment](#verify-deployment)
  - [Access Services](#access-services)
  - [Stop / Cleanup](#stop--cleanup)
  - [Notes \& Tips](#notes--tips)

---

## Prerequisites

Before starting, ensure you have the following installed and configured:

* **Windows 10 / 11 (64-bit)**
* **Hyper-V** or **VirtualBox** enabled (required for Minikube VM driver)
* **Chocolatey** (optional, makes installation easier)
* **Docker Desktop** (optional, allows Minikube to use Docker as the driver)
* Basic familiarity with **PowerShell** commands

> 💡 Tip: Hyper-V must be enabled in BIOS. VirtualBox can be used if Hyper-V is not available.

---

## Install Minikube on Windows

### Option 1: Using Chocolatey (Recommended)

```powershell
choco install minikube -y
```

### Option 2: Manual Installation

1. Download the latest Minikube `.exe` from: [https://minikube.sigs.k8s.io/docs/start/](https://minikube.sigs.k8s.io/docs/start/)
2. Move the executable to a directory included in your `PATH`, e.g., `C:\Program Files\Minikube`

**Verify installation:**

```powershell
minikube version
```

> 💡 Explanation: This ensures that Minikube is correctly installed and available globally in your terminal.

---

## Install kubectl

`kubectl` is the Kubernetes CLI tool to manage clusters.

### Option 1: Using Chocolatey

```powershell
choco install kubernetes-cli -y
```

### Option 2: Manual Installation

1. Download from [https://kubernetes.io/docs/tasks/tools/](https://kubernetes.io/docs/tasks/tools/)
2. Add `kubectl.exe` to your `PATH`

**Verify installation:**

```powershell
kubectl version --client
```

> 💡 Explanation: `kubectl` allows you to create, manage, and monitor Kubernetes objects like pods, deployments, and services.

---

## Start Minikube

1. Open **PowerShell** as Administrator
2. Start Minikube with sufficient resources:

```powershell
minikube start --driver=hyperv --memory=4096 --cpus=2
```

**Check status:**

```powershell
minikube status
```

> 💡 Tip: Adjust memory and CPU allocation based on your system. For learning and small workloads, 4GB memory and 2 CPUs are sufficient.

---

## Access Minikube Dashboard

```powershell
minikube dashboard
```

* Opens a browser-based **Kubernetes dashboard**
* Allows visualization of pods, deployments, services, and cluster health
* Provides easy access to logs and resource usage

> 💡 Tip: Use this for a GUI view instead of always using CLI commands.

---

## Build Docker Image in Minikube

For Kubernetes to deploy an image, it must exist **inside Minikube’s Docker environment**.

1. Switch Docker CLI to Minikube:

```powershell
& minikube -p minikube docker-env --shell powershell | Invoke-Expression
```

2. Pull a generic Nginx image and tag it for your deployment:

```powershell
docker pull nginx:latest
docker tag nginx:latest my-nginx:latest
```

> 💡 Explanation: Tagging allows Kubernetes to reference the image by name (`my-nginx:latest`) during deployment.

---

## Deploy Application to Kubernetes

1. Create a simple deployment YAML (`nginx-deployment.yaml`):

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: my-nginx:latest
          ports:
            - containerPort: 80
```

2. Apply the deployment:

```powershell
kubectl apply -f nginx-deployment.yaml
```

3. Expose it as a service (`nginx-service.yaml`):

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
  type: NodePort
```

```powershell
kubectl apply -f nginx-service.yaml
```

> 💡 Explanation: Deployments ensure your container runs reliably with replicas. Services expose the pods to the network.

---

## Verify Deployment

```powershell
kubectl get pods           # Check pod status
kubectl get svc            # Check service endpoints
kubectl describe pod <pod-name>  # Detailed pod info
kubectl logs <pod-name>          # Check logs for errors
```

> 💡 Tip: Pods should show `STATUS=Running`. If `CrashLoopBackOff` appears, check the container logs.

---

## Access Services

1. **Port-forward (temporary access):**

```powershell
kubectl port-forward svc/nginx-service 8080:80
```

* Access at [http://localhost:8080](http://localhost:8080)

2. **Get Minikube service URL (persistent access):**

```powershell
minikube service nginx-service --url
```

> 💡 Tip: Port-forwarding is temporary; the service URL works as long as Minikube is running.

---

## Stop / Cleanup

1. Delete Kubernetes resources:

```powershell
kubectl delete -f nginx-deployment.yaml
kubectl delete -f nginx-service.yaml
```

2. Stop and delete Minikube:

```powershell
minikube stop
minikube delete
```

3. Delete all images inside Minikube’s Docker environment:

```powershell
& minikube -p minikube docker-env --shell powershell | Invoke-Expression
docker images -q | ForEach-Object { docker rmi -f $_ }
```

> 💡 Explanation: Cleans up disk space and resets the cluster for future experiments.

---

## Notes & Tips

* Always use **PowerShell** on Windows for Minikube commands.
* Allocate sufficient memory and CPU to avoid pod crashes.
* Use `kubectl get pods` and `kubectl get svc` frequently to monitor resources.
* You can deploy **any containerized application**; Nginx here is just an example.
* Minikube dashboard provides a GUI view and is recommended for beginners.
* For advanced testing, consider using ConfigMaps, Secrets, and persistent volumes.

---
