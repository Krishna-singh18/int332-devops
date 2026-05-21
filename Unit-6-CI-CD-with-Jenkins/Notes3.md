
# 1. Introduction to Maven

## 1.1 Definition

Maven is an open-source build automation and dependency management tool primarily used for Java applications.

Maven simplifies:

* Project building
* Dependency management
* Testing
* Packaging
* Deployment

Maven uses:

```text id="mvn1"
pom.xml
```

(Project Object Model) file to define project configuration.

---

## 1.2 Why Maven Is Important

Before Maven, developers manually managed:

* Libraries
* Build scripts
* Compilation
* Packaging

This created problems such as:

* Dependency conflicts
* Complex builds
* Inconsistent project structures

Maven solves these issues through standardized build processes.

---

## 1.3 Features of Maven

Maven provides:

1. Dependency management
2. Standard project structure
3. Automated builds
4. Plugin support
5. Test execution
6. Packaging support

---

# 2. Jenkins and Maven Integration

## 2.1 Introduction

Jenkins integrates with Maven to automate Java application builds.

Jenkins can automatically:

* Download source code
* Execute Maven commands
* Run tests
* Generate artifacts
* Archive reports

This automation improves software delivery speed and reliability.

---

## 2.2 Basic Workflow

Example workflow:

```text id="mvn2"
Developer Pushes Code
          ↓
GitHub Repository
          ↓
Jenkins Pipeline Triggered
          ↓
Maven Build Starts
          ↓
Compile Source Code
          ↓
Run Tests
          ↓
Generate Artifact
          ↓
Store Reports
```

---

# 3. Maven Installation in Jenkins

## 3.1 Introduction

Jenkins requires Maven installation before executing Maven builds.

Maven can be installed:

* Manually on system
* Automatically through Jenkins tools configuration

---

# 3.2 Prerequisites

Before Maven installation:

* Java JDK must be installed
* Jenkins must be running

Check Java version:

```bash id="mvn3"
java -version
```

Check Maven version:

```bash id="mvn4"
mvn -version
```

---

# 3.3 Installing Maven Manually

### Steps

1. Download Maven
2. Extract Maven files
3. Configure environment variables
4. Add Maven to PATH

---

## 3.4 Maven Directory Structure

Example:

```text id="mvn5"
apache-maven/
│
├── bin/
├── conf/
├── lib/
└── boot/
```

Important folder:

```text id="mvn6"
bin/
```

Contains Maven executable files.

---

# 3.5 Configure Environment Variables

Environment variables required:

| Variable   | Purpose                 |
| ---------- | ----------------------- |
| JAVA_HOME  | Java installation path  |
| MAVEN_HOME | Maven installation path |
| PATH       | Access Maven globally   |

Example:

```bash id="mvn7"
export MAVEN_HOME=/opt/maven
export PATH=$PATH:$MAVEN_HOME/bin
```

---

# 4. Global Tool Configuration in Jenkins

## 4.1 Introduction

Jenkins provides centralized tool management through Global Tool Configuration.

This allows Jenkins to manage:

* Maven
* Java JDK
* Git
* Gradle

centrally.

---

## 4.2 Steps to Configure Maven

### Step 1

Open:

```text id="mvn8"
Manage Jenkins
```

---

### Step 2

Select:

```text id="mvn9"
Tools
```

or

```text id="mvn10"
Global Tool Configuration
```

---

### Step 3

Locate:

```text id="mvn11"
Maven Installations
```

---

### Step 4

Add Maven installation.

Options:

* Install automatically
* Use local Maven installation

---

## 4.3 Automatic Maven Installation

Jenkins can download Maven automatically.

Example configuration:

```text id="mvn12"
Name: Maven-3.9
Version: 3.9.x
```

Advantages:

* Easy setup
* Consistent environments
* Centralized management

---

## 4.4 JDK Configuration

JDK configuration is also required.

Example:

```text id="mvn13"
JDK Name: JDK17
JAVA_HOME: /usr/lib/jvm/java-17
```

---

# 5. Running Maven Builds in Jenkins

## 5.1 Introduction

Jenkins can execute Maven commands inside:

* Freestyle jobs
* Pipeline jobs

This automates project builds and testing.

---

# 5.2 Maven Build Lifecycle

Maven follows a build lifecycle.

Common phases:

| Phase    | Purpose                  |
| -------- | ------------------------ |
| validate | Validate project         |
| compile  | Compile source code      |
| test     | Run tests                |
| package  | Generate JAR/WAR         |
| install  | Install artifact locally |
| deploy   | Deploy artifact          |

---

# 5.3 Maven Build Commands

Common commands:

```bash id="mvn14"
mvn clean
```

Removes old build files.

---

```bash id="mvn15"
mvn compile
```

Compiles source code.

---

```bash id="mvn16"
mvn test
```

Runs unit tests.

---

```bash id="mvn17"
mvn package
```

Creates deployable artifact.

---

```bash id="mvn18"
mvn clean install
```

Performs full build process.

---

# 5.4 Running Maven Build in Freestyle Job

## Steps

1. Create Jenkins job
2. Select Freestyle Project
3. Configure Git repository
4. Add build step
5. Select Invoke Top-Level Maven Targets

---

## Maven Goals Example

```text id="mvn19"
clean install
```

