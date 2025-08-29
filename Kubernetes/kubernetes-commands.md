# ☸️ Kubernetes + Minikube Commands — Complete Guide

This document is a comprehensive reference for **Kubernetes**, including essential `kubectl` and `minikube` commands for local development. Use it to set up, manage, and troubleshoot clusters and applications effectively.

---

## 🔧 Setup & Configuration

| Command                                | Description                                 |
| -------------------------------------- | ------------------------------------------- |
| `kubectl version --client`             | Show the version of your kubectl client.    |
| `kubectl config view`                  | View the current kubeconfig settings.       |
| `kubectl config get-contexts`          | List all available contexts.                |
| `kubectl config use-context <context>` | Switch between Kubernetes contexts.         |
| `kubectl config current-context`       | Show the current active context.            |
| `kubectl config set-context ...`       | Modify a context (cluster, namespace, etc). |

---

## 💻 Minikube (Local Kubernetes)

| Command                              | Description                                     |
| ------------------------------------ | ----------------------------------------------- |
| `minikube start`                     | Start a local Kubernetes cluster.               |
| `minikube stop`                      | Stop the Minikube cluster.                      |
| `minikube delete`                    | Delete the Minikube cluster.                    |
| `minikube status`                    | Show the status of Minikube components.         |
| `minikube dashboard`                 | Launch Kubernetes dashboard in browser.         |
| `minikube service <svc-name>`        | Open a service in the browser.                  |
| `minikube ip`                        | Get the IP address of the Minikube VM.          |
| `minikube addons list`               | List available Minikube addons.                 |
| `minikube addons enable ingress`     | Enable the NGINX ingress controller.            |
| `minikube tunnel`                    | Create a tunnel for LoadBalancer services.      |
| `minikube logs`                      | View logs for the Minikube cluster.             |
| `minikube ssh`                       | SSH into the Minikube VM.                       |
| `minikube mount <host-dir>:<vm-dir>` | Mount a host directory inside Minikube.         |
| `minikube image load <image>`        | Load a local Docker image into Minikube.        |
| `minikube kubectl -- <command>`      | Run `kubectl` directly from Minikube's context. |

> 💡 **Tip**: Use `minikube start --driver=docker` to run with Docker instead of VirtualBox or other VM drivers.

---

## 🚀 Getting Started

| Command                        | Description                                            |
| ------------------------------ | ------------------------------------------------------ |
| `kubectl cluster-info`         | Display cluster endpoint and service info.             |
| `kubectl get nodes`            | List all nodes in the cluster.                         |
| `kubectl get pods`             | List pods in the current namespace.                    |
| `kubectl get all`              | Get all resources (pods, services, deployments, etc.). |
| `kubectl create namespace dev` | Create a new namespace called `dev`.                   |

---

## 📦 Resource Management

| Command                              | Description                                |
| ------------------------------------ | ------------------------------------------ |
| `kubectl apply -f <file>.yaml`       | Apply a manifest file.                     |
| `kubectl delete -f <file>.yaml`      | Delete resources defined in a manifest.    |
| `kubectl get <resource>`             | Get resources like pods, svc, deployments. |
| `kubectl describe <resource> <name>` | Detailed info about a specific resource.   |
| `kubectl edit <resource> <name>`     | Edit a resource live (opens in editor).    |
| `kubectl delete <resource> <name>`   | Delete a specific resource.                |

---

## 🧪 Pod Debugging & Logs

| Command                               | Description                                      |
| ------------------------------------- | ------------------------------------------------ |
| `kubectl logs <pod>`                  | View logs from a pod.                            |
| `kubectl logs <pod> -c <container>`   | View logs from a specific container.             |
| `kubectl exec -it <pod> -- /bin/bash` | Start a bash shell in the container (if exists). |
| `kubectl describe pod <pod>`          | Detailed info including events & state.          |
| `kubectl port-forward <pod> 8080:80`  | Forward a local port to the pod.                 |

---

## 🧱 Deployments & Scaling

| Command                                         | Description                       |
| ----------------------------------------------- | --------------------------------- |
| `kubectl create deployment nginx --image=nginx` | Create a simple deployment.       |
| `kubectl scale deployment nginx --replicas=3`   | Scale a deployment to 3 replicas. |
| `kubectl rollout status deployment/nginx`       | Check rollout status.             |
| `kubectl rollout undo deployment/nginx`         | Rollback to the previous version. |

---

## 🌍 Services & Networking

| Command                                     | Description                       |
| ------------------------------------------- | --------------------------------- |
| `kubectl expose deployment nginx --port=80` | Expose a deployment as a service. |
| `kubectl get svc`                           | List services.                    |
| `kubectl describe svc <name>`               | Show detailed service info.       |
| `kubectl port-forward svc/<name> 8080:80`   | Forward local port to service.    |

---

## 🔐 ConfigMaps & Secrets

| Command                                                            | Description                              |
| ------------------------------------------------------------------ | ---------------------------------------- |
| `kubectl create configmap my-config --from-literal=key=val`        | Create a config map from literal values. |
| `kubectl create secret generic my-secret --from-literal=key=value` | Create a secret.                         |
| `kubectl describe configmap my-config`                             | Show config map details.                 |
| `kubectl describe secret my-secret`                                | Show secret details (base64-encoded).    |

---

## 🔄 Rollouts & Updates

| Command                                               | Description                              |
| ----------------------------------------------------- | ---------------------------------------- |
| `kubectl set image deployment/nginx nginx=nginx:1.19` | Update deployment image.                 |
| `kubectl rollout history deployment/nginx`            | Show rollout history.                    |
| `kubectl rollout pause deployment/nginx`              | Pause rollout (for progressive updates). |
| `kubectl rollout resume deployment/nginx`             | Resume a paused rollout.                 |

---

## 🧹 Cleanup

| Command                           | Description                        |
| --------------------------------- | ---------------------------------- |
| `kubectl delete pod <pod>`        | Delete a pod.                      |
| `kubectl delete svc <svc>`        | Delete a service.                  |
| `kubectl delete deployment <dep>` | Delete a deployment.               |
| `kubectl delete all --all`        | Delete all resources in namespace. |

---

## 📌 Useful Tips

* Use `kubectl get all -n <namespace>` to view all resources in a namespace.
* Use `kubectl explain <resource>` to get documentation on a resource (e.g., fields).
* Use namespaces to isolate resources in multi-team or multi-project environments.
* Use labels (`-l key=value`) to filter resources.
* Use `minikube image load` to load local images instead of using a remote registry.

---

## 🌐 External References

* [Kubernetes Docs](https://kubernetes.io/docs/)
* [Minikube Docs](https://minikube.sigs.k8s.io/docs/)
* [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
* [Play with Kubernetes](https://labs.play-with-k8s.com/)
* [Katacoda Scenarios](https://www.katacoda.com/courses/kubernetes)

---

## 🛠 Recommended Local Workflow (Minikube)

### ✅ Start Minikube

```bash
minikube start --driver=docker
```

### 📦 Deploy an App

```bash
kubectl create deployment demo-app --image=nginx
```

### 🌍 Expose the App

```bash
kubectl expose deployment demo-app --type=NodePort --port=80
```

### 🔎 Access the App

```bash
minikube service demo-app
```

---