# Maven Commands Cheat Sheet


<br>

# 1. Maven Installation & Version Commands

## Check Maven Version

```bash id="mvc1"
mvn --version
```

Displays:

* Maven version
* Java version
* Maven home directory

---

## Check Java Version

```bash id="mvc2"
java --version
```

---

# 2. Maven Project Creation Commands

## Create New Maven Project

```bash id="mvc3"
mvn archetype:generate
```

Used to generate a Maven project from templates.

---

## Generate Quickstart Project

```bash id="mvc4"
mvn archetype:generate `
-DgroupId=com.example `
-DartifactId=myapp `
-DarchetypeArtifactId=maven-archetype-quickstart `
-DinteractiveMode=false
```

---

# 3. Maven Build Lifecycle Commands

## Validate Project

```bash id="mvc5"
mvn validate
```

Checks project structure and `pom.xml`.

---

## Compile Source Code

```bash id="mvc6"
mvn compile
```

Compiles Java source files.

---

## Run Unit Tests

```bash id="mvc7"
mvn test
```

Executes test cases using Surefire Plugin.

---

## Package Application

```bash id="mvc8"
mvn package
```

Creates:

* JAR file
* WAR file

inside:

```id="mvc9"
target/
```

---

## Verify Application

```bash id="mvc10"
mvn verify
```

Runs integration checks and validations.

---

## Install Artifact Locally

```bash id="mvc11"
mvn install
```

Installs package into:

```id="mvc12"
.m2/repository
```

---

## Deploy Artifact

```bash id="mvc13"
mvn deploy
```

Deploys package to remote repository.

---

# 4. Maven Clean Commands

## Remove Previous Build Files

```bash id="mvc14"
mvn clean
```

Deletes:

```id="mvc15"
target/
```

directory.

---

## Clean and Build Project

```bash id="mvc16"
mvn clean install
```

Performs:

* clean
* compile
* test
* package
* install

---

# 5. Dependency Management Commands

## Download Dependencies

```bash id="mvc17"
mvn dependency:resolve
```

---

## Show Dependency Tree

```bash id="mvc18"
mvn dependency:tree
```

Displays transitive dependencies.

---

## Analyze Dependencies

```bash id="mvc19"
mvn dependency:analyze
```

Detects:

* unused dependencies
* missing dependencies

---

# 6. Maven Plugin Commands

## Run Compiler Plugin

```bash id="mvc20"
mvn compiler:compile
```

---

## Run Surefire Plugin

```bash id="mvc21"
mvn surefire:test
```

---

## Run Shade Plugin

```bash id="mvc22"
mvn shade:shade
```

Creates executable Uber JAR.

---

# 7. Maven Wrapper Commands

## Linux / Mac

```bash id="mvc23"
./mvnw clean install
```

---

## Windows

```bash id="mvc24"
mvnw.cmd clean install
```

---

# 8. Maven Docker Integration Commands

## Build Maven Project

```bash id="mvc25"
mvn clean package
```

---

## Build Docker Image

```bash id="mvc26"
docker build -t myapp:1.0 .
```

---

## Run Docker Container

```bash id="mvc27"
docker run -d -p 8080:8080 myapp:1.0
```

---

## Build Docker Image Using Maven Plugin

```bash id="mvc28"
mvn dockerfile:build
```

---

## Push Docker Image

```bash id="mvc29"
docker push username/myapp:1.0
```

---

# 9. Maven Repository Commands

## Install Local JAR

```bash id="mvc30"
mvn install:install-file `
-Dfile=myapp.jar `
-DgroupId=com.example `
-DartifactId=myapp `
-Dversion=1.0 `
-Dpackaging=jar
```

---

## Download Artifact

```bash id="mvc31"
mvn dependency:get -Dartifact=junit:junit:4.13.2
```

---

# 10. Useful Maven Options

| Option        | Description             |
| ------------- | ----------------------- |
| `-DskipTests` | Skip unit tests         |
| `-X`          | Debug mode              |
| `-q`          | Quiet mode              |
| `-o`          | Offline mode            |
| `-U`          | Force dependency update |

---

## Example

Skip tests during build:

```bash id="mvc32"
mvn clean package -DskipTests
```

---

# 11. Maven Lifecycle Summary

```id="mvc33"
validate
   ↓
compile
   ↓
test
   ↓
package
   ↓
verify
   ↓
install
   ↓
deploy
```

---

# 12. Common Maven Plugins

| Plugin          | Purpose           |
| --------------- | ----------------- |
| Compiler Plugin | Compile Java code |
| Surefire Plugin | Run unit tests    |
| Shade Plugin    | Create Uber JAR   |
| WAR Plugin      | Create WAR files  |
| JAR Plugin      | Create JAR files  |

---

# 13. Important Maven Files

| File         | Purpose             |
| ------------ | ------------------- |
| pom.xml      | Maven configuration |
| settings.xml | Maven settings      |
| mvnw         | Maven wrapper       |
| target/      | Build output        |

---

# 14. Quick DevOps Workflow

```id="mvc34"
GitHub
   ↓
Maven Build
   ↓
Unit Testing
   ↓
Package JAR
   ↓
Docker Build
   ↓
Push to Registry
   ↓
Deployment
```

---

# 15. Important Notes

* Maven automates build and dependency management
* Plugins perform actual tasks
* `pom.xml` is the heart of Maven
* Maven integrates easily with Docker and CI/CD pipelines
* Maven Wrapper ensures consistent builds
