# Project 11: CLI System Monitor (Advanced)

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build an advanced terminal-based system monitoring tool similar to htop/gotop. Learn real-time data visualization, terminal UI programming, and system metrics collection.

**Difficulty:** Intermediate  
**Estimated Time:** 25-35 hours  
**Category:** Systems Programming, CLI Tools

## Prerequisites

- Completed [Project 6: System Monitor](../01-basic/project-06-system-monitor.md)
- Terminal UI basics

**Required Packages:**
```bash
go get github.com/gizak/termui/v3
go get github.com/shirou/gopsutil/v3
```

## What You'll Learn

- Terminal UI with termui
- Real-time charts and graphs
- CPU, memory, disk, network visualization
- Process tree rendering
- Keyboard navigation
- Color schemes and themes
- Performance optimization for updates

## Core Features

### 1. System Overview
- CPU usage per core
- Memory usage (RAM + swap)
- Disk I/O
- Network traffic
- System uptime
- Load averages

### 2. Process Management
- Process list with filtering
- Sort by CPU/memory/PID
- Process tree view
- Kill processes
- Process details

### 3. Visualization
- Line charts for history
- Bar charts for current usage
- Sparklines for trends
- Tables for processes
- Gauges for percentages

### 4. Interactivity
- Keyboard shortcuts
- Mouse support
- Scrolling
- Filtering
- Configuration

## Implementation Guide

### Basic Terminal UI

```go
package main

import (
    ui "github.com/gizak/termui/v3"
    "github.com/gizak/termui/v3/widgets"
    "github.com/shirou/gopsutil/v3/cpu"
    "github.com/shirou/gopsutil/v3/mem"
)

func main() {
    if err := ui.Init(); err != nil {
        log.Fatal(err)
    }
    defer ui.Close()
    
    // CPU gauge
    cpuGauge := widgets.NewGauge()
    cpuGauge.Title = "CPU Usage"
    cpuGauge.SetRect(0, 0, 50, 3)
    cpuGauge.BarColor = ui.ColorGreen
    
    // Memory gauge
    memGauge := widgets.NewGauge()
    memGauge.Title = "Memory Usage"
    memGauge.SetRect(0, 3, 50, 6)
    memGauge.BarColor = ui.ColorYellow
    
    // CPU history chart
    cpuChart := widgets.NewSparkline()
    cpuChart.Data = []float64{0}
    cpuChart.LineColor = ui.ColorCyan
    
    cpuChartGroup := widgets.NewSparklineGroup(cpuChart)
    cpuChartGroup.Title = "CPU History"
    cpuChartGroup.SetRect(0, 6, 50, 12)
    
    // Process table
    processTable := widgets.NewTable()
    processTable.Title = "Processes"
    processTable.SetRect(0, 12, 100, 24)
    processTable.Rows = [][]string{
        {"PID", "Name", "CPU%", "Memory"},
    }
    
    draw := func() {
        ui.Render(cpuGauge, memGauge, cpuChartGroup, processTable)
    }
    
    updateData := func() {
        // Update CPU
        cpuPercent, _ := cpu.Percent(0, false)
        cpuGauge.Percent = int(cpuPercent[0])
        
        // Update memory
        vmem, _ := mem.VirtualMemory()
        memGauge.Percent = int(vmem.UsedPercent)
        
        // Update CPU history
        cpuChart.Data = append(cpuChart.Data[1:], cpuPercent[0])
        if len(cpuChart.Data) > 50 {
            cpuChart.Data = cpuChart.Data[1:]
        }
        
        // Update process list
        processes := getProcessList()
        processTable.Rows = [][]string{{"PID", "Name", "CPU%", "Memory"}}
        for _, p := range processes {
            processTable.Rows = append(processTable.Rows, []string{
                fmt.Sprintf("%d", p.PID),
                p.Name,
                fmt.Sprintf("%.1f", p.CPUPercent),
                fmt.Sprintf("%.1f MB", p.Memory/1024/1024),
            })
        }
    }
    
    ticker := time.NewTicker(time.Second)
    defer ticker.Stop()
    
    uiEvents := ui.PollEvents()
    
    for {
        select {
        case e := <-uiEvents:
            switch e.ID {
            case "q", "<C-c>":
                return
            case "<Resize>":
                payload := e.Payload.(ui.Resize)
                termWidth := payload.Width
                termHeight := payload.Height
                // Adjust widget sizes
            }
        case <-ticker.C:
            updateData()
            draw()
        }
    }
}
```

## Project Structure

```
system-monitor-advanced/
├── main.go
├── ui/
│   ├── dashboard.go
│   ├── widgets.go
│   └── theme.go
├── monitor/
│   ├── cpu.go
│   ├── memory.go
│   ├── disk.go
│   ├── network.go
│   └── processes.go
├── config/
│   └── config.go
└── README.md
```

## Keyboard Shortcuts

```
q, Ctrl+C : Quit
↑/↓       : Scroll process list
k/j       : Vim-style scroll
Tab       : Switch panels
c         : Sort by CPU
m         : Sort by Memory
/         : Filter processes
F9        : Kill selected process
```

## Challenges & Solutions

### Challenge 1: Flickering
**Problem:** Screen flickers on redraw  
**Solution:** Use double buffering, only redraw changed widgets

### Challenge 2: High CPU Usage
**Problem:** UI loop consuming CPU  
**Solution:** Use ticker, sleep between updates

### Challenge 3: Terminal Size
**Problem:** Widget sizing on different terminals  
**Solution:** Dynamic layout, handle resize events

## Next Steps

- Add Docker container monitoring
- Network connections view
- Disk usage tree
- Move to [Project 12: Process Manager](project-12-process-manager.md)

## Resources

- [termui Documentation](https://github.com/gizak/termui)
- [gopsutil Documentation](https://github.com/shirou/gopsutil)

---

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)
