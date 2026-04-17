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

<img width="776" height="259" alt="WhatsApp Image 2026-04-15 at 11 50 54 PM" src="https://github.com/user-attachments/assets/3277338b-a3dc-4125-af14-f8045dba22a1" />


### 🔹 Hostname Isolation

<img width="881" height="244" alt="image" src="https://github.com/user-attachments/assets/f0a706b3-9ce9-4b27-86c9-2bda28bf54d7" />


### 🔹 Filesystem Isolation

<img width="822" height="120" alt="image" src="https://github.com/user-attachments/assets/f8b35fd2-5626-42e2-a324-4cbc849810ce" />


### 🔹 Container List

<img width="909" height="73" alt="image" src="https://github.com/user-attachments/assets/174c1626-a383-4221-94cb-e83d8cad97c3" />
 ###    remove container 
 <img width="882" height="179" alt="image" src="https://github.com/user-attachments/assets/88d54991-45a5-4de5-b03c-7589a66614e3" />


---

##  Key Concepts Learned

* How containers use Linux namespaces
* Difference between processes and containers
* Role of `chroot()` in filesystem isolation
* Low-level process creation using `clone()`


---

##  Conclusion

This project demonstrates the fundamental concepts behind container runtimes and provides hands-on experience with Linux system programming.

---
