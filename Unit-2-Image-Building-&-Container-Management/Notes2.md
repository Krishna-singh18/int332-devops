

# 1. Environment Variables in Docker

## 1.1 Definition

Environment variables are **key–value pairs** used by applications to:

* Read configuration
* Store secrets (username, password)
* Control application behavior

They allow containers to be configured **dynamically without changing the image**.

---

## 1.2 Need of Environment Variables

### Without `-e`

* Configuration is hard-coded
* Need to rebuild image for changes

---

### With `-e`

* Same image → different behavior
* Flexible configuration
* Used in microservices & cloud

---

## 1.3 Example: Setting Environment Variable

```bash
docker run -e MY_VAR=value httpd env
```

* Sets variable `MY_VAR=value`
* `env` command shows all variables

---

## 1.4 Example: Access Variable Inside Container

```bash
docker run -it -e MY_NAME=Harpreet ubuntu bash
```

Inside container:

```bash
echo $MY_NAME
```

### Note

* Variable exists only inside container
* Host system is not affected

---

## 1.5 Multiple Environment Variables

```bash
docker run -e APP_ENV=production -e APP_VERSION=1.0 nginx
```

---

## 1.6 Example: MySQL Container (Important)

```bash
docker run -d \
  -e MYSQL_ROOT_PASSWORD=root123 \
  -e MYSQL_DATABASE=college \
  -e MYSQL_USER=admin \
  -e MYSQL_PASSWORD=admin123 \
  mysql:8
```

Without these variables, MySQL container **will not start**.

---

## 1.7 Passing Environment Variable from Host

### Step 1: Set variable on host

```bash
export APP_PORT=8080
```

### Step 2: Use in container

```bash
docker run -e APP_PORT nginx env
```

---

## 1.8 Using `.env` File (Professional Method)

Create `.env` file:

```
DB_HOST=localhost
DB_USER=root
DB_PASS=secret
```

Run container:

```bash
docker run --env-file .env myapp
```

---

# 2. Running Containers with Flags

```bash
docker run -it -d httpd
```

Explanation:

* `-it` → interactive mode
* `-d` → background mode
* `httpd` → image name

---

# 3. Port Mapping (`-p`)

## 3.1 Definition

`-p` stands for **publish port**.

It maps:

```
Host Port → Container Port
```

---

## 3.2 Syntax

```bash
docker run -p <HOST_PORT>:<CONTAINER_PORT> IMAGE
```

---

## 3.3 Without Port Mapping

```bash
docker run nginx
```

* Container runs
* Not accessible from browser

---

## 3.4 With Port Mapping

```bash
docker run -p 8080:80 nginx
```

Now access:

```
http://localhost:8080
```

---

## 3.5 Internal Working

```
Browser → Host (8080) → Docker → Container (80)
```

---

## 3.6 Example: MySQL with Port

```bash
docker run -d -p 3307:3306 --name mysql-test -e MYSQL_ROOT_PASSWORD=root123 mysql
```

---

## 3.7 Access MySQL Container

```bash
docker exec -it mysql-test bash
```

```bash
mysql -h 127.0.0.1 -P 3306 -u root -p
```

---

# 4. Container Listing Commands

## Running Containers

```bash
docker ps
```

---

## All Containers

```bash
docker ps -a
```

---

# 5. Task Example

### Task

* Run Ubuntu container
* Pass environment variable `COLLEGE=CSE`
* Display value
* Stop container and observe

---

### Commands

```bash
docker run -it -e COLLEGE=CSE ubuntu bash
```

```bash
echo $COLLEGE
```

---

# 6. Docker Exec Command

```bash
docker exec -it container_id bash
```

Used to:

* Access running container
* Execute commands inside container

---

# 7. Removing Containers

```bash
docker rm container_id
```

Check removal:

```bash
docker ps -a
```

---

# 8. Removing Images

```bash
docker rmi image_id
```

Force remove:

```bash
docker rmi -f image_id
```

#
