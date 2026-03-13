# Container Images, Image Layers, and Image Registries

Container images are the foundation of container-based systems such as Docker. They define how an application and its environment are packaged and distributed.

---

# 1. Container Image

## 1.1 Definition

A **Container Image** is a read-only package that contains everything required to run an application.

It includes:

* Application code
* Runtime environment
* System libraries
* Dependencies
* Configuration files
* OS components

A container image acts as a **blueprint used to create containers**.

Example:

```
docker run nginx
```

Docker pulls the **nginx image** and creates a running container from it.

---

## 1.2 Key Characteristics of Container Images

| Feature   | Description                                  |
| --------- | -------------------------------------------- |
| Read-only | Images cannot be modified directly           |
| Portable  | Can run on any system with container runtime |
| Layered   | Built from multiple layers                   |
| Versioned | Supports tags and versions                   |
| Reusable  | Same image can run multiple containers       |

---

## 1.3 Container Image Structure

A container image typically contains several layers.

```
Container Image
│
├── Base OS Layer
├── System Libraries
├── Runtime (Python / Java / Node)
├── Application Dependencies
├── Application Code
└── Metadata
```

---

## 1.4 Example Dockerfile

```
FROM python:3.10
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

This Dockerfile builds a container image containing a Python application.

---

# 2. Image Layers

## 2.1 Definition

A **Container Image Layer** is a read-only filesystem layer representing a change made to the image.

Each instruction in a Dockerfile creates a new layer.

Example:

```
FROM ubuntu
RUN apt update
RUN apt install python3
COPY app.py /app/
```

Each command above creates a **separate image layer**.

---

## 2.2 Layer Structure

```
Application Layer
───────────────
Dependencies Layer
───────────────
Runtime Layer
───────────────
System Libraries
───────────────
Base OS Layer
```

---

## 2.3 Advantages of Image Layers

### 1. Efficient Storage

Layers can be reused across multiple images.

Example:

```
Image A
Base Layer
Python Layer
App Layer

Image B
Base Layer
Python Layer
Another App Layer
```

Base layers are reused.

---

### 2. Faster Builds

Docker uses **build cache**.

If a layer is unchanged, it is reused.

---

### 3. Faster Downloads

When pulling images:

```
docker pull image
```

Only new layers are downloaded.

---

### 4. Copy-On-Write

When a container runs:

* Image layers = read-only
* Container layer = writable

---

# 3. Container vs Container Image

| Feature    | Container Image           | Container           |
| ---------- | ------------------------- | ------------------- |
| Definition | Blueprint/template        | Running instance    |
| State      | Static                    | Dynamic             |
| Mutability | Read-only                 | Writable layer      |
| Usage      | Used to create containers | Runs application    |
| Storage    | Stored in registry        | Runs in runtime     |
| Lifecycle  | Build → Store             | Create → Run → Stop |

Example:

Image:

```
nginx:latest
```

Container:

```
docker run nginx
```

Concept analogy:

**Image = Class**
**Container = Object**

---

# 4. Image Registry

## 4.1 Definition

An **Image Registry** is a centralized repository used to store and distribute container images.

It allows:

* Storing images
* Sharing images
* Downloading images

Examples:

* Docker Hub
* GitHub Container Registry
* AWS Elastic Container Registry (ECR)

---

## 4.2 Basic Workflow

```
Developer builds image
        ↓
docker build
        ↓
Push image to registry
        ↓
docker push
        ↓
Registry stores image
        ↓
Other systems pull image
        ↓
docker pull
```

---

# 5. Without Image Registry

Without an image registry, images must be transferred manually.

Example:

```
docker save image > image.tar
```

Transfer file to another machine.

```
docker load < image.tar
```

Problems:

* Difficult sharing
* Manual transfer
* No version management
* Not scalable

---

# 6. With Image Registry

Using a registry:

```
docker push username/app:1.0
```

Another system:

```
docker pull username/app:1.0
```

Advantages:

* Centralized storage
* Easy sharing
* Version control
* CI/CD integration

---

# 7. Types of Image Registries

## 7.1 Public Registry

A registry accessible to anyone on the internet.

Examples:

* Docker Hub
* GitHub Container Registry

Characteristics:

* Publicly accessible
* Free images available
* Community maintained

Example:

```
docker pull nginx
```

---

## 7.2 Private Registry

Restricted registry for organizations or authorized users.

Examples:

* AWS ECR
* Azure Container Registry
* Google Container Registry

Characteristics:

* Secure
* Authentication required
* Enterprise usage

---

## 7.3 Self-Hosted Registry

Organizations host their own registry server.

Example:

```
docker run -d -p 5000:5000 registry
```

Advantages:

* Full control
* Internal deployment
* Private network usage

---

# 8. Image Naming Convention

Container images follow a structured naming format.

General format:

```
registry/username/repository:tag
```

Example:

```
docker.io/library/nginx:latest
```

Breakdown:

| Component  | Meaning              |
| ---------- | -------------------- |
| registry   | Registry location    |
| username   | User or organization |
| repository | Image name           |
| tag        | Version              |

Example:

```
ghcr.io/company/backend:1.2
```

---

# 9. Tags and Versioning

## 9.1 Definition

Tags represent versions of an image.

Examples:

```
nginx:1.25
nginx:latest
nginx:alpine
```

---

## 9.2 Tag Format

```
image_name:tag
```

Example:

```
backend:v1
backend:v2
backend:prod
backend:dev
```

---

## 9.3 Importance of Tags

Tags enable:

* Version management
* Rollback capability
* Environment specific builds

Example:

```
app:dev
app:test
app:prod
```

---

## 9.4 Tagging Command

Tag an image:

```
docker tag image_name username/repo:tag
```

Example:

```
docker tag app myrepo/app:v1
```

Push image:

```
docker push myrepo/app:v1
```

---

# 10. Role of Image Registries in CI/CD Pipelines

Image registries are essential components of CI/CD pipelines.

### Workflow

```
Developer commits code
        ↓
CI server builds image
        ↓
Image pushed to registry
        ↓
Deployment system pulls image
        ↓
Application deployed
```

Example pipeline:

```
GitHub → GitHub Actions → Docker Build → Registry → Kubernetes
```

---

### Example CI/CD Flow

Step 1 — Developer pushes code

```
git push origin main
```

Step 2 — CI builds image

```
docker build -t app:1.0 .
```

Step 3 — Push image

```
docker push repo/app:1.0
```

Step 4 — Deployment server pulls image

```
docker pull repo/app:1.0
```

Step 5 — Run container

```
docker run repo/app:1.0
```

Benefits:

* Consistent deployments
* Versioned builds
* Rollback capability
* Centralized storage
* Scalable deployments

---

# 11. Comparison: Public vs Private Registry

| Feature        | Public Registry    | Private Registry        |
| -------------- | ------------------ | ----------------------- |
| Access         | Open to everyone   | Restricted              |
| Security       | Lower              | High                    |
| Cost           | Usually free       | Paid / enterprise       |
| Use Case       | Open source images | Enterprise applications |
| Authentication | Optional           | Required                |
| Control        | Limited            | Full control            |

Examples:

Public Registries:

* Docker Hub
* GitHub Container Registry

Private Registries:

* AWS ECR
* Azure Container Registry
* Google Container Registry



------