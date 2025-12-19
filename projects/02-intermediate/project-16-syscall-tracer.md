# Project 16: System Call Tracer

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a system call tracer using ptrace. Learn process introspection, system call interception, and low-level debugging.

**Difficulty:** Intermediate-Advanced  
**Estimated Time:** 30-50 hours  
**Platform:** Linux only

## What You'll Learn

- ptrace API
- System call table
- Process memory reading
- Register manipulation
- Signal handling
- eBPF for tracing

## Implementation Guide

```go
package main

import (
    "fmt"
    "syscall"
)

func traceProcess(pid int) error {
    err := syscall.PtraceAttach(pid)
    if err != nil {
        return err
    }
    
    var wstatus syscall.WaitStatus
    syscall.Wait4(pid, &wstatus, 0, nil)
    
    for {
        // Continue until next syscall
        err = syscall.PtraceSyscall(pid, 0)
        if err != nil {
            return err
        }
        
        _, err = syscall.Wait4(pid, &wstatus, 0, nil)
        if err != nil {
            return err
        }
        
        if wstatus.Exited() {
            break
        }
        
        // Get registers
        var regs syscall.PtraceRegs
        err = syscall.PtraceGetRegs(pid, &regs)
        if err != nil {
            return err
        }
        
        // Print syscall info
        fmt.Printf("Syscall: %d\n", regs.Orig_rax)
    }
    
    return nil
}
```

## Project Structure

```
syscall-tracer/
├── main.go
├── tracer/
│   ├── ptrace.go
│   ├── syscalls.go
│   └── decoder.go
└── README.md
```

## Next Steps

- Add argument decoding
- Implement filtering
- Create strace-like tool
- Move to [Project 17: NoSQL API](project-17-nosql-api.md)

---

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)
