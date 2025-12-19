# Project 19: Container Runtime (Linux Namespaces & cgroups)

[← Back to Advanced Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a Docker-like container runtime from scratch using Linux namespaces, cgroups, and overlayfs. This is one of the most challenging projects - you'll understand exactly how Docker, containerd, and Kubernetes work under the hood.

**Difficulty:** Advanced  
**Estimated Time:** 100-150 hours  
**Platform:** Linux only  
**Prerequisites:** Solid Linux knowledge, root access, understanding of OS concepts

## What You'll Learn

- Linux namespaces (PID, mount, network, UTS, IPC, user)
- cgroups for resource limiting
- overlayfs for layered filesystems
- Container images and layers
- Network virtumentation (veth pairs, bridges)
- Root filesystem setup (chroot)
- Process isolation

## Core Features

1. **Namespace Isolation:**
   - PID namespace (process isolation)
   - Mount namespace (filesystem isolation)
   - Network namespace (network stack isolation)
   - UTS namespace (hostname isolation)
   - IPC namespace (inter-process communication)
   - User namespace (UID/GID mapping)

2. **Resource Limiting (cgroups):**
   - CPU limits
   - Memory limits
   - Disk I/O limits
   - Network bandwidth

3. **Filesystem:**
   - overlayfs layers
   - Read-only base layer
   - Writable container layer
   - Volume mounts

4. **Networking:**
   - veth pair creation
   - Bridge networking
   - NAT/iptables rules
   - Port mapping

## Quick Start

```go
// Create container
container := NewContainer("alpine:latest")
container.SetCPULimit("1.0")
container.SetMemoryLimit("512M")
container.SetCommand("/bin/sh")

// Run
if err := container.Start(); err != nil {
    log.Fatal(err)
}
```

## Implementation Overview

### 1. Namespace Creation

```go
cmd := exec.Command("/proc/self/exe", "child")
cmd.SysProcAttr = &syscall.SysProcAttr{
    Cloneflags: syscall.CLONE_NEWPID |
                syscall.CLONE_NEWNS |
                syscall.CLONE_NEWNET |
                syscall.CLONE_NEWUTS,
}
```

### 2. cgroups Setup

```go
// Create cgroup
cgroupPath := "/sys/fs/cgroup/memory/mycontainer"
os.Mkdir(cgroupPath, 0755)

// Set memory limit
ioutil.WriteFile(cgroupPath+"/memory.limit_in_bytes", []byte("536870912"), 0644)

// Add process to cgroup
ioutil.WriteFile(cgroupPath+"/cgroup.procs", []byte(fmt.Sprintf("%d", pid)), 0644)
```

### 3. overlayfs Mount

```go
// Mount overlayfs
syscall.Mount("overlay", rootfs, "overlay", 0, 
    "lowerdir=/lower,upperdir=/upper,workdir=/work")
```

## Project Structure

```
container-runtime/
├── main.go
├── container/
│   ├── container.go      # Container struct
│   ├── namespace.go      # Namespace setup
│   ├── cgroup.go         # cgroups configuration
│   └── rootfs.go         # Filesystem setup
├── network/
│   ├── bridge.go         # Bridge creation
│   ├── veth.go           # veth pairs
│   └── iptables.go       # NAT rules
├── image/
│   ├── pull.go           # Image pulling
│   ├── layer.go          # Layer management
│   └── overlay.go        # overlayfs
└── README.md
```

## Security Warnings

⚠️ **DANGEROUS**: This project requires root access and can break your system if done incorrectly.

**Recommendations:**
- Use a VM or container for development
- Never run on production systems
- Understand each syscall before using
- Test thoroughly in isolated environment

## Full Implementation

For complete implementation details with 800+ lines of code examples:
1. Open `golang-learning-projects.md`
2. Search for "## Project 19:" or around line 6500-7500
3. Follow the comprehensive step-by-step guide

## Resources

- [Linux Namespaces](https://man7.org/linux/man-pages/man7/namespaces.7.html)
- [cgroups Documentation](https://www.kernel.org/doc/Documentation/cgroup-v2.txt)
- [overlayfs](https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt)
- [Docker Source Code](https://github.com/moby/moby)

---

[← Back to Advanced Projects](README.md) | [↑ Back to Index](../../projects-index.md)
