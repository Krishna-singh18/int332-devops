# CI/CD with Jenkins

Jenkins is one of the most popular and widely used automation servers in the DevOps ecosystem. It is an open-source tool that helps developers and organizations automate various stages of the software development lifecycle such as building, testing, packaging, integration, and deployment. Jenkins enables teams to implement Continuous Integration (CI) and Continuous Deployment/Delivery (CD) practices efficiently.

In modern software development, applications are updated frequently. Manual testing and deployment processes are slow, error-prone, and difficult to manage. Jenkins solves these problems by automating repetitive tasks and ensuring faster and more reliable software delivery.

Jenkins supports:

* Automated software builds
* Automated testing
* Continuous Integration
* Continuous Delivery and Deployment
* Pipeline automation
* Integration with DevOps tools
* Cloud and container deployments
* Distributed build systems


---

# 1. Introduction to Continuous Integration and Continuous Deployment

Modern software development requires rapid delivery of applications with high quality and reliability. Continuous Integration and Continuous Deployment are two important DevOps practices that help achieve this goal.

---

## 1.1 Continuous Integration (CI)

Continuous Integration (CI) is a software development practice where developers frequently merge their code changes into a shared repository such as GitHub or GitLab. Every time code is pushed to the repository, an automated build and testing process is triggered.

The main objective of CI is to detect bugs and integration issues early in the development cycle.

### Activities Performed in CI

Whenever a developer pushes code:

* Source code is fetched from the repository
* Application is compiled
* Unit tests are executed
* Static code analysis may be performed
* Build reports are generated

### Benefits of Continuous Integration

* Early bug detection
* Improved software quality
* Faster development cycles
* Reduced integration problems
* Better collaboration among developers
* Automated testing and validation

### Example CI Workflow

```text
Developer Pushes Code
          ↓
Jenkins Triggered
          ↓
Download Source Code
          ↓
Build Application
          ↓
Run Automated Tests
          ↓
Generate Build Report
```

### Real-World Example

Suppose multiple developers are working on an e-commerce application. Without CI, integrating code changes manually may create conflicts and bugs. With Jenkins CI pipelines, every code push is automatically tested, ensuring stable integration.

---

## 1.2 Continuous Deployment (CD)

Continuous Deployment (CD) is the process of automatically deploying applications after successful testing and validation.

Once the CI pipeline completes successfully:

* Application artifacts are generated
* Docker images may be created
* Deployment scripts are executed
* Application is deployed to staging or production environments

### Types of CD

#### Continuous Delivery

The deployment process is automated, but deployment to production requires manual approval.

#### Continuous Deployment

The deployment process is fully automated, including production deployment.

### Benefits of Continuous Deployment

* Faster software releases
* Reduced manual effort
* Improved deployment consistency
* Faster feedback from users
* Reduced deployment failures

### Example CD Workflow

```text
Successful Build
        ↓
Create Docker Image
        ↓
Push Image to Registry
        ↓
Deploy to Cloud Server
```

---

# 2. Introduction to Jenkins

Jenkins is an open-source automation server written in Java. It is mainly used to automate software development tasks and implement CI/CD pipelines.

Originally developed as Hudson, Jenkins later became one of the most powerful DevOps automation tools.

### Main Uses of Jenkins

* Continuous Integration
* Continuous Deployment
* Automated testing
* Build automation
* Infrastructure automation
* Monitoring deployment workflows

### Jenkins Integrations

Jenkins integrates with many DevOps tools:

* GitHub
* GitLab
* Docker
* Kubernetes
* Maven
* Gradle
* AWS
* Azure
* Terraform
* Ansible

### Pipeline as Code

Jenkins pipelines are stored in a file called:

```text
Jenkinsfile
```

This file contains all CI/CD stages written as code.

### Advantages of Jenkins

* Open-source and free
* Large plugin ecosystem
* Platform independent
* Highly customizable
* Supports distributed builds
* Strong community support

---

# 3. Jenkins Architecture

