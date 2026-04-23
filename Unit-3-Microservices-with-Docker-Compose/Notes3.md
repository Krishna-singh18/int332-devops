#  Use Case Deployments with Docker Compose

Modern applications are usually built using multiple interconnected services such as frontend applications, backend APIs, databases, authentication services, and caching systems. Managing these services individually becomes difficult in traditional deployment methods. Docker Compose simplifies this process by allowing developers to deploy and manage multi-container applications using a single configuration file.

This unit explains real-world deployment use cases using Docker Compose including:

* Multi-container applications
* WordPress + MySQL deployment
* Node.js + MongoDB deployment
* Java Spring Boot + PostgreSQL deployment



---

# 1. Multi-Container Applications

## 1.1 Introduction

A multi-container application is an application where multiple containers work together to provide complete functionality.

Modern software systems rarely use a single container because applications usually require:

* Frontend service
* Backend service
* Database service
* Cache service
* API gateway

Each component runs independently in its own container.

Docker Compose allows all containers to communicate using internal Docker networks.

---

## 1.2 Example Architecture

Example of a typical web application:

```id="multi1"
Frontend (React / Angular)
            ↓
Backend API (Node.js / Spring Boot)
            ↓
Database (MySQL / MongoDB / PostgreSQL)
```

Each service performs a specific role.

---

## 1.3 Advantages of Multi-Container Applications

### 1. Scalability

Each service can scale independently.

Example:

* Database may require more memory
* Frontend may require more replicas

---

### 2. Isolation

Failure in one service does not crash the complete application.

---

### 3. Flexibility

Different services can use different technologies.

Example:

* Frontend → React
* Backend → Node.js
* Database → MongoDB

---

### 4. Easier Maintenance

Small services are easier to debug and update.

---

# 2. WordPress + MySQL Deployment

## 2.1 Introduction

WordPress is a popular content management system (CMS) used to build websites and blogs. WordPress requires a database to store:

* User data
* Posts
* Themes
* Settings

MySQL is commonly used as the backend database.

Docker Compose simplifies deployment by running both WordPress and MySQL containers together.

---

## 2.2 Architecture

```id="wp1"
Browser
   ↓
WordPress Container
   ↓
MySQL Container
```

The WordPress container communicates with MySQL using Docker networking.

---

## 2.3 Docker Compose Configuration

Example `docker-compose.yml`:

```yaml id="wp2"
version: '3'

services:

  wordpress:
    image: wordpress
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: root
      WORDPRESS_DB_PASSWORD: root123
      WORDPRESS_DB_NAME: wordpress
    depends_on:
      - db

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root123
      MYSQL_DATABASE: wordpress
```

---

## 2.4 Explanation

### WordPress Service

* Runs WordPress application
* Accessible on port 8080
* Uses environment variables to connect database

---

### Database Service

* Runs MySQL container
* Stores WordPress data

---

### depends_on

Ensures database container starts before WordPress.

---

## 2.5 Running the Application

Start services:

```bash id="wp3"
docker-compose up -d
```

Open browser:

```id="wp4"
http://localhost:8080
```

---

## 2.6 Advantages

* Easy setup
* Portable deployment
* Fast development environment
* Real-world CMS deployment

---

# 3. Node.js + MongoDB Deployment

## 3.1 Introduction

Node.js is widely used for backend API development. MongoDB is a NoSQL database used for storing JSON-like documents.

This combination is very common in MERN stack applications.

Docker Compose helps developers deploy both services together.

---

## 3.2 Architecture

```id="node1"
Client
   ↓
Node.js Backend
   ↓
MongoDB Database
```

---

## 3.3 Docker Compose Configuration

```yaml id="node2"
version: '3'

services:

  backend:
    build: .
    ports:
      - "3000:3000"
    environment:
      MONGO_URL: mongodb://mongo:27017/mydb
    depends_on:
      - mongo

  mongo:
    image: mongo
    ports:
      - "27017:27017"
```

---

## 3.4 Explanation

### Backend Service

* Builds Node.js application
* Runs on port 3000
* Connects MongoDB using service name `mongo`

---

### MongoDB Service

* Runs MongoDB container
* Stores application data

---

## 3.5 Internal Networking

Docker Compose automatically creates communication between services.

Example connection string:

```id="node3"
mongodb://mongo:27017/mydb
```

Here:

* `mongo` = service name
* Docker DNS resolves service automatically

---

## 3.6 Running Application

```bash id="node4"
docker-compose up -d
```

Access application:

```id="node5"
http://localhost:3000
```

---

## 3.7 Advantages

* Simplified development
* Easy database integration
* Consistent environments
* Faster deployment

---

# 4. Java Spring Boot + PostgreSQL Deployment

## 4.1 Introduction

Spring Boot is a popular Java framework used for enterprise applications. PostgreSQL is an advanced relational database management system.

Docker Compose helps deploy Spring Boot applications with PostgreSQL in isolated containers.

---

## 4.2 Architecture

```id="java1"
Client
   ↓
Spring Boot Application
   ↓
PostgreSQL Database
```

---

## 4.3 Docker Compose Configuration

```yaml id="java2"
version: '3'

services:

  app:
    build: .
    ports:
      - "8081:8080"
    environment:
      SPRING_DATASOURCE_URL: jdbc:postgresql://postgres:5432/mydb
      SPRING_DATASOURCE_USERNAME: admin
      SPRING_DATASOURCE_PASSWORD: admin123
    depends_on:
      - postgres

  postgres:
    image: postgres
    environment:
      POSTGRES_DB: mydb
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: admin123
```

---

## 4.4 Explanation

### Spring Boot Service

* Builds Java application
* Runs on port 8081
* Connects PostgreSQL database

---

### PostgreSQL Service

* Runs PostgreSQL database
* Stores enterprise data

---

## 4.5 Database Connection

Spring Boot uses JDBC connection:

```id="java3"
jdbc:postgresql://postgres:5432/mydb
```

Where:

* `postgres` = service name
* `5432` = PostgreSQL default port

---

## 4.6 Running Application

```bash id="java4"
docker-compose up -d
```

Access application:

```id="java5"
http://localhost:8081
```

---

## 4.7 Advantages

* Enterprise deployment support
* Database isolation
* Easy configuration
* Suitable for cloud deployment

---

# 5. Docker Compose Networking in Use Cases

In all use cases:

* Containers communicate internally
* Service names act as hostnames
* Docker creates isolated networks automatically

Example:

```id="net1"
frontend → backend → database
```

This simplifies communication and reduces manual networking configuration.

---

# 6. Persistent Storage with Volumes

Databases require persistent storage because container deletion should not remove data.

Example:

```yaml id="vol1"
volumes:
  - db_data:/var/lib/mysql
```

Benefits:

* Data persistence
* Backup support
* Container independence

---

# 7. Environment Variables in Deployments

Environment variables are heavily used for configuration.

Examples:

* Database passwords
* API keys
* Connection strings

Example:

```yaml id="env1"
environment:
  MYSQL_ROOT_PASSWORD: root123
```

Advantages:

* Flexible configuration
* Security
* Reusable images

---

# 8. Service Dependencies

Services often depend on databases or backend APIs.

Example:

```yaml id="dep1"
depends_on:
  - database
```

This ensures proper startup order.

---

# 9. Real-World Importance

These deployment patterns are widely used in:

* Cloud-native applications
* DevOps pipelines
* Kubernetes environments
* Enterprise software
* SaaS platforms

Companies use Docker Compose during development and testing before deploying applications to Kubernetes clusters.

---