Jenkins automatically executes Maven build.

---

# 5.5 Running Maven Build in Pipeline Job

Pipeline example:

```groovy id="mvn20"
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

# 5.6 Explanation

### Agent

Defines execution environment.

---

### Stage

Represents pipeline phase.

---

### Steps

Contains commands executed by Jenkins.

---

### sh

Executes shell commands.

---

# 6. Maven Build Stages in Jenkins Pipelines

Pipelines usually contain multiple Maven stages.

Example:

```text id="mvn21"
Checkout
   ↓
Compile
   ↓
Test
   ↓
Package
   ↓
Deploy
```

---

# 7. Checkout Source Code

Source code is downloaded from Git repository.

Example:

```groovy id="mvn22"
git 'https://github.com/user/repo.git'
```

---

# 8. Compile Stage

Compiles Java source files.

Example:

```groovy id="mvn23"
sh 'mvn compile'
```

Generated files:

```text id="mvn24"
target/classes/
```

---

# 9. Test Stage

Runs automated unit tests.

Example:

```groovy id="mvn25"
sh 'mvn test'
```

Testing frameworks:

* JUnit
* TestNG

---

# 10. Package Stage

Creates deployable artifacts.

Example:

```groovy id="mvn26"
sh 'mvn package'
```

Generated outputs:

* JAR
* WAR

Stored inside:

```text id="mvn27"
target/
```

---

# 11. Install Stage

Installs artifacts into local Maven repository.

Example:

```groovy id="mvn28"
sh 'mvn install'
```

Local repository:

```text id="mvn29"
~/.m2/repository
```

---

# 12. Deploy Stage

Uploads artifacts to remote repository.

Example:

```groovy id="mvn30"
sh 'mvn deploy'
```

Common repositories:

* Nexus
* Artifactory

---

# 13. Code Coverage

## 13.1 Introduction

Code coverage measures how much application code is tested.

It helps identify:

* Untested code
* Weak test cases
* Risk areas

---

## 13.2 Benefits of Code Coverage

* Better software quality
* Improved testing
* Early bug detection
* Higher reliability

---

# 13.3 Popular Code Coverage Tools

| Tool      | Purpose            |
| --------- | ------------------ |
| JaCoCo    | Java code coverage |
| Cobertura | Coverage reports   |
| Clover    | Coverage analysis  |

---

# 13.4 JaCoCo Example

Maven dependency:

```xml id="mvn31"
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
</plugin>
```

---

# 13.5 Generate Coverage Report

Example command:

```bash id="mvn32"
mvn test jacoco:report
```

Generated reports:

```text id="mvn33"
target/site/jacoco/
```

---

# 14. Test Reports in Jenkins

## 14.1 Introduction

Jenkins can display automated test reports.

Test reports provide:

* Passed tests
* Failed tests
* Error details
* Execution statistics

---

# 14.2 JUnit Reports

JUnit reports are commonly used.

Example pipeline step:

```groovy id="mvn34"
junit 'target/surefire-reports/*.xml'
```

---

# 14.3 Surefire Plugin

Maven Surefire Plugin executes unit tests.

Example configuration:

```xml id="mvn35"
<plugin>
    <artifactId>maven-surefire-plugin</artifactId>
</plugin>
```

---

# 14.4 Test Report Workflow

```text id="mvn36"
Run Tests
     ↓
Generate XML Reports
     ↓
Jenkins Reads Reports
     ↓
Display Test Results
```

---

# 15. Artifact Management in Jenkins

## 15.1 Introduction

Artifacts are generated outputs from Maven builds.

Examples:

* JAR files
* WAR files
* Reports

---

## 15.2 Archive Artifacts

Example:

```groovy id="mvn37"
archiveArtifacts artifacts: 'target/*.jar'
```

---

## 15.3 Benefits

* Easy artifact download
* Deployment reuse
* Build traceability

---

# 16. Complete Jenkins Maven Pipeline Example

```groovy id="mvn38"
pipeline {

    agent any

    tools {
        maven 'Maven-3.9'
    }

    stages {

        stage('Checkout') {

            steps {
                git 'https://github.com/user/repo.git'
            }

        }

        stage('Build') {

            steps {
                sh 'mvn clean compile'
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

            junit 'target/surefire-reports/*.xml'

            archiveArtifacts artifacts: 'target/*.jar'

        }

    }

}
```

---

# 17. Advantages of Jenkins and Maven Integration

This integration provides several benefits:

1. Automated Java builds
2. Dependency management
3. Continuous testing
4. Artifact generation
5. Build standardization
6. Faster software delivery
7. Better CI/CD automation

---

# 18. Real-World Usage

Organizations use Jenkins and Maven integration for:

* Enterprise Java applications
* Spring Boot projects
* Microservices
* Cloud-native applications
* CI/CD automation

Industries:

* Banking
* Healthcare
* E-commerce
* IT services

---

# 19. Best Practices

## Use Pipeline as Code

Store Jenkinsfile inside repository.

---

## Use Separate Build Stages

Separate:

* Build
* Test
* Package
* Deploy

---

## Archive Reports

Store artifacts and test reports for debugging.

---

## Use Automated Testing

Always execute tests before deployment.

---

## Use Dependency Caching

Improves build performance.

---


