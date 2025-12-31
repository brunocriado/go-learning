# Basic Level Projects (1-6)

Welcome to the Basic Level projects! These 6 projects will teach you Go fundamentals and prepare you for more advanced work.

---

## Projects in This Level

### [Project 1: CLI Todo Application](project-01-cli-todo.md)
**Time**: 8-12 hours | **Prerequisites**: None (Start here!)

Build a command-line todo app with file persistence. Learn Go basics, file I/O, JSON encoding/decoding, and CLI flag parsing.

**Key Skills**: Variables, functions, structs, file operations, JSON, error handling

---

### [Project 2: URL Shortener Service](project-02-url-shortener.md)
**Time**: 12-18 hours | **Prerequisites**: Project 1

Create a URL shortening service with HTTP server and web interface. Learn HTTP servers, routing, maps, and persistent storage.

**Key Skills**: HTTP server, routing, hash maps, JSON persistence, middleware basics

---

### [Project 3: File Organizer Tool](project-03-file-organizer.md)
**Time**: 15-20 hours | **Prerequisites**: Projects 1-2

Build a tool that automatically organizes files by type, date, or custom rules. Learn filesystem operations, goroutines, and file watching.

**Key Skills**: File system traversal, goroutines, channels, fsnotify, concurrent patterns

---

### [Project 4: System Process Monitor](project-04-process-monitor.md)
**Time**: 12-18 hours | **Prerequisites**: Projects 1-3

Create a process monitoring tool that displays CPU, memory usage, and process information. Learn `/proc` filesystem and system calls.

**Key Skills**: Process information, `/proc` filesystem, real-time monitoring, system APIs

---

### [Project 5: Log File Analyzer & Tail](project-05-log-analyzer.md)
**Time**: 10-15 hours | **Prerequisites**: Project 1

Build a log analyzer that parses, filters, and tails log files. Implement `tail -f` functionality and log pattern matching.

**Key Skills**: File I/O, regex patterns, file seeking, line-by-line reading, statistics

---

### [Project 6: System Resource Monitor](project-06-system-monitor.md)
**Time**: 15-20 hours | **Prerequisites**: Project 4

Create a comprehensive system monitor displaying CPU, memory, disk, and network metrics. Learn cross-platform system monitoring.

**Key Skills**: System metrics, gopsutil library, cross-platform code, resource monitoring

---

## Learning Objectives

After completing all Basic projects, you will:

✅ Understand Go syntax, types, and control structures  
✅ Work confidently with files, JSON, and XML  
✅ Build HTTP servers and make HTTP requests  
✅ Use goroutines and channels for basic concurrency  
✅ Parse command-line arguments and environment variables  
✅ Handle errors properly and write clean Go code  
✅ Test your code and use the Go toolchain

---

## Progression Path

```
Project 1 (CLI Todo)
    ↓
    ├→ Project 2 (URL Shortener)
    ├→ Project 5 (Log Analyzer)
    └→ Project 3 (File Organizer)
         ↓
         └→ Project 4 (Process Monitor)
              ↓
              └→ Project 6 (System Monitor)
                   ↓
              BASIC COMPLETE ✓
              Ready for Intermediate!
```

---

## Time Estimate

- **Minimum**: 6 weeks (1 project per week)
- **Recommended**: 8-12 weeks (with practice and refinement)
- **Total Hours**: 75-105 hours

---

## Tips for Success

1. **Complete in order** - Each project builds on previous concepts
2. **Write tests** - Start building good testing habits early
3. **Handle errors** - Don't use `panic()` except in truly exceptional cases
4. **Ask for help** - Join the [Go community](../../resources.md#community--support)
5. **Refactor** - Come back and improve your code as you learn more

---

## Next Steps

- Start with **[Project 1: CLI Todo](project-01-cli-todo.md)**
- Review **[Getting Started](../../getting-started.md)** if you need setup help
- Check **[Projects Index](../../projects-index.md)** for the full roadmap

---

**Ready to begin?** Open Project 1 and start building! 🚀
