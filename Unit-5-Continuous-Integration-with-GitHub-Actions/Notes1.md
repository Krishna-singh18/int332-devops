# Continuous Integration (CI) with GitHub Actions

Continuous Integration (CI) is one of the most important practices in modern DevOps and software engineering. It allows developers to automatically build, test, and validate applications whenever changes are pushed to a repository. GitHub Actions is a powerful automation platform provided by GitHub that enables developers to create CI/CD pipelines directly inside GitHub repositories.

GitHub Actions helps automate software workflows such as:

* Code compilation
* Automated testing
* Docker image building
* Deployment
* Notifications
* Security scanning

GitHub Actions uses workflow files written in YAML format to define automation pipelines.

---

# 1. Introduction to Continuous Integration (CI)

Continuous Integration (CI) is a software development practice where developers frequently merge code changes into a shared repository. Every code change is automatically built and tested to detect errors early.

The main goal of CI is to:

* Improve code quality
* Detect bugs early
* Reduce integration problems
* Automate software validation

In traditional development, developers worked separately for long periods and merged code manually, causing conflicts and failures. CI solves this problem by integrating changes continuously.

Example CI Workflow:

```id="gha1"
Developer Pushes Code
        ↓
GitHub Actions Triggered
        ↓
Code Build
        ↓
Automated Tests
        ↓
Success / Failure Report
```

CI is a core practice in DevOps because it supports faster and more reliable software delivery.

---

# 2. Introduction to GitHub Actions

GitHub Actions is GitHub’s built-in automation platform used for Continuous Integration and Continuous Deployment (CI/CD).

It allows developers to automate workflows directly inside GitHub repositories without external tools.

GitHub Actions can automate:

* Project builds
* Unit testing
* Docker builds
* Code analysis
* Deployment pipelines
* Scheduled tasks

Workflows are defined using YAML configuration files stored inside the repository.

GitHub Actions works on the concept:

```id="gha2"
Event → Workflow → Jobs → Steps
```

---

# 3. Understanding Workflow Automation

Workflow automation means automatically executing predefined tasks when specific events occur.

In GitHub Actions:

* A workflow defines automation logic
* Events trigger workflows
* Jobs execute tasks
* Steps perform individual actions

Example:

When a developer pushes code:

1. Workflow starts automatically
2. Application is compiled
3. Unit tests are executed
4. Build status is generated

This automation removes manual effort and improves software quality.

---

# 4. Workflow Directory Structure

GitHub Actions workflows are stored inside:

```id="gha3"
.github/workflows/
```

Example project structure:

```id="gha4"
project/
│
├── src/
├── pom.xml
├── Dockerfile
│
└── .github/
    └── workflows/
        └── ci.yml
```

---

## Explanation

### .github

Special GitHub directory used for automation and configuration.

---

### workflows

Contains workflow YAML files.

---

### ci.yml

Defines CI pipeline configuration.

---

# 5. Workflow File Structure

A workflow file is written in YAML format.

Basic example:

```yaml id="gha5"
name: Java CI

on:
  push:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Build Project
        run: mvn package
```

---

# 6. Key Components of GitHub Actions

GitHub Actions consists of several important components.

---

# 7. Workflows

## 7.1 Definition

A workflow is an automated process defined inside a YAML file.

A workflow contains:

* Events
* Jobs
* Steps
* Actions

A repository can contain multiple workflows.

Example:

* CI workflow
* Deployment workflow
* Security scanning workflow

---

## 7.2 Workflow Example

```yaml id="gha6"
name: Build Workflow
```

This defines workflow name.

---

# 8. Jobs

## 8.1 Definition

A job is a collection of steps executed on the same runner.

Each workflow can contain multiple jobs.

Example:

```yaml id="gha7"
jobs:
  build:
  test:
  deploy:
```

---

## 8.2 Job Features

Jobs can:

* Run independently
* Run sequentially
* Share outputs

Example:

```id="gha8"
Build Job → Test Job → Deploy Job
```

---

## 8.3 Example Job

```yaml id="gha9"
jobs:
  build:
    runs-on: ubuntu-latest
```