## 3.1 Overview

Jenkins follows a distributed architecture called the **Master-Agent Architecture**.

This architecture improves scalability and performance by distributing workloads across multiple machines.

### Architecture Flow

```text
Developer
    ↓
Git Repository
    ↓
Jenkins Master
    ↓
Jenkins Agents
    ↓
Build / Test / Deploy
```

### Components of Jenkins Architecture

1. Jenkins Master
2. Jenkins Agents
3. Build Queue
4. Executors
5. Plugins
6. Pipelines

---

# 4. Jenkins Master

## 4.1 Definition

The Jenkins Master is the central server responsible for controlling and managing Jenkins operations.

It acts as the brain of the Jenkins environment.

### Responsibilities of Jenkins Master

The master handles:

* Job scheduling
* Pipeline management
* User authentication
* Plugin management
* Build monitoring
* Agent communication
* Security configuration

---

## 4.2 Responsibilities of Jenkins Master

### 1. Job Scheduling

The master decides when and where jobs should run.

### 2. Build Monitoring

It tracks build status and logs.

### 3. User Authentication

Controls user login and permissions.

### 4. Plugin Management

Installs and manages Jenkins plugins.

### 5. Pipeline Coordination

Coordinates execution of CI/CD pipelines.

---

## 4.3 Limitations of Jenkins Master

Running all builds directly on the master can create problems:

* High CPU usage
* Memory overload
* Slow performance
* Reduced scalability

To solve this issue, Jenkins uses agents.

---

# 5. Jenkins Agents

## 5.1 Definition

Jenkins Agents are worker machines connected to the Jenkins master.

Agents execute actual tasks such as:

* Building applications
* Running tests
* Deploying applications

---

## 5.2 Why Agents Are Used

Agents provide distributed execution capabilities.

### Advantages of Agents

* Parallel builds
* Better scalability
* Faster execution
* Platform-specific builds
* Reduced load on master

### Example

```text
Linux Agent → Java Application Build
Windows Agent → .NET Application Build
Mac Agent → iOS Build
```

---

## 5.3 Agent Communication

The Jenkins master communicates with agents using:

* SSH
* JNLP
* WebSockets

### Agent Types

1. Permanent Agents
2. Dynamic Cloud Agents
3. Docker Agents
4. Kubernetes Agents

---

# 6. Jenkins Installation

## 6.1 Jenkins Installation on Windows

### Prerequisites

* Java JDK installed
* Minimum RAM and storage

### Installation Steps

1. Download Java JDK
2. Install Java
3. Download Jenkins installer
4. Run Jenkins installer
5. Start Jenkins service
6. Open browser

Default Jenkins URL:

```text
http://localhost:8080
```

### Unlock Jenkins

During first startup:

* Jenkins generates an admin password
* Password is stored in installation directory
* Enter password to continue setup

---

## 6.2 Jenkins Installation Using Docker

Docker simplifies Jenkins installation.

### Docker Command

```bash
docker run -d -p 8080:8080 jenkins/jenkins:lts
```

### Explanation

* `-d` → Run container in background
* `-p 8080:8080` → Map ports
* `jenkins/jenkins:lts` → Official Jenkins image

### Benefits of Docker Installation

* Easy setup
* Portable environment
* Isolation
* Quick deployment

---

# 7. Jenkins UI Overview

The Jenkins dashboard provides a graphical interface for managing CI/CD workflows.

### Main Features

* Job creation
* Build monitoring
* Pipeline visualization
* Plugin management
* User management

### Important Sections

| Section        | Purpose               |
| -------------- | --------------------- |
| Dashboard      | Displays all jobs     |
| New Item       | Create new jobs       |
| Build History  | Shows previous builds |
| Manage Jenkins | Global configuration  |
| Credentials    | Manage secrets        |
| Nodes          | Manage agents         |

---

# 8. Plugins Management

## 8.1 Introduction

Plugins extend Jenkins functionality.

Jenkins has thousands of plugins available for integrating with DevOps tools.

