# Container Runtime, Namespaces, and Control Groups (cgroups)

These concepts are fundamental components of **containerization in Linux-based systems** such as Docker. Containers rely on the Linux kernel for process isolation and resource management.

The three major technologies that make containers possible are:

* Container Runtime
* Namespaces
* Control Groups (cgroups)

---

# 1. Container Runtime

## 1.1 Definition

A **Container Runtime** is the software responsible for running containers on a host system.

It performs several tasks including:

* Creating containers
* Starting and stopping containers
* Managing container lifecycle
* Setting up namespaces and cgroups
* Handling container images
* Isolating container processes

In simple terms:

**Container Runtime = Engine that runs containers**

---

## Example Flow

```
User Command (docker run)
        ↓
Container Runtime
        ↓
Create Container Process
        ↓
Linux Kernel Features (namespaces + cgroups)
```

---

## 1.2 Responsibilities of Container Runtime

A container runtime performs the following operations.

### 1. Container Creation

Creates a container instance from a container image.

### 2. Process Isolation

Uses **Linux namespaces** to isolate processes.

### 3. Resource Control

Uses **cgroups** to limit resources such as CPU and memory.

### 4. Filesystem Setup

Creates layered container filesystems.

### 5. Networking

Configures network interfaces for containers.

### 6. Lifecycle Management

Manages container lifecycle operations:

* Start
* Stop
* Pause
* Delete containers

---

## 1.3 Container Runtime Architecture

Typical container runtime architecture:

```
User
 │
Docker CLI
 │
Docker Daemon (dockerd)
 │
containerd
 │
runc
 │
Linux Kernel
```

### Component Explanation

| Component     | Role                                    |
| ------------- | --------------------------------------- |
| Docker CLI    | User command interface                  |
| Docker Daemon | Manages containers                      |
| containerd    | Container lifecycle manager             |
| runc          | Low level container runtime             |
| Linux Kernel  | Provides isolation and resource control |

---

## 1.4 Types of Container Runtime

Container runtimes are classified into two types.

### 1. Low-Level Container Runtime

These runtimes interact directly with the **Linux kernel**.

Responsibilities:

* Create containers
* Configure namespaces
* Configure cgroups
* Start container processes

Examples:

| Runtime      | Description                          |
| ------------ | ------------------------------------ |
| runc         | Most common container runtime        |
| crun         | Faster alternative to runc           |
| runv         | Lightweight VM runtime               |
| kata-runtime | Secure runtime using lightweight VMs |

Example flow:

```
containerd → runc → Linux Kernel
```

---

### 2. High-Level Container Runtime

High-level runtimes provide additional features such as:

* Image management
* Networking
* Storage management
* Integration with orchestration systems

Examples:

| Runtime       | Used In         |
| ------------- | --------------- |
| containerd    | Docker          |
| CRI-O         | Kubernetes      |
| Docker Engine | Docker platform |

---

## 1.5 Popular Container Runtimes

### runc

* Default runtime for Docker
* Implements OCI runtime specification
* Responsible for running containers

### containerd

* Container runtime used by Docker
* Manages container lifecycle

### CRI-O

* Lightweight runtime designed for Kubernetes

### Kata Containers

* Provides stronger isolation using lightweight virtual machines

---

# 2. Namespaces

## 2.1 Definition

**Namespaces** are a Linux kernel feature that provides **process isolation**.

They allow containers to have their own view of system resources.

Each container believes it has:

* Its own processes
* Its own network
* Its own filesystem

Example:

```
Container A → sees its own processes
Container B → sees its own processes
Host → sees all processes
```

---

## 2.2 Purpose of Namespaces

Namespaces isolate several system resources including:

* Process IDs
* Network interfaces
* Mount points
* Hostname
* Users
* IPC resources

Thus containers behave like **independent systems**.

---

## 2.3 Types of Namespaces

Linux provides several namespaces.

---

### 1. PID Namespace

PID = **Process ID**

Each container has its own process numbering.

Example:

```
Host PID: 1000

Container PID:
1
2
3
```

Inside container:

