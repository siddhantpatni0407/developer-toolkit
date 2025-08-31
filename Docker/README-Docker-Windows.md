# Docker Installation & Setup (Windows)

This guide explains how to install and set up **Docker on Windows**, run containerized applications, and clean up resources. It is intended for developers who want a **local containerization environment** for testing, learning, and building applications.

This guide uses **Nginx** as a placeholder, but the instructions apply to **any containerized application**.

---

## Table of Contents

- [Docker Installation \& Setup (Windows)](#docker-installation--setup-windows)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Install Docker Desktop](#install-docker-desktop)
    - [Option 1: Using Installer (Recommended)](#option-1-using-installer-recommended)
    - [Option 2: Using Chocolatey](#option-2-using-chocolatey)
  - [Verify Installation](#verify-installation)
  - [Run Your First Container](#run-your-first-container)
  - [Build a Custom Docker Image](#build-a-custom-docker-image)
  - [Volumes \& Persistent Storage](#volumes--persistent-storage)
  - [Networking \& Port Mapping](#networking--port-mapping)
  - [Manage Containers](#manage-containers)
  - [Manage Docker Images](#manage-docker-images)
  - [Environment Variables](#environment-variables)
  - [Stop / Cleanup](#stop--cleanup)
  - [Troubleshooting](#troubleshooting)
  - [Notes \& Tips](#notes--tips)

---

## Prerequisites

- Windows 10 / 11 (64-bit)
- **Hyper-V** or **WSL2** enabled
- **PowerShell** or **Command Prompt** familiarity

> 💡 Tip: For Windows Home edition, Docker Desktop uses WSL2. Make sure WSL2 is installed and running.

---

## Install Docker Desktop

### Option 1: Using Installer (Recommended)

1. Download Docker Desktop from [Docker Desktop](https://www.docker.com/products/docker-desktop)
2. Run the installer and follow the wizard
3. During installation:

   - Enable **WSL2** integration if prompted
   - Select required Windows features

4. After installation, restart your computer

### Option 2: Using Chocolatey

```powershell
choco install docker-desktop -y
```

> 💡 Docker Desktop provides Docker Engine, CLI, and GUI for managing containers on Windows.

---

## Verify Installation

Open PowerShell or CMD:

```powershell
docker --version
docker info
```

> Expected output: Docker version, info about your CPU, memory, and storage available to Docker.

---

## Run Your First Container

1. Pull a generic Nginx image:

```powershell
docker pull nginx:latest
```

2. Run the container:

```powershell
docker run -d -p 8080:80 --name my-nginx nginx:latest
```

3. Access the application in your browser: [http://localhost:8080](http://localhost:8080)

> 💡 Explanation:
> `-d` runs in detached mode
> `-p 8080:80` maps host port 8080 to container port 80

---

## Build a Custom Docker Image

1. Create a simple `Dockerfile`:

```dockerfile
# Base image
FROM nginx:latest

# Add a custom index.html
COPY index.html /usr/share/nginx/html/index.html
```

2. Build the image:

```powershell
docker build -t my-custom-nginx:latest .
```

3. Run the custom image:

```powershell
docker run -d -p 8081:80 --name my-custom-nginx my-custom-nginx:latest
```

> 💡 Explanation: Dockerfile defines how the image is built; `COPY` adds local files to the container.

---

## Volumes & Persistent Storage

To persist data between container restarts:

```powershell
docker run -d -p 8082:80 --name my-nginx-volume -v C:\nginx-data:/usr/share/nginx/html nginx:latest
```

- `-v host_path:container_path` maps a local folder to the container, making data persistent.

---

## Networking & Port Mapping

- Map multiple containers to different host ports:

```powershell
docker run -d -p 8083:80 --name nginx2 nginx:latest
```

- Docker network inspect:

```powershell
docker network ls
docker network inspect bridge
```

> 💡 This helps in connecting multiple containers together using user-defined networks.

---

## Manage Containers

```powershell
docker ps               # List running containers
docker ps -a            # List all containers
docker stop <container> # Stop a running container
docker start <container># Start a stopped container
docker rm <container>   # Remove a container
docker logs <container> # View logs
docker exec -it <container> powershell # Access shell inside container
```

---

## Manage Docker Images

```powershell
docker images                # List images
docker rmi <image>           # Remove image
docker tag <image> <name:tag># Tag an image
docker history <image>       # See image layers
```

> 💡 Remove unused images to save disk space.

---

## Environment Variables

Pass environment variables to containers:

```powershell
docker run -d -p 8084:80 --name my-nginx-env -e NGINX_HOST=localhost nginx:latest
```

- Access variables inside the container to configure behavior dynamically.

---

## Stop / Cleanup

1. Stop all containers:

```powershell
docker stop $(docker ps -q)
```

2. Remove all containers:

```powershell
docker rm $(docker ps -a -q)
```

3. Remove all images:

```powershell
docker rmi $(docker images -q)
```

---

## Troubleshooting

- **Docker not starting:** Check WSL2 or Hyper-V installation.
- **Port already in use:** Change host port in `-p host:container`.
- **File permission issues with volumes:** Use a Windows path accessible by Docker Desktop.
- **Memory / CPU limits:** Adjust in Docker Desktop settings.

---

## Notes & Tips

- Always run **PowerShell or CMD as Administrator** for Docker commands on Windows.
- Use Docker Desktop GUI to monitor containers, images, and volumes.
- You can deploy **any containerized application**; Nginx here is just an example.
- Learn `docker-compose` for multi-container setups and orchestration.
- Use `docker system prune -a` carefully to clean all unused containers, images, and networks.

---
