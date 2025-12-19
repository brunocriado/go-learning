# Advanced Level Projects (19-21)

Welcome to Advanced Level! These 3 challenging projects will teach you systems programming, kernel interaction, and virtualization.

---

## What You'll Build

In this level, you'll work with operating system internals, kernel APIs, and virtualization technologies. These are the projects that set systems programmers apart.

---

## Projects in This Level

### [Project 19: FUSE Filesystem](project-19-fuse-filesystem.md)
**Time**: 40-60 hours | **Prerequisites**: Projects 3, 9, 14

Build a custom filesystem using FUSE (Filesystem in Userspace). Create encrypted filesystems, cloud-backed storage, or virtual file browsers.

**Key Skills**: Filesystem APIs, FUSE, Virtual FS, System calls, File operations

**What You'll Learn:**
- How filesystems work at the system call level
- Implementing file operations (open, read, write, close)
- Directory operations and metadata
- FUSE protocol and userspace implementation
- Performance considerations for filesystems

---

### [Project 20: eBPF Monitoring Tool](project-20-ebpf-monitor.md)
**Time**: 50-80 hours | **Prerequisites**: Projects 11-16

Create a kernel-level monitoring tool using eBPF (extended Berkeley Packet Filter). Trace system calls, network packets, and performance metrics without modifying the kernel.

**Key Skills**: eBPF, Kernel tracing, Performance analysis, BPF bytecode, Observability

**What You'll Learn:**
- eBPF fundamentals and use cases
- Writing eBPF programs in C
- Loading and attaching eBPF programs
- Reading eBPF maps from userspace
- Tracing system calls and kernel functions
- Performance monitoring without overhead

---

### [Project 21: Hypervisor (KVM-based)](project-21-hypervisor.md)
**Time**: 80-120 hours | **Prerequisites**: Projects 19-20

Build a basic hypervisor using KVM (Kernel-based Virtual Machine). Create and manage virtual machines, handle memory and CPU virtualization.

**Key Skills**: Virtualization, KVM API, Memory management, CPU virtualization, Device emulation

**What You'll Learn:**
- How virtual machines work
- KVM API and ioctl interface
- Memory virtualization (EPT/NPT)
- CPU virtualization (VT-x/AMD-V)
- Device emulation basics
- Virtual machine lifecycle management

---

## Learning Objectives

After completing Advanced projects, you will:

✅ Understand filesystem internals  
✅ Work with kernel-level tracing  
✅ Build monitoring tools with eBPF  
✅ Create virtual machines  
✅ Master systems programming  
✅ Contribute to infrastructure projects  
✅ Debug complex system issues  
✅ Optimize at the kernel level

---

## Progression Path

```
Projects 1-18 (Basic & Intermediate)
    ↓
Project 19 (FUSE Filesystem)
    ↓
Project 20 (eBPF Monitor)
    ↓
Project 21 (Hypervisor)
    ↓
ADVANCED COMPLETE ✓
Ready for Expert & Specialized!
```

---

## Prerequisites

**Strongly Recommended:**
- Complete all Basic projects (1-6)
- Complete most Intermediate projects (7-18)
- Comfortable with C programming
- Linux/Unix systems knowledge
- Kernel concepts understanding

**System Requirements:**
- **OS**: Linux (Ubuntu 20.04+ or similar) - Required for eBPF and KVM
- **macOS**: Limited support (FUSE works, eBPF/KVM require Linux VM)
- **Windows**: Use WSL2 or Linux VM
- **CPU**: x86_64 with virtualization support (VT-x/AMD-V) for Project 21
- **RAM**: 8GB minimum (16GB recommended)
- **Permissions**: Some projects require root/sudo

---

## Time Estimate

- **Minimum**: 12-24 weeks total
- **Recommended**: Take your time, these are challenging
- **Total Hours**: 170-260 hours

**Project 19**: 4-8 weeks  
**Project 20**: 6-10 weeks  
**Project 21**: 10-15 weeks

---

## Platform Notes

### Linux (Recommended)
- Full support for all projects
- eBPF requires kernel 4.4+ (5.8+ recommended)
- KVM requires CPU virtualization support

### macOS
- FUSE works with macFUSE
- eBPF not supported (requires Linux VM)
- KVM not supported (requires Linux VM)

### Windows
- Use WSL2 (Windows Subsystem for Linux)
- Or run Linux in VirtualBox/VMware
- Native Windows not supported

---

## Required Tools & Libraries

```bash
# FUSE development (Project 19)
# Ubuntu/Debian
sudo apt install libfuse-dev

# Fedora/RHEL
sudo dnf install fuse-devel

# macOS
brew install macfuse

# eBPF development (Project 20)
sudo apt install libbpf-dev clang llvm
sudo apt install linux-headers-$(uname -r)

# KVM development (Project 21)
sudo apt install qemu-kvm libvirt-dev
# Check KVM support
kvm-ok
```

---

## Tips for Success

1. **Start with Project 19** - Most accessible advanced project
2. **Use Linux** - Better support for systems programming
3. **Read documentation** - FUSE, eBPF, KVM have good docs
4. **Study examples** - Look at existing FUSE/eBPF/KVM code
5. **Debug carefully** - Kernel-level bugs can crash systems
6. **VM for testing** - Test dangerous code in VMs
7. **Join communities** - eBPF and KVM have active communities
8. **Be patient** - These projects are legitimately difficult

---

## Safety Warnings

⚠️ **These projects interact with the kernel:**
- Bugs can crash your system
- Test in virtual machines when possible
- Backup important data
- Don't run on production systems
- Be careful with sudo/root access

⚠️ **Project 21 (Hypervisor):**
- Requires CPU virtualization (VT-x/AMD-V)
- Can conflict with other hypervisors
- Resource-intensive
- Only one hypervisor at a time

---

## Career Impact

Completing these projects demonstrates:

✅ Systems programming expertise  
✅ Kernel knowledge  
✅ Infrastructure understanding  
✅ Complex problem-solving  
✅ Performance optimization skills

**Career Opportunities:**
- Infrastructure Engineer
- Systems Programmer
- Kernel Developer
- Performance Engineer
- Cloud Infrastructure
- Container Runtime Development

---

## After Advanced

You'll be ready for:
- **Expert Level** (Projects 22-25) - Distributed systems patterns
- **Specialized** (Projects 26-35) - Production cloud-native
- **Open Source** - Contribute to Docker, Kubernetes, containerd, etc.
- **Senior Positions** - Staff/Principal engineer roles

---

## Next Steps

- Review **[Prerequisites Flowchart](../../getting-started.md#prerequisites-flowchart)**
- Set up Linux environment (VM if needed)
- Start with **[Project 19: FUSE Filesystem](project-19-fuse-filesystem.md)**
- Join [eBPF community](https://ebpf.io/) and [KVM mailing lists](https://www.linux-kvm.org/)

---

**Ready for the challenge?** These projects will push your limits and make you a true systems programmer. Let's build! 🚀