### Examples of Plugins

* Git Plugin
* Docker Plugin
* Maven Plugin
* Kubernetes Plugin
* Blue Ocean Plugin

---

## 8.2 Installing Plugins

### Steps

1. Open Manage Jenkins
2. Select Plugins
3. Search plugin
4. Install plugin
5. Restart Jenkins if required

---

## 8.3 Important Plugins

| Plugin            | Purpose                |
| ----------------- | ---------------------- |
| Git Plugin        | Git integration        |
| Pipeline Plugin   | Pipeline support       |
| Docker Plugin     | Docker integration     |
| Maven Plugin      | Maven builds           |
| Blue Ocean        | Modern UI              |
| Kubernetes Plugin | Kubernetes integration |

---

# 9. Jenkins Security

## 9.1 Importance

Jenkins handles sensitive operations such as:

* Deployments
* Credentials
* Production access
* Cloud infrastructure

Improper security configuration can expose systems to attacks.

---

## 9.2 Security Features

Jenkins provides:

* Authentication
* Authorization
* Role-based access control
* Credentials management
* API token security

### Best Practices

* Enable HTTPS
* Use strong passwords
* Restrict anonymous access
* Backup Jenkins regularly
* Use RBAC

---

# 10. Users and Roles

## 10.1 User Management

Jenkins supports multiple users.

Each user can have:

* Username
* Password
* Permissions

### User Types

* Administrator
* Developer
* Tester
* Viewer

---

## 10.2 Role-Based Access Control

Permissions are assigned using roles.

### Example Roles

| Role      | Permissions              |
| --------- | ------------------------ |
| Admin     | Full access              |
| Developer | Build and configure jobs |
| Viewer    | Read-only access         |

### Benefits

* Improved security
* Controlled access
* Better team management

---

# 11. Jenkins Pipelines

## 11.1 Introduction

A Jenkins pipeline defines the CI/CD workflow as code.

Pipelines automate:

* Source code checkout
* Build process
* Testing
* Packaging
* Deployment

Pipeline code is stored inside:

```text
Jenkinsfile
```

### Benefits of Pipelines

* Automation
* Reusability
* Version control
* Scalability
* Better visibility

---

# 12. Freestyle Jobs vs Pipeline Jobs

## 12.1 Freestyle Jobs

Freestyle jobs are traditional Jenkins jobs configured using the graphical interface.

### Advantages

* Easy setup
* Beginner friendly

### Disadvantages

* Difficult maintenance
* Limited scalability
* Hard to version control

---

## 12.2 Pipeline Jobs

Pipeline jobs use code-based configuration.

### Advantages

* Version controlled
* Reusable
* Scalable
* Better automation

---

## 12.3 Comparison

| Feature         | Freestyle | Pipeline |
| --------------- | --------- | -------- |
| Configuration   | GUI       | Code     |
| Scalability     | Low       | High     |
| Version Control | Difficult | Easy     |
| Reusability     | Limited   | High     |
| Automation      | Basic     | Advanced |

---

# 13. Declarative Pipeline Syntax

## 13.1 Introduction

Declarative pipelines use structured syntax and are easier to read.

### Example

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

    }
}
```

---

## 13.2 Features

* Simple syntax
* Easy readability
* Recommended for beginners
* Better validation support

### Main Components

* pipeline
* agent
* stages
* steps
* post

---

# 14. Scripted Pipeline Syntax

## 14.1 Introduction

Scripted pipelines use Groovy scripting language.

### Example

```groovy
node {

    stage('Build') {
        sh 'mvn clean install'
    }

}
```

---

## 14.2 Features

* More flexibility
* Advanced scripting
* Complex workflow support
* Dynamic pipeline generation

### Difference from Declarative Pipeline

Scripted pipelines provide more control but are harder to maintain.

---

# 15. Jenkinsfile Structure

A Jenkinsfile defines the complete CI/CD workflow.

### Basic Structure

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {

            }
        }

        stage('Build') {
            steps {

            }
        }

    }
}
```

