# GitHub Actions Runners, Docker Integration, and Deployments

GitHub Actions provides powerful automation capabilities for Continuous Integration and Continuous Deployment (CI/CD). One of the core components of GitHub Actions is the runner system, which executes workflow jobs. GitHub Actions also integrates strongly with Docker and cloud deployment platforms, allowing developers to automate software builds, containerization, image publishing, and application deployment.

Modern DevOps pipelines commonly use GitHub Actions for:

* Automated builds
* Docker image creation
* Container registry integration
* Cloud deployment
* Infrastructure automation



---

# 1. Introduction to Runners

## 1.1 Definition

A runner is a machine or execution environment that runs GitHub Actions workflows.

When a workflow starts:

1. GitHub selects a runner
2. The runner downloads repository code
3. Workflow jobs execute on the runner

Runners can be:

* GitHub-hosted runners
* Self-hosted runners

---

## 1.2 Role of Runners in GitHub Actions

Runners are responsible for:

* Executing jobs
* Running scripts
* Installing dependencies
* Building applications
* Running tests
* Deploying applications

Without runners, workflows cannot execute.

---

# 2. GitHub-Hosted Runners

## 2.1 Introduction

GitHub-hosted runners are virtual machines managed by GitHub.

GitHub automatically provides infrastructure for workflow execution.

Developers do not need to manage servers manually.

Supported operating systems:

* Ubuntu
* Windows
* macOS

---

## 2.2 Example Configuration

```yaml id="ghr1"
runs-on: ubuntu-latest
```

This workflow runs on the latest Ubuntu runner provided by GitHub.

---

## 2.3 Available GitHub-Hosted Runners

| Runner         | Operating System |
| -------------- | ---------------- |
| ubuntu-latest  | Linux            |
| windows-latest | Windows          |
| macos-latest   | macOS            |

---

## 2.4 Advantages of GitHub-Hosted Runners

GitHub-hosted runners provide several benefits:

1. No infrastructure management
2. Automatic updates
3. Fast setup
4. Pre-installed software tools
5. Easy scalability

These runners are suitable for most CI/CD pipelines.

---

## 2.5 Limitations

GitHub-hosted runners also have limitations:

* Limited customization
* Execution time limits
* Shared infrastructure
* Limited hardware control

For advanced enterprise use cases, organizations often use self-hosted runners.

---

# 3. Self-Hosted Runners

## 3.1 Introduction

Self-hosted runners are machines managed by the organization itself.

These runners can run on:

* Physical servers
* Virtual machines
* Cloud instances
* Kubernetes clusters

Organizations install GitHub runner software on their own infrastructure.

---

## 3.2 Why Self-Hosted Runners Are Used

Self-hosted runners are useful when organizations require:

* Custom software
* Internal network access
* Better security
* High-performance hardware
* Specialized environments

Example:

A company may need internal database access during workflow execution.

---

## 3.3 Self-Hosted Runner Architecture

```id="ghr2"
GitHub Repository
        ↓
GitHub Actions Workflow
        ↓
Self-Hosted Runner
        ↓
Internal Infrastructure
```

---

## 3.4 Registering Self-Hosted Runner

GitHub provides commands to register runners.

Example:

```bash id="ghr3"
./config.sh --url https://github.com/company/repo --token TOKEN
```

---

## 3.5 Starting Runner

```bash id="ghr4"
./run.sh
```

The runner continuously listens for workflow jobs.

---

## 3.6 Advantages of Self-Hosted Runners

1. Full infrastructure control
2. Better customization
3. Access to internal systems
4. Faster execution
5. Better hardware utilization

---

## 3.7 Disadvantages

1. Infrastructure maintenance required
2. Security management responsibility
3. Manual updates
4. Higher operational complexity

---

# 4. Runner Security and Management

## 4.1 Importance of Runner Security

Runners execute workflow code, making them important security targets.

Poorly secured runners may expose:

* Secrets
* Tokens
* Internal infrastructure
* Source code

Therefore, proper security practices are essential.

---

# 4.2 Security Best Practices

## Use Least Privilege Access

Grant minimum required permissions.

Example:

* Limited repository access
* Restricted deployment permissions

---

## Protect Secrets

Store credentials securely using GitHub Secrets.

Example:

```yaml id="ghr5"
${{ secrets.DOCKER_PASSWORD }}
```

---

## Isolate Runners

Separate production and development runners.

This reduces security risks.

---

## Keep Runners Updated

Regularly update:

* Operating system
* Docker
* GitHub runner software

---

## Monitor Runner Activity

Organizations should monitor:

* Workflow logs
* Runner usage
* Unauthorized activity

---

# 5. Docker and GitHub Actions

## 5.1 Introduction

GitHub Actions integrates strongly with Docker.

