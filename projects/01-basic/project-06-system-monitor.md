# Project 6: System Resource Monitor

[← Back to Basic Projects](README.md) | [↑ Back to Index](../../projects-index.md)

---

## Prerequisites & Requirements

**Before Starting:**
- **Completed**: Process Monitor project (recommended)

**Knowledge Prerequisites:**
- **Must Know**: Basic Go, file I/O, goroutines
- **Will Learn**: System metrics, cross-platform code, `/proc` and `/sys` filesystems

**What to Install:**
```bash
mkdir system-monitor
cd system-monitor
go mod init github.com/yourusername/system-monitor

go get github.com/shirou/gopsutil/v3/cpu
go get github.com/shirou/gopsutil/v3/mem
go get github.com/shirou/gopsutil/v3/disk
go get github.com/shirou/gopsutil/v3/net
go get github.com/shirou/gopsutil/v3/host
```

**Estimated Time:** 15-25 hours

---

## Overview

Build a system resource monitor showing CPU, memory, disk, and network usage. Cross-platform using gopsutil.

### What You'll Learn

- **CPU Metrics**: Usage per core, load average
- **Memory**: RAM usage, swap, available memory
- **Disk I/O**: Read/write rates, IOPS
- **Network**: Bandwidth usage per interface
- **System Info**: Uptime, OS version, hostname
- **Historical Data**: Track metrics over time

### Core Features

1. Real-time CPU usage (overall and per-core)
2. Memory usage (RAM, swap)
3. Disk usage and I/O rates
4. Network traffic per interface
5. Load average (Linux/Unix)
6. System uptime
7. Temperature sensors (if available)
8. Export metrics to Prometheus format

---

## Project Structure

```
system-monitor/
├── main.go
├── monitor/
│   ├── cpu.go
│   ├── memory.go
│   ├── disk.go
│   └── network.go
├── ui/
│   └── dashboard.go
└── export/
    └── prometheus.go
```

---

## Implementation Guide

### Step 1: CPU Monitoring

**What to create:**
```go
type CPUStats struct {
    Overall   float64
    PerCore   []float64
    LoadAvg   [3]float64
}

func GetCPUStats() (*CPUStats, error) {
    // Use gopsutil cpu package
    // Get overall and per-core percentages
    // Get load average (Linux/Unix)
}
```

### Step 2: Memory Monitoring

**What to create:**
```go
type MemoryStats struct {
    Total       uint64
    Used        uint64
    Available   uint64
    UsedPercent float64
    SwapTotal   uint64
    SwapUsed    uint64
}

func GetMemoryStats() (*MemoryStats, error) {
    // Use gopsutil mem package
}
```

### Step 3: Disk Monitoring

**What to create:**
- Disk usage per partition
- I/O rates (read/write bytes per second)
- IOPS (operations per second)

### Step 4: Network Monitoring

**What to create:**
- Network interfaces list
- Bytes sent/received per interface
- Packets sent/received
- Errors and drops

### Step 5: Display Dashboard

Create a simple terminal UI that updates every second showing all metrics.

---

## Challenge Yourself

1. **Web Dashboard**: Build HTTP server with real-time graphs
2. **Historical Data**: Store metrics in time-series database
3. **Alerts**: Notify when thresholds exceeded
4. **Comparison**: Compare with system tools (`top`, `htop`, `iostat`)
5. **Battery Status**: Show battery info for laptops
6. **GPU Usage**: Monitor NVIDIA/AMD GPUs
7. **Process Correlation**: Link CPU/memory to specific processes
8. **Export**: Send metrics to Prometheus, Grafana, or InfluxDB

---

## Common Gotchas

**Problem**: Metrics differ from system tools  
**Fix**: Different calculation methods, both can be correct

**Problem**: High CPU usage from monitoring itself  
**Fix**: Increase sampling interval, optimize queries

**Problem**: Permission errors on some metrics  
**Fix**: Some metrics need elevated privileges

---

## Next Steps

After completing all 6 basic projects, you're ready for:
- **Intermediate Level**: Projects 7-18 (REST APIs, databases, real-time systems)
- Focus on Project 7 (REST API with Database) as foundation for backend development

---

[← Back to Basic Projects](README.md) | [↑ Back to Index](../../projects-index.md)
