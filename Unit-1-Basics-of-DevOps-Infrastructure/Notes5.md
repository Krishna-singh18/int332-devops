# Introduction to Docker Hub, Docker Architecture and Lifecycle

Docker is a container platform that allows developers to build, ship, and run applications using containers. Docker Hub and Docker Architecture are core components of this ecosystem.

---


# 1. Introduction to Docker Hub

## 1.1 Definition

Docker Hub is a **cloud-based image registry service** used to:

* Store container images
* Share images globally
* Manage image versions
* Integrate with CI/CD pipelines

It is the **default public registry used by Docker**.

---

## 1.2 Key Concepts

* **Repository** → Collection of related images
* **Image** → Snapshot of an application
* **Tag** → Version of an image
* **Namespace** → User or organization name

Example:

```
docker pull nginx
```

Docker automatically pulls the image from Docker Hub.

---

## 1.3 Types of Repositories in Docker Hub

### 1. Public Repository

* Accessible by anyone
* Free to use
* Example: nginx, ubuntu

**2. Private Repository**

* Restricted access
* Requires authentication
* Used by organizations

---

# 2. Features of Docker Hub

## 2.1 Core Features

### 1. Image Hosting

* Store container images

### 2. Public & Private Repositories

* Open source + secure enterprise usage

### 3. Automated Builds

* Connect GitHub/Bitbucket
* Automatically build images on code push

### 4. Webhooks

* Trigger CI/CD pipelines on updates

### 5. Version Control (Tags)

* Maintain multiple versions

### 6. Image Security Scanning

* Detect vulnerabilities

### 7. Official Images

* Verified images (nginx, mysql, node)

---

## 2.2 Advantages

* Easy sharing
* Global access
* CI/CD integration
* Standardized deployment

---

# 3. Docker Architecture

## 3.1 Overview

Docker uses a **client-server architecture**.

```
Docker Client → Docker Daemon → Docker Registry
                        ↓
                   Containers
```

---

## 3.2 Components

| Component       | Role                 |
| --------------- | -------------------- |
| Docker Client   | Sends commands       |
| Docker Daemon   | Executes commands    |
| Docker Images   | Blueprint            |
| Containers      | Running applications |
| Docker Registry | Stores images        |

---

# 4. Key Components of Docker

## 4.1 Docker Client

### Definition

The Docker Client is the **command-line interface (CLI)** used by users.

### Example Commands

```
docker build
docker run
docker pull
docker push
```

### Working

1. User enters command
2. Client sends request to daemon
3. Daemon executes

---

## 4.2 Docker Daemon (dockerd)

### Definition

The Docker Daemon is the **core engine** of Docker.

### Responsibilities

* Build images
* Run containers
* Manage networks & volumes
* Communicate with registries

---

## 4.3 Docker Images

### Definition

A Docker Image is a **read-only template** used to create containers.

### Features

* Layered
* Immutable
* Version controlled

Example:

```
docker pull ubuntu
```

---

## 4.4 Containers

### Definition

A Container is a **running instance of an image**.

### Features

* Lightweight
* Fast startup
* Isolated

Example:

```
docker run -d nginx
```

---

### Container vs Virtual Machine

| Feature     | Container | Virtual Machine |
| ----------- | --------- | --------------- |
| Boot Time   | Seconds   | Minutes         |
| Size        | MB        | GB              |
| OS          | Shared    | Separate        |
| Performance | High      | Moderate        |

---

## 4.5 Docker Registry (Docker Hub)

### Definition

A Docker Registry stores Docker images.
Docker Hub is the default registry.

### Operations

```
docker push → Upload image
docker pull → Download image
```

---

## Example Workflow

```
docker build -t myapp:1.0 .
docker push username/myapp:1.0
docker pull username/myapp:1.0
```

---

# 5. Docker Workflow (End-to-End)

```
Developer writes Dockerfile
        ↓
docker build → Image created
        ↓
docker push → Image stored in registry
        ↓
docker pull → Image downloaded
        ↓
docker run → Container started
```

---

# 6. Docker Lifecycle Stages

## 6.1 Image Lifecycle

### Stage 1: Build

```
docker build -t app:1.0 .
```

Creates image from Dockerfile.

---

### Stage 2: Tag

```
docker tag app username/app:1.0
```

Assign version.

---

### Stage 3: Push

```
docker push username/app:1.0
```

Upload image.

---

### Stage 4: Pull

```
docker pull username/app:1.0
```

Download image.

---

## 6.2 Container Lifecycle

### Stage 1: Create

```
docker create nginx
```

---

### Stage 2: Start

```
docker start container_id
```

---

### Stage 3: Running

Application executes.

---

### Stage 4: Pause / Unpause

```
docker pause container_id
docker unpause container_id
```

---

### Stage 5: Stop

```
docker stop container_id
```

---

### Stage 6: Kill

```
docker kill container_id
```

---

### Stage 7: Remove

```
docker rm container_id
```

---

## 6.3 Container States

| State   | Description |
| ------- | ----------- |
| Created | Initialized |
| Running | Active      |
| Paused  | Suspended   |
| Stopped | Not running |
| Deleted | Removed     |

---

# 7. Complete Docker Flow 

```
Dockerfile
   ↓
docker build
   ↓
Docker Image
   ↓
docker push
   ↓
Docker Hub (Registry)
   ↓
docker pull
   ↓
Container
   ↓
Application Running
```

---

# 8. Docker in CI/CD Integration

```
GitHub → CI Pipeline → Docker Build → Docker Hub → Deployment
```

---

# 9. Key Points

| Topic         | Key Point                       |
| ------------- | ------------------------------- |
| Docker Hub    | Cloud image registry            |
| Docker Client | Command interface               |
| Docker Daemon | Core engine                     |
| Image         | Blueprint                       |
| Container     | Running instance                |
| Registry      | Image storage                   |
| Lifecycle     | Build → Push → Pull → Run       |