Developers can automate:

* Docker image building
* Image testing
* Container deployment
* Registry publishing

This enables fully automated container-based CI/CD pipelines.

---

# 6. Building Docker Images in CI

## 6.1 Introduction

Docker images can be automatically built whenever code changes are pushed.

Workflow process:

```id="ghr6"
Push Code
    ↓
GitHub Actions Triggered
    ↓
Docker Image Build
    ↓
Image Testing
    ↓
Push to Registry
```

---

## 6.2 Example Docker Build Workflow

```yaml id="ghr7"
name: Docker Build

on:
  push:

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - name: Build Docker Image
        run: docker build -t myapp .
```

---

## 6.3 Advantages

* Automated container builds
* Faster delivery
* Consistent images
* Reduced manual work

---

# 7. Pushing Docker Images to Docker Hub

## 7.1 Introduction

Docker Hub is the default public Docker registry.

GitHub Actions can automatically push images to Docker Hub after successful builds.

---

## 7.2 Docker Login Action

Example:

```yaml id="ghr8"
- name: Login to Docker Hub
  uses: docker/login-action@v3
  with:
    username: ${{ secrets.DOCKER_USERNAME }}
    password: ${{ secrets.DOCKER_PASSWORD }}
```

---

## 7.3 Build and Push Image

```yaml id="ghr9"
- name: Build and Push
  uses: docker/build-push-action@v5
  with:
    push: true
    tags: username/myapp:latest
```

---

## 7.4 Complete Workflow Example

```yaml id="ghr10"
name: Docker Hub CI

on:
  push:

jobs:

  docker:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - uses: docker/build-push-action@v5
        with:
          push: true
          tags: username/myapp:latest
```

---

# 8. GitHub Container Registry (GHCR)

## 8.1 Introduction

GitHub Container Registry (GHCR) is GitHub’s container image registry.

It allows developers to store Docker images directly inside GitHub.

---

## 8.2 Advantages of GHCR

1. Integrated with GitHub
2. Better repository access control
3. Supports private images
4. Simplifies CI/CD workflows

---

## 8.3 Login to GHCR

Example:

```yaml id="ghr11"
- name: Login to GHCR
  run: echo "${{ secrets.GITHUB_TOKEN }}" | docker login ghcr.io -u USERNAME --password-stdin
```

---

## 8.4 Push Image to GHCR

```yaml id="ghr12"
- name: Push Image
  run: |
    docker build -t ghcr.io/user/myapp:latest .
    docker push ghcr.io/user/myapp:latest
```

---

# 9. Deployments to Servers

## 9.1 Introduction

GitHub Actions can automatically deploy applications to remote servers.

Deployment methods include:

* SSH
* SCP
* Docker deployment
* Kubernetes deployment

---

## 9.2 SSH Deployment Example

```yaml id="ghr13"
- name: Deploy to Server
  run: |
    ssh user@server "
      docker pull username/myapp:latest &&
      docker restart myapp
    "
```

---

## 9.3 Advantages

* Automated deployment
* Reduced downtime
* Faster releases
* Better reliability

---

# 10. Deployments to Cloud Platforms

## 10.1 Introduction

GitHub Actions supports deployment to cloud platforms such as:

* AWS
* Azure
* Google Cloud
* DigitalOcean

---

## 10.2 AWS Deployment Example

```yaml id="ghr14"
- uses: aws-actions/configure-aws-credentials@v4
```

---

## 10.3 Kubernetes Deployment Example

```yaml id="ghr15"
- name: Deploy to Kubernetes
  run: kubectl apply -f deployment.yaml
```

---

## 10.4 Docker Deployment to Cloud VM

```yaml id="ghr16"
- name: Deploy Docker Container
  run: docker run -d -p 80:80 myapp
```

---

# 11. Complete CI/CD Pipeline Example

```id="ghr17"
Developer Pushes Code
          ↓
GitHub Actions Triggered
          ↓
Build Application
          ↓
Run Tests
          ↓
Build Docker Image
          ↓
Push to Docker Hub / GHCR
          ↓
Deploy to Server or Cloud
```

---

# 12. Real-World Usage

Organizations use GitHub Actions and Docker integration for:

* Microservices deployment
* Cloud-native applications
* Kubernetes CI/CD
* Automated DevOps pipelines
* Enterprise software delivery

GitHub Actions is widely used with:

* Docker
* Kubernetes
* Maven
* Terraform
* AWS

---

# 13. Advantages of GitHub Actions with Docker

This integration provides several benefits:

1. Automated container pipelines
2. Faster deployments
3. Consistent environments
4. Scalable CI/CD systems
5. Better DevOps automation

Docker and GitHub Actions together form a powerful cloud-native deployment platform.

---

