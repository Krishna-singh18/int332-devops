
# 1. Checking Docker Version and Information

## 1.1 Check Docker Version

```id="v1cmd"
docker --version
```

Displays the installed Docker version.

---

## 1.2 Docker System Information

```id="v2cmd"
docker info
```

Provides detailed information about Docker:

* Kernel version
* Number of containers
* Number of images
* Storage driver
* System resources

---

# 2. Checking Image History

```id="v3cmd"
docker history httpd
```

Displays the history of a Docker image including:

* Image layers
* Commands used to create layers
* Size of each layer

---

# 3. Pulling Docker Images

To download an image from Docker Hub:

```id="v4cmd"
docker pull httpd
```

Example:

* Pulls Apache HTTP Server image from Docker Hub
* Stores it locally

---

# 4. Listing Docker Images

```id="v5cmd"
docker images
```

Displays all images available on the system with details:

* Repository
* Tag
* Image ID
* Size

---

# 5. Docker Run Command

## 5.1 Definition

The `docker run` command is used to:

* Create a container
* Start the container

---

## 5.2 Syntax

```id="v6cmd"
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

### Explanation

* **OPTIONS** → configuration flags
* **IMAGE** → image name
* **COMMAND** → command to run inside container
* **ARG** → arguments for the command

---

## 5.3 Common Options

| Option   | Description                       |
| -------- | --------------------------------- |
| `-it`    | Interactive terminal              |
| `-d`     | Run in background (detached mode) |
| `--name` | Assign container name             |
| `--rm`   | Remove container after exit       |
| `-p`     | Port mapping                      |
| `-e`     | Set environment variable          |
| `-v`     | Mount volume                      |

---

## 5.4 Meaning of `-d`

```id="v7cmd"
-d
```

Runs the container in **detached mode (background)**.

---

# 6. Examples of Docker Run

## 6.1 Example 1: Simple Container Execution

```id="v8cmd"
docker run httpd echo "Hello, World!"
```

Explanation:

* Runs container using `httpd` image
* Executes `echo` command
* Prints output inside container

---

## 6.2 Example 2: Container with Name

```id="v9cmd"
docker run --name my-container httpd echo "Hello, World!"
```

Explanation:

* `--name` → assigns container name
* `my-container` → container name
* `echo` → command
* `"Hello, World!"` → argument

This command creates and runs a container named **my-container**.

