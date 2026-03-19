# Docker Commands Cheat Sheet

This cheat sheet covers essential Docker commands including **Quick Start, Containers, Images, Interaction, Volumes, Networks, and Cleanup**.

---

# 🚀 1. Docker Quick Start Commands

## 🔹 Check Installation

```
docker --version
docker info
```

---

## 🔹 Run Your First Container

```
docker run hello-world
```

---

## 🔹 Run Interactive Container

```
docker run -it ubuntu bash
```

### Important Flags

* `-i` → interactive mode
* `-t` → terminal (TTY)
* `-d` → detached mode (background)
* `--name` → assign container name

Example:

```
docker run -it --name mycontainer ubuntu
```

---

## 🔹 Run in Background

```
docker run -d nginx
```

---

## 🔹 List Containers

```
docker ps        # running containers
docker ps -a     # all containers
```

---

# 📦 2. Image Commands

## 🔹 List Images

```
docker images
```

---

## 🔹 Pull Image

```
docker pull nginx
```

---

## 🔹 Build Image

```
docker build -t myapp:1.0 .
```

### Flags

* `-t` → tag (name:version)
* `.` → current directory (build context)

---

## 🔹 Remove Image

```
docker rmi image_id
docker rmi -f image_id
```

---

## 🔹 Inspect Image

```
docker inspect image_id
```

---

## 🔹 Image History

```
docker history image_name
```

---

# 📦 3. Container Commands

## 🔹 Create Container

```
docker create nginx
```

---

## 🔹 Run Container

```
docker run nginx
```

---

## 🔹 Start / Stop / Restart

```
docker start container_id
docker stop container_id
docker restart container_id
```

---

## 🔹 Pause / Unpause

```
docker pause container_id
docker unpause container_id
```

---

## 🔹 Kill Container

```
docker kill container_id
```

---

## 🔹 Remove Container

```
docker rm container_id
docker rm -f container_id
```

---

## 🔹 Rename Container

```
docker rename old_name new_name
```

---

# 💬 4. Container Interaction Commands

## 🔹 Execute Command Inside Container

```
docker exec -it container_id bash
```

---

## 🔹 Attach to Container

```
docker attach container_id
```

---

## 🔹 View Logs

```
docker logs container_id
docker logs -f container_id
```

---

## 🔹 Copy Files

### Container → Host

```
docker cp container_id:/path/file .
```

### Host → Container

```
docker cp file container_id:/path/
```

---

## 🔹 Inspect Container

```
docker inspect container_id
```

---

## 🔹 Container Stats

```
docker stats
```

---

# 💾 5. Volume Commands

## 🔹 Create Volume

```
docker volume create myvolume
```

---

## 🔹 List Volumes

```
docker volume ls
```

---

## 🔹 Inspect Volume

```
docker volume inspect myvolume
```

---

## 🔹 Use Volume in Container

```
docker run -d -v myvolume:/data nginx
```

---

## 🔹 Bind Mount (Host Path)

```
docker run -d -v /host/path:/container/path nginx
```

---

## 🔹 Remove Volume

```
docker volume rm myvolume
```

---

## 🔹 Remove Unused Volumes

```
docker volume prune
```

---

# 🌐 6. Network Commands

## 🔹 List Networks

```
docker network ls
```

---

## 🔹 Create Network

```
docker network create mynetwork
```

---

## 🔹 Inspect Network

```
docker network inspect mynetwork
```

---

## 🔹 Connect / Disconnect Container

```
docker network connect mynetwork container_id
docker network disconnect mynetwork container_id
```

---

## 🔹 Remove Network

```
docker network rm mynetwork
```

---

## 🔹 Run Container with Network

```
docker run -d --network mynetwork nginx
```

---

# 🧹 7. Cleanup Commands (Important ⚠️)

## 🔹 Remove Stopped Containers

```
docker container prune
```

---

## 🔹 Remove Unused Images

```
docker image prune
```

---

## 🔹 Remove All (Danger)

```
docker system prune
```

---

## 🔹 Remove Everything (Including Volumes)

```
docker system prune -a --volumes
```

### Flags

* `-a` → remove all unused images
* `--volumes` → remove volumes

---

# ⚡ 8. Important Combined Commands

## 🔹 Run with Port Mapping

```
docker run -d -p 8080:80 nginx
```

* `-p` → host:container port

---

## 🔹 Run with Environment Variable

```
docker run -e ENV=prod nginx
```

---

## 🔹 Run with Name + Volume + Port

```
docker run -d --name app -p 5000:5000 -v myvol:/data nginx
```

---


# 📌 Summary

* `docker run` → create + start container
* `docker build` → create image
* `docker pull/push` → registry interaction
* `docker exec` → interact inside container
* `docker volume` → persistent storage
* `docker network` → communication
* `docker system prune` → cleanup
