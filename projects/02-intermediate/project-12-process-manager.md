# Project 12: CLI Process Manager

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a process management tool for running and monitoring multiple processes. Learn process lifecycle management, signal handling, and log aggregation.

**Difficulty:** Intermediate  
**Estimated Time:** 20-30 hours  
**Category:** Systems Programming, Process Management

## Prerequisites

- Completed [Project 4: Process Monitor](../01-basic/project-04-process-monitor.md)
- Understanding of Unix processes and signals

**Required Packages:**
```bash
go get github.com/spf13/cobra
```

## What You'll Learn

- Process spawning and management
- Signal handling (SIGTERM, SIGKILL, SIGHUP)
- Process restart strategies
- Log capturing and aggregation
- PID file management
- Daemon processes
- Resource limits
- Health checks

## Core Features

### 1. Process Lifecycle
- Start/stop/restart processes
- Auto-restart on crash
- Graceful shutdown
- Process groups
- Dependency management

### 2. Monitoring
- Health checks (HTTP, TCP, command)
- Resource usage tracking
- Exit code tracking
- Crash detection
- Auto-restart with backoff

### 3. Logging
- Stdout/stderr capture
- Log rotation
- Centralized logging
- Log filtering
- Real-time log tailing

### 4. Configuration
- YAML/JSON config
- Environment variables
- Working directory
- Resource limits
- User/group switching

## Implementation Guide

### Process Manager

```go
package main

import (
    "os/exec"
    "syscall"
    "time"
)

type Process struct {
    ID          string
    Command     string
    Args        []string
    WorkingDir  string
    Env         []string
    
    cmd         *exec.Cmd
    pid         int
    status      string
    restarts    int
    maxRestarts int
    
    stdout      io.Writer
    stderr      io.Writer
}

type ProcessManager struct {
    processes map[string]*Process
    mu        sync.RWMutex
}

func NewProcessManager() *ProcessManager {
    return &ProcessManager{
        processes: make(map[string]*Process),
    }
}

func (pm *ProcessManager) Start(p *Process) error {
    pm.mu.Lock()
    defer pm.mu.Unlock()
    
    if _, exists := pm.processes[p.ID]; exists {
        return fmt.Errorf("process %s already exists", p.ID)
    }
    
    p.cmd = exec.Command(p.Command, p.Args...)
    p.cmd.Dir = p.WorkingDir
    p.cmd.Env = p.Env
    p.cmd.Stdout = p.stdout
    p.cmd.Stderr = p.stderr
    
    if err := p.cmd.Start(); err != nil {
        return err
    }
    
    p.pid = p.cmd.Process.Pid
    p.status = "running"
    pm.processes[p.ID] = p
    
    // Monitor process
    go pm.monitor(p)
    
    return nil
}

func (pm *ProcessManager) Stop(id string) error {
    pm.mu.Lock()
    p, exists := pm.processes[id]
    pm.mu.Unlock()
    
    if !exists {
        return fmt.Errorf("process %s not found", id)
    }
    
    // Send SIGTERM
    if err := p.cmd.Process.Signal(syscall.SIGTERM); err != nil {
        return err
    }
    
    // Wait for graceful shutdown
    done := make(chan error)
    go func() {
        done <- p.cmd.Wait()
    }()
    
    select {
    case <-done:
        p.status = "stopped"
    case <-time.After(10 * time.Second):
        // Force kill
        p.cmd.Process.Kill()
        p.status = "killed"
    }
    
    return nil
}

func (pm *ProcessManager) Restart(id string) error {
    if err := pm.Stop(id); err != nil {
        return err
    }
    
    pm.mu.RLock()
    p := pm.processes[id]
    pm.mu.RUnlock()
    
    return pm.Start(p)
}

func (pm *ProcessManager) monitor(p *Process) {
    err := p.cmd.Wait()
    
    p.status = "exited"
    exitCode := p.cmd.ProcessState.ExitCode()
    
    log.Printf("Process %s exited with code %d", p.ID, exitCode)
    
    // Auto-restart on crash
    if exitCode != 0 && p.restarts < p.maxRestarts {
        p.restarts++
        time.Sleep(time.Duration(p.restarts) * time.Second) // Exponential backoff
        
        log.Printf("Restarting process %s (attempt %d/%d)", p.ID, p.restarts, p.maxRestarts)
        pm.Start(p)
    }
}

func (pm *ProcessManager) List() []*Process {
    pm.mu.RLock()
    defer pm.mu.RUnlock()
    
    list := make([]*Process, 0, len(pm.processes))
    for _, p := range pm.processes {
        list = append(list, p)
    }
    return list
}
```

### Configuration

```yaml
# processes.yaml
processes:
  - id: web-server
    command: ./myapp
    args: ["--port", "8080"]
    working_dir: /app
    env:
      - PORT=8080
      - ENV=production
    auto_restart: true
    max_restarts: 5
    health_check:
      type: http
      url: http://localhost:8080/health
      interval: 10s
      
  - id: worker
    command: ./worker
    args: ["--queue", "default"]
    working_dir: /app
    auto_restart: true
    max_restarts: 10
```

## Project Structure

```
process-manager/
├── main.go
├── cmd/
│   ├── start.go
│   ├── stop.go
│   ├── restart.go
│   ├── list.go
│   └── logs.go
├── manager/
│   ├── process.go
│   ├── supervisor.go
│   └── health.go
├── config/
│   ├── config.go
│   └── processes.yaml
├── logs/
│   └── aggregator.go
└── README.md
```

## CLI Commands

```bash
# Start all processes
procmgr start

# Start specific process
procmgr start web-server

# Stop process
procmgr stop web-server

# Restart process
procmgr restart web-server

# List processes
procmgr list

# View logs
procmgr logs web-server

# Tail logs
procmgr logs -f web-server

# Status
procmgr status
```

## Challenges & Solutions

### Challenge 1: Zombie Processes
**Problem:** Child processes not cleaned up  
**Solution:** Proper Wait() calls, signal handling

### Challenge 2: Graceful Shutdown
**Problem:** Processes don't stop cleanly  
**Solution:** SIGTERM first, SIGKILL after timeout

### Challenge 3: Log File Rotation
**Problem:** Logs grow indefinitely  
**Solution:** Size-based or time-based rotation

## Next Steps

- Add Docker support
- Web UI for management
- Metrics and alerting
- Move to [Project 13: Advanced Log Analyzer](project-13-log-analyzer.md)

## Resources

- [Unix Process Management](https://www.man7.org/linux/man-pages/man2/fork.2.html)
- [Systemd for inspiration](https://systemd.io/)

---

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)
