# Intermediate Level Projects (7-18)

Welcome to Intermediate Level! These 12 projects will transform you from a Go beginner into a capable backend developer.

---

## What You'll Build

In this level, you'll create production-ready backends, real-time systems, and network services. You'll work with databases, WebSockets, TCP/IP, and operating system APIs.

---

## Projects in This Level

### Backend & Web Services (7-10)

**[Project 7: REST API with Database](project-07-rest-api.md)**  
**Time**: 20-30 hours | **Prerequisites**: Projects 4-5

Build a full-featured REST API with PostgreSQL, JWT authentication, middleware, and comprehensive testing. Your first production-ready backend.

**Key Skills**: SQL, JWT, Middleware, Testing, Database design, API design

---

**[Project 8: WebSocket Chat Server](project-08-websocket-chat.md)**  
**Time**: 20-30 hours | **Prerequisites**: Project 7

Create a real-time chat application with WebSockets, rooms, user presence, and message history. Learn pub/sub patterns.

**Key Skills**: WebSockets, Pub/Sub, Real-time communication, Connection management

---

**[Project 9: File Sync Tool](project-09-file-sync.md)**  
**Time**: 25-35 hours | **Prerequisites**: Project 7

Build a file synchronization tool using TCP sockets, implementing a custom protocol with checksums and delta transfers.

**Key Skills**: TCP, Binary protocols, Checksums, Network programming

---

**[Project 10: Web Scraper & Crawler](project-10-web-scraper.md)**  
**Time**: 25-35 hours | **Prerequisites**: Projects 7-8

Develop a concurrent web scraper with politeness rules, HTML parsing, and data extraction. Handle rate limiting and robots.txt.

**Key Skills**: Concurrency, HTML parsing, HTTP clients, Rate limiting

---

### Systems Programming (11-13)

**[Project 11: Process Monitor](project-11-process-monitor.md)**  
**Time**: 15-20 hours | **Prerequisites**: Projects 1-5

Monitor system processes, CPU/memory usage, and display real-time statistics. Cross-platform system information gathering.

**Key Skills**: OS APIs, /proc filesystem, System metrics, Real-time updates

---

**[Project 12: Log Analyzer](project-12-log-analyzer.md)**  
**Time**: 15-20 hours | **Prerequisites**: Project 11

Parse and analyze log files with regex patterns, generate reports, and detect anomalies. Handle multiple log formats.

**Key Skills**: Regex, Pattern matching, Text processing, Reporting

---

**[Project 13: System Monitor Dashboard](project-13-system-monitor.md)**  
**Time**: 20-30 hours | **Prerequisites**: Projects 11-12

Create a web dashboard showing system metrics with charts and alerts. Combine backend monitoring with frontend visualization.

**Key Skills**: Metrics collection, Visualization, APIs, WebSockets

---

### Advanced Systems (14-16)

**[Project 14: Custom Shell/Terminal](project-14-custom-shell.md)**  
**Time**: 25-35 hours | **Prerequisites**: Project 11

Build your own command-line shell with pipes, redirects, job control, and command history. Understand how bash works.

**Key Skills**: Processes, exec, Pipes, File descriptors, Signal handling

---

**[Project 15: Network Packet Sniffer](project-15-packet-sniffer.md)**  
**Time**: 30-40 hours | **Prerequisites**: Project 14

Capture and analyze network packets using raw sockets. Decode TCP/IP, HTTP, and DNS protocols.

**Key Skills**: Raw sockets, TCP/IP, Protocol analysis, Packet capture

---

**[Project 16: System Call Tracer](project-16-syscall-tracer.md)**  
**Time**: 30-40 hours | **Prerequisites**: Projects 14-15

Build a tool like `strace` that traces system calls made by programs. Deep dive into process debugging.

**Key Skills**: ptrace, System calls, Process debugging, Binary analysis

---

### Database & Search (17-18)

**[Project 17: NoSQL API (MongoDB & Redis)](project-17-nosql-api.md)**  
**Time**: 30-40 hours | **Prerequisites**: Project 7

Integrate MongoDB for documents and Redis for caching/sessions. Build a hybrid data layer for scalable applications.

**Key Skills**: NoSQL, Caching, Sessions, Data modeling, Performance

---

**[Project 18: Search Engine (OpenSearch/Elasticsearch)](project-18-search-engine.md)**  
**Time**: 35-45 hours | **Prerequisites**: Project 17

Implement full-text search with OpenSearch/Elasticsearch. Build autocomplete, faceted search, and relevance scoring.

**Key Skills**: Full-text search, Indexing, Aggregations, Search algorithms

---

## Learning Objectives

After completing Intermediate projects, you will:

✅ Build production REST APIs with databases  
✅ Implement real-time features with WebSockets  
✅ Work with TCP/IP and network protocols  
✅ Interact with operating system APIs  
✅ Handle system-level programming  
✅ Use NoSQL databases effectively  
✅ Implement full-text search  
✅ Write concurrent and scalable code

---

## Progression Path

```
Project 7 (REST API) ← CRITICAL MILESTONE
    ↓
    ├→ Project 8 (WebSocket)
    ├→ Project 9 (File Sync)
    ├→ Project 10 (Web Scraper)
    ├→ Project 17 (NoSQL)
    └→ Project 18 (Search)

Project 11 (Process Monitor)
    ↓
    ├→ Project 12 (Log Analyzer)
    └→ Project 13 (System Monitor)
         ↓
         Project 14 (Shell)
              ↓
              ├→ Project 15 (Packet Sniffer)
              └→ Project 16 (Syscall Tracer)
```

**Can work in parallel**: Web Track (7-10, 17-18) and Systems Track (11-16)

---

## Time Estimate

- **Minimum**: 24 weeks (2 per project)
- **Recommended**: 32-48 weeks (3-4 per project)
- **Total Hours**: 290-430 hours

---

## Tips for Success

1. **Project 7 is crucial** - REST API is foundation for many others
2. **Test thoroughly** - Write unit and integration tests
3. **Handle errors** - Production-quality error handling
4. **Add observability** - Logging, metrics from the start
5. **Security matters** - Input validation, authentication, HTTPS
6. **Performance counts** - Profile and optimize
7. **Document well** - API docs, architecture decisions

---

## After Intermediate

You'll be ready for:
- **Advanced Level** (Projects 19-21) - Systems programming
- **Expert Level** (Projects 22-25) - Distributed systems
- **Job Applications** - Mid-level backend positions

---

## Next Steps

- Start with **[Project 7: REST API](project-07-rest-api.md)**
- Review **[Getting Started](../../getting-started.md)** for database setup
- Check **[Observability Guide](../../guides/observability-monitoring.md)**
- Reference **[Projects Index](../../projects-index.md)** for the full roadmap

---

**Ready for the next level?** Project 7 awaits! 🚀
