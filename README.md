#  OS-Jackfruit: Lightweight Container Runtime in C

##  Overview

OS-Jackfruit is a lightweight container runtime implemented in C using Linux system calls.
It demonstrates how containers work internally by providing process isolation, filesystem isolation, and basic container lifecycle management.

---

## 🚀 Features Implemented

* Container creation using `clone()`
* PID namespace isolation (process isolation)
* UTS namespace (hostname isolation)
* Filesystem isolation using `chroot()`
* Mounting `/proc` for process visibility
* Execution of commands inside container
* Basic container lifecycle tracking (`running`, `exited`)
* Custom command `engine ps` to list container status

---

## Concepts Used

* Linux Namespaces (`CLONE_NEWPID`, `CLONE_NEWUTS`, `CLONE_NEWNS`)
* `clone()` system call
* `chroot()` for filesystem isolation
* `mount()` for `/proc`
* Process management
* File handling for container tracking

---

##  Project Structure

```
boilerplate/
│── engine.c          # Main container engine
│── monitor.c         # Kernel module (optional)
│── cpu_hog.c         # CPU stress test
│── memory_hog.c      # Memory stress test
│── Makefile
│── rootfs-alpha/     # Container filesystem (created at runtime)
│── containers.txt    # Stores container states
```

---

##  Setup Instructions

### 1. Navigate to project

```bash
cd OS-Jackfruit/boilerplate
```

---

### 2. Clean previous setup

```bash
sudo umount -l rootfs-alpha/proc 2>/dev/null
sudo rm -rf rootfs-alpha
```

---

### 3. Create root filesystem

```bash
mkdir rootfs-alpha

sudo cp -r /bin rootfs-alpha/
sudo cp -r /lib rootfs-alpha/
sudo cp -r /lib64 rootfs-alpha/
sudo cp -r /usr rootfs-alpha/

mkdir rootfs-alpha/proc
mkdir -p rootfs-alpha/etc
echo "root:x:0:0:root:/root:/bin/sh" > rootfs-alpha/etc/passwd
```

---

### 4. Compile the project

```bash
make
```

---

##  Running the Container

```bash
sudo ./engine start alpha ./rootfs-alpha /bin/sh
```

---

##  Inside Container (Test Commands)

```bash
ps
hostname
ls /
ls /proc
whoami
```

---

##  Exit Container

```bash
exit
```

---

##  Check Container Status

```bash
./engine ps
```

---

##  Known Issues

* TTY warning may appear:

  ```
  Cannot set tty process group
  ```

  This is expected due to minimal terminal handling.

* Duplicate container entries may appear in `containers.txt`
  (can be cleared manually).

---

##  Sample Output

```
Starting container: alpha
Inside container!

# ps
PID   CMD
1     sh
2     ps

# hostname
alpha
```

---

##  Learning Outcomes

* Understanding how containers work internally
* Hands-on experience with Linux namespaces
* Working with low-level system calls in C
* Building a mini Docker-like runtime

---

##  Viva Summary

This project implements a lightweight container runtime using `clone()` and Linux namespaces. It provides isolation of processes, hostname, and filesystem, and demonstrates how containers function at a low level.

---

## Future Improvements

* Add network namespace support
* Implement resource limits (CPU, memory)
* Improve container lifecycle management
* Add logging and monitoring features

---

## Author

* Preksha

---
