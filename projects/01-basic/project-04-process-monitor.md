# Project 4: System Process Monitor

[← Back to Basic Projects](README.md) | [↑ Back to Index](../../projects-index.md)

---

## Prerequisites & Requirements

**Before Starting:**
- **Completed**: All 3 basic projects OR equivalent experience
- Understanding of processes (PID, CPU, memory)
- Operating system basics
- Command-line interfaces

**Knowledge Prerequisites:**
- **Must Know**:
  - Basic Go syntax
  - File reading (`os.ReadFile`, `bufio.Scanner`)
  - String parsing (`strings.Split`, `strconv`)
  - Goroutines basics
  - Time and duration
- **Will Learn**:
  - `/proc` filesystem (Linux)
  - `ps` command internals
  - Process information gathering
  - Cross-platform process APIs
  - Real-time monitoring
  - Terminal UI basics

**External Dependencies:**
- **Required**:
  - `github.com/shirou/gopsutil/v3` - Cross-platform system info
- **Optional**:
  - `github.com/gizak/termui/v3` - Terminal UI

**What to Install:**
```bash
mkdir process-monitor
cd process-monitor
go mod init github.com/yourusername/process-monitor

go get github.com/shirou/gopsutil/v3/process
go get github.com/shirou/gopsutil/v3/cpu
go get github.com/shirou/gopsutil/v3/mem

# Optional: Terminal UI
go get github.com/gizak/termui/v3
```

**Estimated Time:** 15-20 hours

---

## Overview

Build a cross-platform system process monitor (like `top` or Task Manager) that displays running processes with CPU, memory usage, and allows sorting/filtering.

### What You'll Learn

- **Process Information**: Read process details from OS
- **/proc Filesystem**: Linux process info (on Linux)
- **Cross-platform APIs**: gopsutil for portability
- **Real-time Updates**: Live monitoring with goroutines
- **Resource Usage**: CPU, memory, threads
- **Terminal UI**: Interactive console applications
- **Sorting/Filtering**: Data manipulation

### Core Features

1. List all running processes
2. Show PID, name, CPU%, memory%, status
3. Sort by CPU, memory, PID, name
4. Filter by name or user
5. Real-time updates (refresh every second)
6. Kill process by PID
7. Search functionality
8. Cross-platform support

---

## Project Structure

```
process-monitor/
├── main.go
├── monitor/
│   ├── process.go      # Process information
│   ├── system.go       # System stats
│   └── filter.go       # Filtering logic
├── ui/
│   ├── display.go      # Display formatting
│   └── input.go        # User input handling
└── utils/
    └── format.go       # Formatting helpers
```

---

## Implementation Guide

### Step 1: List Processes

**What to create:**
```go
// monitor/process.go
type ProcessInfo struct {
    PID        int32
    Name       string
    CPUPercent float64
    MemPercent float32
    Status     string
    CreateTime int64
}

func GetAllProcesses() ([]ProcessInfo, error) {
    // Use gopsutil to get process list
    // Iterate and collect info
}
```

**Hints:**
- `process.Processes()` returns all processes
- Use `p.Name()`, `p.CPUPercent()`, `p.MemoryPercent()`
- Handle errors gracefully (some processes may not be accessible)

### Step 2: Display Process Table

Create table formatter with:
- Header row
- Data rows with alignment
- Color coding (optional)

**Hints:**
- Use `fmt.Sprintf()` for formatting
- Right-align numbers, left-align text
- `\r` to overwrite current line for live updates

### Step 3: Sorting and Filtering

**What to create:**
- Sort by different fields
- Filter by name, user, or threshold
- Command-line flags for options

**Hints:**
- Use `sort.Slice()` with custom comparison
- `strings.Contains()` for name filtering
- Parse flags with `flag` package

### Step 4: Real-time Monitoring

**What to create:**
- Refresh display every second
- Clear screen and redraw
- Handle Ctrl+C gracefully

**Hints:**
- `time.Ticker` for periodic updates
- `os/signal` to catch interrupts
- `\033[2J\033[H` to clear terminal (ANSI codes)

---

## Challenge Yourself

1. **Process Tree**: Show parent-child relationships
2. **CPU Graph**: Historical CPU usage chart
3. **Disk I/O**: Show read/write rates per process
4. **Network**: Show network usage per process
5. **Process Details**: Detailed view for selected process
6. **Export**: Save snapshot to CSV/JSON
7. **Alerts**: Notify when process exceeds threshold
8. **Interactive UI**: Use termui for rich interface
9. **Remote Monitoring**: Monitor processes on remote machines
10. **Platform-Specific**: Use native APIs on each OS

---

## Common Gotchas

**Problem**: Permission denied accessing some processes  
**Fix**: Normal behavior, skip inaccessible processes or run with elevated privileges

**Problem**: CPU percentage over 100%  
**Fix**: Multi-core systems can show >100% (per-core usage), divide by CPU count

**Problem**: Slow updates  
**Fix**: Cache process info, only update changed processes

---

[← Back to Basic Projects](README.md) | [↑ Back to Index](../../projects-index.md)
