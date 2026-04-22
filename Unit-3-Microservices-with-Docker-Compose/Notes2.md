
# 1. Introduction to Docker Compose

Docker Compose is designed to manage applications that require multiple containers working together. Instead of manually running multiple `docker run` commands, Docker Compose allows all services to be defined inside a single YAML file.

For example, a web application may require:

* Frontend container
* Backend container
* Database container
* Redis cache container

Managing these containers individually becomes complex. Docker Compose solves this problem by providing centralized configuration and orchestration.

Docker Compose is widely used in:

* Microservices architecture
* Local development environments
* CI/CD pipelines
* Multi-container applications

---

# 2. YAML Structure in Docker Compose

Docker Compose uses YAML (YAML Ain’t Markup Language) format for configuration.

YAML is:

* Human-readable
* Indentation-based
* Simple to understand

The configuration is stored inside:

```id="yaml1"
docker-compose.yml
```

A basic structure of a Docker Compose file is:

```yaml id="yaml2"
version: '3'

services:
  web:
    image: nginx
```

The YAML file defines:

* Compose version
* Services
* Networks
* Volumes
* Environment variables

---

# 3. Writing docker-compose.yml File

The `docker-compose.yml` file is the main configuration file used by Docker Compose.

It contains definitions for all containers and services required by the application.

Example:

```yaml id="yaml3"
version: '3'

services:
  web:
    image: nginx
    ports:
      - "8080:80"

  database:
    image: mysql
```

In this example:

* `web` service runs NGINX
* `database` service runs MySQL
* Both services start together

Docker Compose automatically creates networking between services.

---

# 4. Version in Docker Compose

The `version` field specifies the Compose file format version.

Example:

```yaml id="yaml4"
version: '3'
```

Different versions support different features.

Common versions include:

* Version 2
* Version 3
* Version 3.8

Version 3 is commonly used in modern Docker Compose configurations because it supports:

* Swarm compatibility
* Networking
* Volumes
* Secrets
* Configurations

The version field ensures compatibility between Docker Compose and Docker Engine.

---

# 5. Services in Docker Compose

The `services` section defines the containers that will run as part of the application.

Each service represents one container.

Example:

```yaml id="yaml5"
services:
  frontend:
    image: nginx

  backend:
    image: node

  database:
    image: mysql
```

In this configuration:

* Frontend service handles UI
* Backend service handles application logic
* Database service stores data

Each service can have:

* Ports
* Volumes
* Networks
* Environment variables
* Dependencies

Services communicate using service names as hostnames.

Example:

```id="yaml6"
backend → database
```

Docker Compose automatically creates internal DNS for communication.

---

# 6. Volumes in Docker Compose

Volumes are used for persistent data storage.

Containers are temporary by nature. If a container is deleted, its internal data may also be removed. Volumes solve this problem by storing data outside the container.

Example:

```yaml id="yaml7"
services:
  database:
    image: mysql
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```

In this example:

* `db_data` is a named volume
* MySQL data remains safe even if container stops

Advantages of volumes:

* Persistent storage
* Data backup
* Data sharing between containers
* Better performance

Volumes are commonly used for:

* Databases
* Logs
* Uploaded files

---

# 7. Networks in Docker Compose

Docker Compose automatically creates a default network for services.

Networks allow containers to communicate securely.

Example:

```yaml id="yaml8"
services:
  frontend:
    image: nginx

  backend:
    image: node
```

Both containers communicate through the same network.

Custom network example:

```yaml id="yaml9"
networks:
  app_network:
```

Service using network:

```yaml id="yaml10"
services:
  backend:
    image: node
    networks:
      - app_network
```

Advantages of networks:

* Secure communication
* Service discovery
* Isolation between applications

Docker Compose supports:

* Bridge networks
* Overlay networks
* Host networks

---

# 8. Environment Variables in Docker Compose

Environment variables are used to configure containers dynamically.

Example:

```yaml id="yaml11"
services:
  app:
    image: nginx
    environment:
      - APP_ENV=production
      - PORT=8080
```

Environment variables help in:

* Configuration management
* Security
* Portability

Common uses:

* Database credentials
* API keys
* Application modes

---

# 9. Using .env File

Docker Compose supports external `.env` files.

Example `.env` file:

```id="yaml12"
DB_HOST=localhost
DB_USER=root
DB_PASS=secret
```

Using variables:

```yaml id="yaml13"
services:
  database:
    environment:
      - MYSQL_ROOT_PASSWORD=${DB_PASS}
```

Advantages:

* Cleaner configuration
* Better security
* Easier management

---

# 10. Secrets and Configs

Secrets are used to securely manage sensitive data.

Examples:

* Passwords
* API keys
* Tokens

Example:

```yaml id="yaml14"
secrets:
  db_password:
    file: ./password.txt
```

Using secret:

```yaml id="yaml15"
services:
  database:
    secrets:
      - db_password
```

Benefits of secrets:

* Better security
* Sensitive data protection
* Avoid hardcoding passwords

Configs are used for non-sensitive configuration files.

Example:

* Application configuration
* NGINX config files

---

# 11. Build vs Image Fields in YAML

Docker Compose supports both `build` and `image`.

---

## 11.1 Image Field

The `image` field is used when pulling an existing image from Docker Hub or another registry.

Example:

```yaml id="yaml16"
services:
  web:
    image: nginx
```

Docker pulls the image automatically.

---

## 11.2 Build Field

The `build` field is used to build a custom image from a Dockerfile.

Example:

```yaml id="yaml17"
services:
  app:
    build: .
```

Docker Compose searches for a Dockerfile in the current directory.

Custom build example:

```yaml id="yaml18"
services:
  app:
    build:
      context: .
      dockerfile: Dockerfile.dev
```

---

## Difference Between Build and Image

| Feature             | build              | image               |
| ------------------- | ------------------ | ------------------- |
| Purpose             | Build custom image | Pull existing image |
| Requires Dockerfile | Yes                | No                  |
| Used for            | Development        | Deployment          |
| Source              | Local system       | Docker registry     |

---

# 12. Service Dependency Ordering

In microservices applications, some services depend on others.

Example:

* Backend depends on database
* API depends on Redis

Docker Compose uses `depends_on` to define dependencies.

Example:

```yaml id="yaml19"
services:
  backend:
    image: node
    depends_on:
      - database

  database:
    image: mysql
```

In this configuration:

* Database starts first
* Backend starts after database

Advantages:

* Proper startup sequence
* Reduced startup failures
* Better orchestration

However, `depends_on` only controls startup order and does not guarantee that the dependent service is fully ready.

---

# 13. Docker Compose Commands

Common Docker Compose commands:

### Start Services

```bash id="yaml20"
docker-compose up
```

---

### Start in Background

```bash id="yaml21"
docker-compose up -d
```

---

### Stop Services

```bash id="yaml22"
docker-compose down
```

---

### View Running Services

```bash id="yaml23"
docker-compose ps
```

---

### View Logs

```bash id="yaml24"
docker-compose logs
```

---

# 14. Advantages of Docker Compose

Docker Compose provides several advantages:

1. Simplifies multi-container deployment
2. Centralized configuration
3. Easy networking
4. Easy volume management
5. Better development workflow
6. Useful for CI/CD pipelines

Docker Compose is highly useful in microservices architecture because it allows developers to manage multiple services efficiently.

---