This creates a build job using Ubuntu runner.

---

# 9. Steps

## 9.1 Definition

Steps are individual tasks executed inside a job.

Each step performs a specific action.

Examples:

* Checkout code
* Install dependencies
* Run tests
* Build project

---

## 9.2 Example Steps

```yaml id="gha10"
steps:
  - uses: actions/checkout@v4

  - name: Run Tests
    run: mvn test
```

---

## Explanation

### uses

Executes reusable GitHub Action.

---

### run

Executes shell command.

---

# 10. Actions

## 10.1 Definition

Actions are reusable automation components.

GitHub provides official actions for common tasks.

Examples:

* Checkout repository
* Setup Java
* Setup Node.js
* Docker login

---

## 10.2 Popular Actions

| Action              | Purpose               |
| ------------------- | --------------------- |
| actions/checkout    | Clone repository      |
| actions/setup-java  | Install Java          |
| actions/setup-node  | Install Node.js       |
| docker/login-action | Docker authentication |

---

## 10.3 Example

```yaml id="gha11"
- uses: actions/setup-java@v4
```

Installs Java environment.

---

# 11. Runners

## 11.1 Definition

A runner is a machine that executes GitHub Actions workflows.

GitHub provides hosted runners.

Supported operating systems:

* Ubuntu
* Windows
* macOS

---

## 11.2 Example Runner

```yaml id="gha12"
runs-on: ubuntu-latest
```

This job executes on Ubuntu virtual machine.

---

## 11.3 Self-Hosted Runners

Organizations can also use their own servers as runners.

Advantages:

* Better control
* Custom software
* Internal infrastructure support

---

# 12. Workflow Triggers

Workflow triggers define when workflows should start.

Triggers are defined using:

```yaml id="gha13"
on:
```

---

# 13. Push Trigger

## 13.1 Definition

The `push` trigger runs workflow when code is pushed to repository.

Example:

```yaml id="gha14"
on:
  push:
```

---

## 13.2 Branch-Specific Push Trigger

```yaml id="gha15"
on:
  push:
    branches:
      - main
```

Workflow runs only for `main` branch.

---

# 14. Pull Request Trigger

## 14.1 Definition

The `pull_request` trigger runs workflows when pull requests are created or updated.

Example:

```yaml id="gha16"
on:
  pull_request:
```

---

## 14.2 Purpose

Used for:

* Code review validation
* Automated testing
* Merge verification

This improves code quality before merging.

---

# 15. Schedule Trigger

## 15.1 Definition

The `schedule` trigger runs workflows automatically at specified times.

Uses cron syntax.

Example:

```yaml id="gha17"
on:
  schedule:
    - cron: '0 0 * * *'
```

Runs workflow daily at midnight.

---

## 15.2 Uses of Schedule Trigger

* Backup automation
* Security scanning
* Dependency updates
* Scheduled testing

---

# 16. Complete Workflow Example

Example CI workflow:

```yaml id="gha18"
name: Maven CI

on:
  push:
    branches:
      - main

jobs:
  build:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - name: Setup Java
        uses: actions/setup-java@v4
        with:
          java-version: '17'

      - name: Build Project
        run: mvn clean install
```

---

# 17. Workflow Execution Process

Workflow execution flow:

```id="gha19"
Developer Pushes Code
          ↓
GitHub Detects Event
          ↓
Workflow Triggered
          ↓
Runner Created
          ↓
Jobs Executed
          ↓
Steps Executed
          ↓
Build Result Generated
```

---

# 18. Advantages of GitHub Actions

GitHub Actions provides several advantages:

1. Built-in CI/CD support
2. Easy GitHub integration
3. YAML-based configuration
4. Automated testing
5. Multi-platform support
6. Large marketplace of actions
7. Cloud-hosted runners

GitHub Actions simplifies DevOps automation significantly.

---

# 19. Real-World Usage

GitHub Actions is widely used for:

* Java Maven builds
* Docker image builds
* Kubernetes deployment
* Automated testing
* Security scanning
* CI/CD pipelines

Companies use GitHub Actions to automate software delivery pipelines efficiently.

---

