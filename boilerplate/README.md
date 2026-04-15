# Multi-Container Runtime (Mini Container Engine)

# Overview

This project implements a lightweight container runtime in C using Linux system calls such as `clone()`, `chroot()`, and namespaces.

The goal is to understand how containers work internally by building a simplified version of a container engine similar to Docker.

---

##  Features Implemented

*  Container creation using `clone()`
*  PID namespace isolation
*  UTS namespace (hostname isolation)
*  Filesystem isolation using `chroot()`
*  Execution of commands inside container
*  Basic container lifecycle tracking (`running`, `exited`)
*  `engine ps` to list containers

---

##  Technologies Used

* C Programming
* Linux System Calls
* Namespaces (PID, UTS, Mount)
* Process Management (`clone`, `execvp`, `waitpid`)
* File handling for container state tracking

---

##  How It Works

### 1. Container Creation

* Uses `clone()` to create a new process
* Applies namespace isolation:

  * `CLONE_NEWPID`
  * `CLONE_NEWUTS`
  * `CLONE_NEWNS`

---

### 2. Filesystem Isolation

* Uses `chroot()` to isolate container filesystem
* Each container has its own root filesystem

---

### 3. Process Execution

* Inside container:

  * `/proc` is mounted
  * Command is executed using `execvp()`

---

### 4. Container Tracking

* Container states are stored in `containers.txt`
* Tracks:

  * running
  * exited

---

## 💻 Commands

### Start a container

```bash
sudo ./engine start alpha ../rootfs-alpha /bin/sh
```

### List containers

```bash
./engine ps
```

---

##  Screenshots

### 🔹 Container Process Isolation

(Add screenshot of `ps` inside container)

### 🔹 Hostname Isolation

(Add screenshot of `hostname`)

### 🔹 Filesystem Isolation

(Add screenshot of `ls /`)

### 🔹 Container List

(Add screenshot of `./engine ps`)

---

##  Key Concepts Learned

* How containers use Linux namespaces
* Difference between processes and containers
* Role of `chroot()` in filesystem isolation
* Low-level process creation using `clone()`

---

##  Limitations

* No full supervisor implementation
* No IPC communication implemented
* Logging system not implemented
* State tracking is basic (file-based)

---

##  Conclusion

This project demonstrates the fundamental concepts behind container runtimes and provides hands-on experience with Linux system programming.

---