**PID 1 = main container process**

Benefit:

* Process isolation

---

### 2. Network Namespace

Each container gets its own network stack including:

* IP address
* Routing table
* Network interfaces
* Firewall rules
* Ports

Example:

```
Container A IP: 172.17.0.2
Container B IP: 172.17.0.3
```

Benefits:

* Independent networking

---

### 3. Mount Namespace

Controls filesystem visibility.

Each container sees its own filesystem hierarchy.

Example:

```
Host filesystem
       │
Container filesystem
```

Containers cannot access host files unless mounted.

---

### 4. IPC Namespace

IPC = **Inter Process Communication**

Controls access to:

* Shared memory
* Message queues
* Semaphores

Containers cannot share IPC resources with other containers.

---

### 5. UTS Namespace

UTS = **Unix Time Sharing**

Allows containers to have separate:

* Hostname
* Domain name

Example:

```
Container A hostname → app-server
Container B hostname → db-server
```

---

### 6. User Namespace

Provides user ID isolation.

Example:

```
Inside container: root = UID 0
Host system: mapped to non-root user
```

Benefit:

Improves security.

---

## Summary of Namespaces

| Namespace | Resource Isolated          |
| --------- | -------------------------- |
| PID       | Processes                  |
| Network   | Networking stack           |
| Mount     | Filesystem                 |
| IPC       | Interprocess communication |
| UTS       | Hostname                   |
| User      | User IDs                   |

---

# 3. Control Groups (cgroups)

## 3.1 Definition

**Control Groups (cgroups)** are a Linux kernel feature used to **limit, monitor, and isolate resource usage** of processes.

Since containers share the same OS kernel, **cgroups ensure fair resource allocation**.

Example:

```
Container A → 2 CPU cores
Container B → 1 CPU core
```

---

## 3.2 Purpose of cgroups

They control system resources including:

* CPU usage
* Memory usage
* Disk I/O
* Network bandwidth
* Number of processes

Without cgroups:

One container could consume all system resources.

With cgroups:

Resources are controlled and limited.

---

## 3.3 Functions of cgroups

### 1. Resource Limiting

Limits resource usage.

Example:

```
Memory limit = 512MB
CPU limit = 2 cores
```

---

### 2. Resource Accounting

Tracks resource usage such as:

* CPU usage
* Memory usage
* Disk I/O usage

---

### 3. Resource Isolation

Ensures one container cannot impact another container.

---

### 4. Resource Prioritization

Some containers may get higher priority.

Example:

Database container > Logging container

---

## 3.4 cgroups Controllers

Each controller manages a specific resource.

| Controller | Resource Managed  |
| ---------- | ----------------- |
| cpu        | CPU usage         |
| cpuacct    | CPU accounting    |
| memory     | RAM usage         |
| blkio      | Disk I/O          |
| devices    | Device access     |
| net_cls    | Network traffic   |
| pids       | Process count     |
| freezer    | Suspend processes |

---

## 3.5 Example of cgroups in Docker

Example Docker command:

```
docker run -m 512m --cpus=1 nginx
```

Meaning:

* Memory limit = **512MB**
* CPU limit = **1 core**

Docker internally uses **cgroups** to enforce these limits.

---

## 3.6 cgroups Versions

There are two versions of cgroups.

### cgroups v1

* Older implementation
* Each controller has its own hierarchy

Example:

* cpu subsystem
* memory subsystem
* blkio subsystem

---

### cgroups v2

Modern implementation with:

* Unified hierarchy
* Better resource management
* Improved performance

---

## 3.7 How Containers Use cgroups

```
Docker / Container Runtime
        ↓
Create cgroup
        ↓
Assign resource limits
        ↓
Attach container process
        ↓
Linux Kernel enforces limits
```

---

# 4. Namespaces vs cgroups

| Feature         | Namespaces            | cgroups             |
| --------------- | --------------------- | ------------------- |
| Purpose         | Isolation             | Resource control    |
| What it manages | System resources      | Resource usage      |
| Example         | Separate process list | CPU limit           |
| Used for        | Container environment | Resource management |
