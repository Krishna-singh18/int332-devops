

# 1. Introduction to Jenkins CI/CD Deployment Flows

A CI/CD deployment flow is an automated pipeline that controls the entire software delivery process from code commit to deployment.

Typical Jenkins deployment flow:

```text id="flow1"
Developer Pushes Code
          ↓
Git Repository
          ↓
Jenkins Triggered
          ↓
Build Application
          ↓
Run Automated Tests
          ↓
Generate Artifacts
          ↓
Deploy to Server/Cloud
```

These automated flows improve:

* Development speed
* Reliability
* Software quality
* Deployment consistency

---

# 2. Triggering Builds in Jenkins

## 2.1 Introduction

Jenkins pipelines can start automatically when specific events occur.

These events are called:

```text id="flow2"
Build Triggers
```

Triggers automate CI/CD workflows without manual intervention.

---

# 3. Types of Build Triggers

Common Jenkins build triggers include:

| Trigger           | Purpose                        |
| ----------------- | ------------------------------ |
| pollSCM           | Periodically checks repository |
| Webhook           | Instant build trigger          |
| Manual Trigger    | User starts build              |
| Scheduled Trigger | Time-based execution           |

---

# 4. pollSCM Trigger

## 4.1 Definition

`pollSCM` is a Jenkins mechanism that periodically checks the source code repository for changes.

If Jenkins detects changes:

* Build starts automatically

---

## 4.2 Working Process

```text id="flow3"
Jenkins Checks Repository
          ↓
Code Change Detected
          ↓
Pipeline Triggered
```

---

## 4.3 Example Configuration

Example pipeline:

```groovy id="flow4"
triggers {
    pollSCM('* * * * *')
}
```

---

## 4.4 Cron Syntax Explanation

The expression:

```text id="flow5"
* * * * *
```

means:

```text id="flow6"
Every minute
```

Cron format:

```text id="flow7"
MIN HOUR DAY MONTH WEEKDAY
```

---

## 4.5 Advantages of pollSCM

* Simple setup
* No external configuration required
* Automatic repository monitoring

---

## 4.6 Disadvantages

* Continuous repository polling increases load
* Slower than webhooks
* Not real-time

Because of these limitations, webhooks are preferred.

---

# 5. Webhook Trigger

## 5.1 Definition

A webhook is an event-based HTTP callback used to trigger Jenkins builds instantly when repository events occur.

Supported events:

* Push
* Pull request
* Merge

---

## 5.2 Webhook Workflow

```text id="flow8"
Developer Pushes Code
          ↓
GitHub Sends Webhook
          ↓
Jenkins Receives Request
          ↓
Pipeline Starts Immediately
```

---

## 5.3 GitHub Webhook Configuration

### Steps

1. Open GitHub Repository
2. Go to Settings
3. Select Webhooks
4. Add Jenkins webhook URL

Example URL:

```text id="flow9"
http://jenkins-server/github-webhook/
```

---

## 5.4 Jenkins Configuration

Enable GitHub webhook trigger.

Example:

```groovy id="flow10"
triggers {
    githubPush()
}
```

---

## 5.5 Advantages of Webhooks

* Real-time builds
* Faster CI/CD
* Reduced server load
* Better automation

Webhooks are the industry-standard approach for CI/CD triggering.

---

# 6. Pipeline Libraries

## 6.1 Introduction

Pipeline libraries allow reusable Jenkins pipeline code.

Instead of repeating pipeline logic in every Jenkinsfile, common code is stored centrally.

---

## 6.2 Why Pipeline Libraries Are Important

Without libraries:

* Code duplication increases
* Maintenance becomes difficult
* Pipelines become inconsistent

Pipeline libraries solve these issues.

---

# 6.3 Shared Library Structure

Example structure:

```text id="flow11"
shared-library/
│
├── vars/
├── src/
└── resources/
```

---

## 6.4 Important Directories

### vars/

Contains reusable pipeline scripts.

---

### src/

Contains Groovy classes.

---

### resources/

Contains external resource files.

---

# 6.5 Example Shared Function

Example:

```groovy id="flow12"
def buildApp() {
    sh 'mvn clean install'
}
```

---

# 6.6 Using Shared Libraries

Example Jenkinsfile:

```groovy id="flow13"
@Library('my-shared-library') _

pipeline {

    agent any

    stages {

        stage('Build') {

            steps {
                buildApp()
            }

        }

    }

}
```

---

## 6.7 Advantages of Pipeline Libraries

* Reusable code
* Better maintainability
* Standardized pipelines
* Reduced duplication

