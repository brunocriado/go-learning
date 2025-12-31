# Complete Projects Index

A comprehensive index of all 54 Golang learning projects, organized by difficulty level and skill focus.

**📊 Current Status**: 18 of 54 projects fully documented (33%) | 36 projects with placeholder files

**✅ Complete**: Projects 1-18 (Basic + Intermediate levels)
**⏳ Placeholders**: Projects 19-54 (Advanced, Expert, Specialized, Bonus)
**📚 Guides**: Observability guide and resources file now available!

**Quick Links:**
- [Complete Projects Index](#complete-projects-index)
  - [🟢 Basic Level (1-6) - Foundations](#-basic-level-1-6---foundations)
  - [🟡 Intermediate Level (7-18) - Backend Development](#-intermediate-level-7-18---backend-development)
  - [🔴 Advanced Level (19-21) - Systems Programming](#-advanced-level-19-21---systems-programming)
  - [⚫ Expert Level (22-30) - Distributed Systems](#-expert-level-22-30---distributed-systems)
  - [🟣 Specialized (31-36) - Production \& Cloud-Native](#-specialized-31-36---production--cloud-native)
  - [🎁 Bonus Projects (36-54) - Advanced Go Features](#-bonus-projects-36-54---advanced-go-features)
    - [Language Features \& Advanced Topics](#language-features--advanced-topics)
    - [Distributed System Patterns](#distributed-system-patterns)
    - [Third-Party Integrations](#third-party-integrations)
    - [Performance \& Optimization](#performance--optimization)
  - [Project Tracks](#project-tracks)
    - [🎯 Critical Path (Fastest to Employability)](#-critical-path-fastest-to-employability)
    - [🔧 Systems Track](#-systems-track)
    - [☁️ Cloud-Native Track](#️-cloud-native-track)
    - [📊 Data Engineering Track](#-data-engineering-track)
  - [How to Use This Index](#how-to-use-this-index)
  - [Legend](#legend)
  - [Next Steps](#next-steps)

---

## 🟢 Basic Level (1-6) - Foundations
**Time**: 1-2 weeks each | **Total**: 6-12 weeks

Master Go fundamentals, CLI development, file I/O, HTTP clients, and basic concurrency.

| # | Project | Key Concepts | Time | Prerequisites |
|---|---------|-------------|------|---------------|
| 1 | [CLI Todo App](projects/01-basic/project-01-cli-todo.md) | File I/O, JSON, CLI flags | 8-12h | None (Start here!) |
| 2 | [URL Shortener](projects/01-basic/project-02-url-shortener.md) | HTTP server, Hash maps, Web basics | 10-15h | Project 1 |
| 3 | [File Organizer](projects/01-basic/project-03-file-organizer.md) | Recursion, File system, Regex | 12-18h | Project 1 |
| 4 | [System Process Monitor](projects/01-basic/project-04-process-monitor.md) | OS APIs, /proc, Real-time updates | 15-20h | Projects 1-2 |
| 5 | [Log Analyzer](projects/01-basic/project-05-log-analyzer.md) | Regex, Pattern matching, Reporting | 15-25h | Projects 1, 4 |
| 6 | [System Monitor](projects/01-basic/project-06-system-monitor.md) | Metrics, Visualization, APIs | 20-30h | Projects 4-5 |

**🎓 After Basic**: You can build CLI tools, simple web servers, and understand Go fundamentals.

**[View All Basic Projects →](projects/01-basic/)**

---

## 🟡 Intermediate Level (7-18) - Backend Development
**Time**: 2-4 weeks each | **Total**: 24-48 weeks

Build production-ready backends with databases, real-time systems, and network services.

| # | Project | Key Concepts | Time | Prerequisites |
|---|---------|-------------|------|---------------|
| 7 | [REST API + Database](projects/02-intermediate/project-07-rest-api.md) | SQL, JWT, Middleware, Testing | 20-30h | Projects 4-5 |
| 8 | [WebSocket Chat](projects/02-intermediate/project-08-websocket-chat.md) | WebSockets, Pub/Sub, Real-time | 20-30h | Project 7 |
| 9 | [File Sync Tool](projects/02-intermediate/project-09-file-sync.md) | TCP, Protocols, Checksums | 25-35h | Project 7 |
| 10 | [Web Scraper](projects/02-intermediate/project-10-web-scraper.md) | Concurrency, HTML parsing, Politeness | 25-35h | Projects 7-8 |
| 11 | [System Monitor (Advanced)](projects/02-intermediate/project-11-system-monitor.md) | Metrics, TUI, Real-time data | 25-35h | Projects 1-5 |
| 12 | [Process Manager](projects/02-intermediate/project-12-process-manager.md) | Process control, Signals, Supervision | 25-35h | Project 11 |
| 13 | [Advanced Log Analyzer](projects/02-intermediate/project-13-log-analyzer.md) | Complex patterns, Statistics, Alerting | 30-40h | Projects 11-12 |
| 14 | [Custom Shell](projects/02-intermediate/project-14-custom-shell.md) | Processes, exec, Pipes | 25-35h | Project 11 |
| 15 | [Packet Sniffer](projects/02-intermediate/project-15-packet-sniffer.md) | Raw sockets, TCP/IP, Protocols | 30-40h | Project 14 |
| 16 | [System Call Tracer](projects/02-intermediate/project-16-syscall-tracer.md) | ptrace, Syscalls, Debugging | 30-40h | Projects 14-15 |
| 17 | [MongoDB/Redis API](projects/02-intermediate/project-17-nosql-api.md) | NoSQL, Caching, Sessions | 30-40h | Project 7 |
| 18 | [OpenSearch Engine](projects/02-intermediate/project-18-search-engine.md) | Full-text search, Indexing, Aggregations | 35-45h | Project 17 |

**🎓 After Intermediate**: You can build production backends, work with databases, understand distributed systems basics.

**[View All Intermediate Projects →](projects/02-intermediate/)**

---

## 🔴 Advanced Level (19-21) - Systems Programming
**Time**: 4-8 weeks each | **Total**: 12-24 weeks

Deep dive into operating system internals, kernel programming, and virtualization.

| # | Project | Key Concepts | Time | Prerequisites |
|---|---------|-------------|------|---------------|
| 19 | [FUSE Filesystem](projects/03-advanced/project-19-fuse-filesystem.md) | Filesystem APIs, FUSE, Virtual FS | 40-60h | Projects 3, 9, 14 |
| 20 | [eBPF Monitor](projects/03-advanced/project-20-ebpf-monitor.md) | eBPF, Kernel tracing, Performance | 50-80h | Projects 11-16 |
| 21 | [Hypervisor (KVM)](projects/03-advanced/project-21-hypervisor.md) | Virtualization, KVM, VMs | 80-120h | Projects 19-20 |

**🎓 After Advanced**: You can work on infrastructure, contribute to systems software, understand kernel internals.

**[View All Advanced Projects →](projects/03-advanced/)**

---

## ⚫ Expert Level (22-30) - Distributed Systems
**Time**: 4-8 weeks each | **Total**: 36-72 weeks

Design and implement distributed systems, complex patterns, and fault-tolerant services.

| # | Project | Key Concepts | Time | Prerequisites |
|---|---------|-------------|------|---------------|
| 22 | [Design Patterns Library](projects/04-expert/project-22-design-patterns.md) | All GoF patterns, Concurrency patterns | 40-60h | Projects 7-18 |
| 23 | [Testing Framework](projects/04-expert/project-23-testing-framework.md) | Testing, Benchmarking, Fuzzing, Mocks | 30-40h | Any 10 projects |
| 24 | [Message Queue System](projects/04-expert/project-24-message-queue.md) | Event-driven, Pub/Sub, Async | 50-70h | Projects 7, 17 |
| 25 | [Distributed Cache](projects/04-expert/project-25-distributed-cache.md) | Caching, Rate limiting, Algorithms | 40-60h | Project 17 |
| 26 | [Load Balancer](projects/04-expert/project-26-placeholder.md) | Load balancing, Health checks, Discovery | 40-60h | Projects 7, 24 |
| 27 | [Context Patterns](projects/04-expert/project-27-placeholder.md) | Context, Cancellation, Timeouts | 20-30h | Projects 7-10 |
| 28 | [gRPC Microservices](projects/04-expert/project-28-placeholder.md) | gRPC, Protobuf, Streaming | 50-70h | Projects 7, 26 |
| 29 | [Distributed Tracing](projects/04-expert/project-29-placeholder.md) | OpenTelemetry, Tracing, APM | 30-50h | Project 28 |
| 30 | [Auth System](projects/04-expert/project-30-placeholder.md) | JWT, OAuth, RBAC, Security | 40-60h | Project 7 |

**🎓 After Expert**: You can design distributed systems, implement complex patterns, build fault-tolerant services.

**[View All Expert Projects →](projects/04-expert/)**

---

## 🟣 Specialized (31-36) - Production & Cloud-Native
**Time**: 2-6 weeks each | **Total**: 12-36 weeks

Deploy to production, build cloud-native apps, and master DevOps practices.

| # | Project | Key Concepts | Time | Prerequisites |
|---|---------|-------------|------|---------------|
| 31 | [CI/CD Pipeline](projects/05-specialized/project-31-placeholder.md) | GitHub Actions, Testing, Deployment | 30-50h | Project 23 |
| 32 | [Kubernetes Operator](projects/05-specialized/project-32-placeholder.md) | K8s API, Controllers, CRDs | 60-90h | Projects 19, 28 |
| 33 | [Profiling & Optimization](projects/05-specialized/project-33-placeholder.md) | pprof, Benchmarks, Memory | 30-40h | Projects 7, 23 |
| 34 | [Payment Integration](projects/05-specialized/project-34-placeholder.md) | Stripe API, Webhooks, Idempotency | 40-60h | Projects 7, 30 |
| 35 | [Multi-Cloud Storage](projects/05-specialized/project-35-placeholder.md) | S3, GCS, Azure, Abstractions | 35-50h | Projects 7, 9 |
| 36 | [Reflection Deep Dive](projects/05-specialized/project-36-placeholder.md) | Reflection, Type inspection, Dynamic code | 20-30h | Projects 7, 22 |

**🎓 After Specialized**: You can deploy to production, work in DevOps, handle real-world integrations, optimize at scale.

**[View All Specialized Projects →](projects/05-specialized/)**

---

## 🎁 Bonus Projects (36-54) - Advanced Go Features
**Time**: Variable | Deep expertise in Go-specific features and patterns

Master advanced Go features, architectural patterns, and third-party integrations.

### Language Features & Advanced Topics

| # | Project | Key Concepts | Time |
|---|---------|-------------|------|
| 36 | [Reflection Deep Dive](projects/06-bonus/project-36-reflection.md) | Reflection, Type inspection, Dynamic code | 20-30h |
| 37 | [Generics Guide](projects/06-bonus/project-37-generics.md) | Type parameters, Constraints, Generic algorithms | 20-30h |
| 38 | [Embed Package](projects/06-bonus/project-38-embed.md) | Static file embedding, Assets | 10-15h |
| 39 | [Build Tags](projects/06-bonus/project-39-build-tags.md) | Conditional compilation, Platform-specific | 15-20h |
| 40 | [CGO Integration](projects/06-bonus/project-40-cgo.md) | C interop, Foreign functions | 25-35h |
| 41 | [Go Modules Advanced](projects/06-bonus/project-41-go-modules.md) | Dependencies, Versioning, Workspaces | 15-25h |
| 42 | [Assembly Optimization](projects/06-bonus/project-42-assembly.md) | Go assembly, Hot paths, Performance | 30-40h |

### Distributed System Patterns

| # | Project | Key Concepts | Time |
|---|---------|-------------|------|
| 43 | [Saga Pattern](projects/06-bonus/project-43-saga-pattern.md) | Distributed transactions, Compensation | 30-40h |
| 44 | [CQRS](projects/06-bonus/project-44-cqrs.md) | Command Query separation, Event sourcing | 30-40h |
| 45 | [Bulkhead Pattern](projects/06-bonus/project-45-bulkhead.md) | Failure isolation, Circuit breakers | 20-30h |
| 46 | [Sidecar Pattern](projects/06-bonus/project-46-sidecar.md) | Service mesh, Proxy patterns | 25-35h |
| 47 | [Strangler Fig](projects/06-bonus/project-47-strangler-fig.md) | Legacy migration, Incremental refactoring | 30-40h |
| 48 | [Database per Service](projects/06-bonus/project-48-database-per-service.md) | Polyglot persistence, Data ownership | 25-35h |

### Third-Party Integrations

| # | Project | Key Concepts | Time |
|---|---------|-------------|------|
| 49 | [Email Service](projects/06-bonus/project-49-email-service.md) | SendGrid, AWS SES, Templates | 20-30h |
| 50 | [SMS Integration](projects/06-bonus/project-50-sms-integration.md) | Twilio, Message queuing | 15-25h |
| 51 | [Search Integration](projects/06-bonus/project-51-search-integration.md) | Algolia, Meilisearch, Full-text | 25-35h |
| 52 | [Social Auth](projects/06-bonus/project-52-social-auth.md) | OAuth providers, SSO | 20-30h |

### Performance & Optimization

| # | Project | Key Concepts | Time |
|---|---------|-------------|------|
| 53 | [Lock-Free Programming](projects/06-bonus/project-53-lock-free.md) | Atomic operations, CAS, Memory ordering | 30-40h |
| 54 | [SIMD Instructions](projects/06-bonus/project-54-simd.md) | Vector operations, Assembly, Performance | 35-45h |

**[View All Bonus Projects →](projects/06-bonus/)**

---

## Project Tracks

### 🎯 Critical Path (Fastest to Employability)
**Total**: ~300-400 hours | Projects: 1, 4, 7, 17, 23, 27, 28, 30

### 🔧 Systems Track
**Total**: ~500-700 hours | Projects: 1, 3, 11-16, 19-21, 33

### ☁️ Cloud-Native Track
**Total**: ~400-600 hours | Projects: 1-7, 13, 24, 26, 28-29, 31-32

### 📊 Data Engineering Track
**Total**: ~350-500 hours | Projects: 1-7, 10, 12, 17-18, 24-25

---

## How to Use This Index

1. **Start at the top** if you're a complete beginner
2. **Use the [Skill Assessment](getting-started.md#skill-assessment)** to find your level
3. **Follow a [Learning Path](getting-started.md#learning-paths)** for structured progression
4. **Check prerequisites** before starting any project
5. **Track your progress** - aim to complete at least 10 projects for employability

---

## Legend

- **Time**: Estimated hours to complete with full features and tests
- **Prerequisites**: Projects you should complete first
- **Key Concepts**: Main technologies and patterns you'll learn
- **🎓**: Skills you'll have after completing this level

---

## Next Steps

- **[Back to README](README.md)** for overview and motivation
- **[Getting Started Guide](getting-started.md)** for setup and paths
- **[Start Project 1](projects/01-basic/project-01-cli-todo.md)** and begin your journey
- **[Observability Guide](guides/observability-monitoring.md)** for logging, metrics, and tracing
- **[Learning Resources](resources.md)** for books, courses, and community

---

**Total Learning Time**: 1,200-2,000 hours for all 54 projects (18-24 months part-time)

**Career Impact**: Complete 10 projects → Junior-Mid level | 20 projects → Mid-Senior | 35+ projects → Senior-Staff level