### Common Sections

* Agent
* Environment
* Parameters
* Stages
* Post actions

---

# 16. Parameters in Jenkins

## 16.1 Introduction

Parameters allow users to provide input during pipeline execution.

### Examples

* Environment selection
* Version number
* Deployment target

---

## 16.2 Example Parameter

```groovy
parameters {
    string(name: 'VERSION')
}
```

### Types of Parameters

* String
* Boolean
* Choice
* Password

---

# 17. Environment Variables

## 17.1 Definition

Environment variables store reusable configuration values.

### Example

```groovy
environment {
    APP_ENV = 'production'
}
```

---

## 17.2 Benefits

* Reusable configuration
* Better maintainability
* Secure credential handling
* Simplified pipeline management

---

# 18. Jenkins Multi-Branch Pipelines

## 18.1 Introduction

Multi-branch pipelines automatically detect Git branches and create separate pipelines.

### Example Branches

```text
main
develop
feature/login
bugfix/payment
```

---

## 18.2 Advantages

* Branch isolation
* Automated CI for all branches
* Easier feature development
* Better testing workflows

---

# 19. Pipeline Stages

Pipelines are divided into logical stages.

### Common Stages

1. Checkout
2. Build
3. Test
4. Package
5. Deploy

### Benefits of Stages

* Better organization
* Easier debugging
* Improved visualization

---

# 20. Checkout Code from Git

Source code is downloaded from Git repositories.

### Example

```groovy
git 'https://github.com/user/repo.git'
```

### Supported Repositories

* GitHub
* GitLab
* Bitbucket

---

# 21. Build Stage

The build stage compiles source code into executable artifacts.

### Example

```groovy
sh 'mvn compile'
```

### Build Tools

* Maven
* Gradle
* Ant

---

# 22. Test Stage

The test stage executes automated tests.

### Example

```groovy
sh 'mvn test'
```

### Types of Tests

* Unit tests
* Integration tests
* Functional tests

---

# 23. Package Stage

The package stage creates deployable artifacts.

### Example

```groovy
sh 'mvn package'
```

### Generated Artifacts

* JAR files
* WAR files
* ZIP packages

---

# 24. Post Actions

## 24.1 Introduction

Post actions execute after pipeline completion.

### Examples

* Notifications
* Cleanup
* Artifact archiving
* Email alerts

---

## 24.2 Example

```groovy
post {

    always {
        echo 'Pipeline Finished'
    }

}
```

### Post Conditions

* always
* success
* failure
* unstable

---

# 25. Managing Artifacts

## 25.1 Definition

Artifacts are generated outputs from builds.

### Examples

* JAR files
* WAR files
* Reports
* Docker images

---

## 25.2 Artifact Archiving

### Example

```groovy
archiveArtifacts artifacts: 'target/*.jar'
```

### Benefits

* Easy download
* Deployment reuse
* Build traceability

---

# 26. Complete Jenkins Pipeline Example

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/user/repo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

    }

    post {

        success {
            archiveArtifacts artifacts: 'target/*.jar'
        }

    }
}
```

### Workflow Explanation

1. Source code is downloaded
2. Application is built
3. Tests are executed
4. Package is generated
5. Artifacts are archived

---

# 27. Advantages of Jenkins

Jenkins provides many advantages in DevOps environments.

### Major Benefits

1. Automated CI/CD pipelines
2. Large plugin ecosystem
3. Distributed builds
4. Git integration
5. Docker and Kubernetes support
6. Pipeline as Code
7. Scalable automation
8. Open-source platform
9. Community support

---

# 28. Real-World Usage

Jenkins is widely used in enterprise environments.

### Common Use Cases

* Enterprise CI/CD
* Java application builds
* Docker deployments
* Kubernetes automation
* Cloud deployments
* Infrastructure automation

### Industries Using Jenkins

* Banking
* E-commerce
* Healthcare
* IT services
* Cloud computing

---