Shared libraries are heavily used in enterprise Jenkins environments.

---

# 7. Jenkins Agents

## 7.1 Introduction

Agents are worker machines used by Jenkins to execute builds and deployment tasks.

Agents improve:

* Scalability
* Parallel execution
* Resource distribution

---

# 8. SSH-Based Jenkins Agents

## 8.1 Definition

SSH-based agents connect to Jenkins master using SSH protocol.

---

## 8.2 Workflow

```text id="flow14"
Jenkins Master
       ↓ SSH
Remote Agent
       ↓
Build Execution
```

---

## 8.3 Advantages

* Secure communication
* Easy Linux integration
* Distributed builds

---

## 8.4 SSH Agent Configuration

Required:

* SSH server
* Authentication credentials
* Java installation

---

# 9. SFTP-Based Deployment

## 9.1 Introduction

SFTP is used for secure file transfer between Jenkins and remote servers.

Jenkins pipelines can upload:

* Artifacts
* Build files
* Deployment packages

---

## 9.2 Example Workflow

```text id="flow15"
Build Artifact
       ↓
SFTP Upload
       ↓
Remote Server
```

---

## 9.3 Advantages

* Secure file transfer
* Encrypted communication
* Remote deployment support

---

# 10. Container-Based Jenkins Agents

## 10.1 Introduction

Jenkins supports containerized agents using Docker.

Each pipeline runs inside isolated containers.

---

## 10.2 Example Pipeline

```groovy id="flow16"
pipeline {

    agent {
        docker {
            image 'maven:3.9'
        }
    }

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

## 10.3 Advantages

* Isolated environments
* Consistent builds
* Dependency management
* Portable pipelines

Container-based agents are widely used in cloud-native DevOps workflows.

---

# 11. Deployments to Servers

## 11.1 Introduction

Jenkins pipelines can deploy applications automatically to remote servers.

Deployment targets:

* Linux servers
* Virtual machines
* Bare-metal servers

---

## 11.2 Deployment Workflow

```text id="flow17"
Build Application
       ↓
Generate Artifact
       ↓
Transfer Artifact
       ↓
Restart Application
```

---

## 11.3 Example Deployment Script

```groovy id="flow18"
stage('Deploy') {

    steps {

        sh '''
        scp target/app.jar user@server:/deploy/
        ssh user@server "systemctl restart app"
        '''

    }

}
```

---

# 12. Deployments to Cloud Platforms

## 12.1 Introduction

Jenkins supports deployment to cloud environments such as:

* AWS
* Azure
* Google Cloud
* DigitalOcean

---

# 12.2 AWS Deployment

Example workflow:

```text id="flow19"
Jenkins
    ↓
AWS EC2 / ECS / EKS
```

---

## 12.3 Kubernetes Deployment

Example command:

```groovy id="flow20"
sh 'kubectl apply -f deployment.yaml'
```

---

## 12.4 Docker-Based Deployment

Example:

```groovy id="flow21"
sh 'docker run -d -p 8080:8080 myapp'
```

---

# 13. Complete Jenkins CI/CD Deployment Pipeline

Example deployment flow:

```text id="flow22"
Code Push
    ↓
Webhook Trigger
    ↓
Jenkins Pipeline
    ↓
Checkout Code
    ↓
Build Application
    ↓
Run Tests
    ↓
Package Artifact
    ↓
Build Docker Image
    ↓
Push Image to Registry
    ↓
Deploy to Server/Cloud
```

---

# 14. Real-World Usage

Organizations use Jenkins deployment flows for:

* Enterprise CI/CD
* Microservices deployment
* Cloud-native applications
* Kubernetes automation
* Docker deployment

Industries:

* Banking
* Healthcare
* E-commerce
* IT services

---

# 15. Pipeline Best Practices

## Use Webhooks Instead of pollSCM

Webhooks provide faster and more efficient triggering.

---

## Use Shared Libraries

Improves pipeline standardization and reusability.

---

## Use Container-Based Agents

Provides isolated and reproducible build environments.

---

## Secure Credentials

Store credentials using Jenkins Credentials Manager.

---

## Archive Artifacts

Store deployment artifacts for traceability.

---

## Monitor Pipelines

Track:

* Build failures
* Execution time
* Deployment status

---

# 16. Advantages of Jenkins CI/CD Deployment Flows

Jenkins deployment pipelines provide:

1. Automated software delivery
2. Faster deployment cycles
3. Better scalability
4. Continuous integration
5. Cloud deployment support
6. Reusable automation workflows
7. Improved software quality

These capabilities make Jenkins a leading enterprise CI/CD platform.

---

