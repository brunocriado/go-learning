# Golang Learning Projects: Build Your Mastery

**54 Production-Ready Projects** | **Complete Roadmap Coverage** | **Zero to Expert**

> 🎯 **Complete Coverage**: [roadmap.sh/golang](https://roadmap.sh/golang) + [roadmap.sh/system-design](https://roadmap.sh/system-design)
> 🚀 **From Basics to Expert**: CLI tools → Microservices → Kernel Programming → Distributed Systems
> ⏱️ **Realistic Timeline**: 18-24 months for complete mastery (can focus on 20-30 core projects)
> 💼 **Career Ready**: Build a portfolio that lands senior engineering roles
> 📦 **Modular Learning**: Pick projects matching your career path—not all 54 are required

---

## 📚 Table of Contents

### Quick Navigation
- [Why These Projects](#why-these-projects-matter)
- [How to Use This Guide](#how-to-use-this-guide)
- [Prerequisites Flowchart](#prerequisites-flowchart)
- [Common Setup Guide](#common-development-environment-setup)
- [Learning Paths](#learning-paths)
- [Project Index](#complete-project-index)

### Project Categories
- **[Basic Projects (1-6)](#golang-learning-projects---basic-level)** - Foundations (Weeks 1-8)
- **[Intermediate Projects (7-18)](#golang-learning-projects---intermediate-level)** - Backend Development (Months 3-8)
- **[Advanced Projects (19-21)](#golang-learning-projects---advanced-level)** - Systems Programming (Months 9-12)
- **[Expert Projects (22-25)](#expert-level-projects)** - Distributed Systems (Months 13-16)
- **[Specialized Projects (26-35)](#specialized-projects)** - Production Skills (Months 17-24)

### Supplementary Sections
- [Observability & Monitoring](#observability--monitoring-guide)
- [12-Factor App Methodology](#12-factor-app-methodology)
- [Deployment Guides](#deployment-to-production)
- [Security Checklists](#security-best-practices)
- [Interview Preparation](#technical-interview-guide)
- [Resources & Community](#resources-and-community)

---

## Complete Project Index

### 🟢 Basic Level (1-6) - Foundations
**Time**: 1-2 weeks each | **Total**: 6-12 weeks

| # | Project | Key Concepts | Time | Prerequisites |
|---|---------|-------------|------|---------------|
| 1 | [CLI Todo App](#project-1-cli-todo-application) | File I/O, JSON, CLI flags | 8-12h | None (Start here!) |
| 2 | [Weather CLI](#project-2-weather-cli-tool) | HTTP clients, APIs, JSON parsing | 10-15h | Project 1 |
| 3 | [File Organizer](#project-3-file-organizer-tool) | Recursion, File system, Regex | 12-18h | Project 1 |
| 4 | [URL Shortener](#project-4-url-shortener-web-service) | HTTP server, Hash maps, Web basics | 15-20h | Projects 1-2 |
| 5 | [RSS Aggregator](#project-5-rss-aggregator) | XML parsing, Goroutines, Scheduling | 15-25h | Projects 2, 4 |
| 6 | [Markdown Blog](#project-6-markdown-blog-generator) | Templates, Static sites, File processing | 15-25h | Projects 3, 4 |

**🎓 After Basic**: You can build CLI tools, simple web servers, and understand Go fundamentals.

---

### 🟡 Intermediate Level (7-18) - Backend Development
**Time**: 2-4 weeks each | **Total**: 24-48 weeks

| # | Project | Key Concepts | Time | Prerequisites |
|---|---------|-------------|------|---------------|
| 7 | [REST API + Database](#project-1-rest-api-with-database) | SQL, JWT, Middleware, Testing | 20-30h | Projects 4-5 |
| 8 | [WebSocket Chat](#project-2-websocket-chat-server) | WebSockets, Pub/Sub, Real-time | 20-30h | Project 7 |
| 9 | [File Sync Tool](#project-3-file-sync-tool) | TCP, Protocols, Checksums | 25-35h | Project 7 |
| 10 | [Web Scraper](#project-4-web-scraper--crawler) | Concurrency, HTML parsing, Politeness | 25-35h | Projects 7-8 |
| 11 | [Process Monitor](#project-1-process-monitor) | OS APIs, /proc, Real-time updates | 15-20h | Projects 1-5 |
| 12 | [Log Analyzer](#project-2-log-analyzer) | Regex, Pattern matching, Reporting | 15-20h | Project 11 |
| 13 | [System Monitor](#project-3-system-monitor-dashboard) | Metrics, Visualization, APIs | 20-30h | Projects 11-12 |
| 14 | [Custom Shell](#project-1-custom-shell) | Processes, exec, Pipes | 25-35h | Project 11 |
| 15 | [Packet Sniffer](#project-2-network-packet-sniffer) | Raw sockets, TCP/IP, Protocols | 30-40h | Project 14 |
| 16 | [System Call Tracer](#project-3-system-call-tracer) | ptrace, Syscalls, Debugging | 30-40h | Projects 14-15 |
| 17 | [MongoDB/Redis API](#project-3a-nosql-api-mongodb--redis) | NoSQL, Caching, Sessions | 30-40h | Project 7 |
| 18 | [OpenSearch Engine](#project-3b-search-engine-opensearch--elasticsearch) | Full-text search, Indexing, Aggregations | 35-45h | Project 17 |

**🎓 After Intermediate**: You can build production backends, work with databases, understand distributed systems basics.

---

### 🔴 Advanced Level (19-21) - Systems Programming
**Time**: 4-8 weeks each | **Total**: 12-24 weeks

| # | Project | Key Concepts | Time | Prerequisites |
|---|---------|-------------|------|---------------|
| 19 | [FUSE Filesystem](#project-1-fuse-filesystem) | Filesystem APIs, FUSE, Virtual FS | 40-60h | Projects 3, 9, 14 |
| 20 | [eBPF Monitor](#project-2-ebpf-monitoring-tool) | eBPF, Kernel tracing, Performance | 50-80h | Projects 11-16 |
| 21 | [Hypervisor (KVM)](#project-3-hypervisor-kvm-based) | Virtualization, KVM, VMs | 80-120h | Projects 19-20 |

**🎓 After Advanced**: You can work on infrastructure, contribute to systems software, understand kernel internals.

---

### ⚫ Expert Level (22-25) - Distributed Systems
**Time**: 4-8 weeks each | **Total**: 16-32 weeks

| # | Project | Key Concepts | Time | Prerequisites |
|---|---------|-------------|------|---------------|
| 22 | [Design Patterns Library](#project-22-design-patterns-library--demo-system) | All GoF patterns, Concurrency patterns | 40-60h | Projects 7-18 |
| 23 | [Testing Framework](#project-23-testing-framework--advanced-testing) | Testing, Benchmarking, Fuzzing, Mocks | 30-40h | Any 10 projects |
| 24 | [Message Queue System](#project-24-message-queue--event-driven-system) | Event-driven, Pub/Sub, Async | 50-70h | Projects 7, 17 |
| 25 | [Distributed Cache](#project-25-distributed-cache--rate-limiter) | Caching, Rate limiting, Algorithms | 40-60h | Project 17 |

**🎓 After Expert**: You can design distributed systems, implement complex patterns, build fault-tolerant services.

---

### 🟣 Specialized (26-35) - Production & Cloud-Native
**Time**: 2-6 weeks each | **Total**: 24-48 weeks

| # | Project | Key Concepts | Time | Prerequisites |
|---|---------|-------------|------|---------------|
| 26 | [Load Balancer](#project-26-service-mesh--load-balancer) | Load balancing, Health checks, Discovery | 40-60h | Projects 7, 24 |
| 27 | [Context Patterns](#project-27-context--cancellation-patterns) | Context, Cancellation, Timeouts | 20-30h | Projects 7-10 |
| 28 | [gRPC Microservices](#project-28-grpc-microservices) | gRPC, Protobuf, Streaming | 50-70h | Projects 7, 26 |
| 29 | [Distributed Tracing](#project-29-distributed-tracing--apm) | OpenTelemetry, Tracing, APM | 30-50h | Project 28 |
| 30 | [Auth System](#project-30-authentication--authorization-system) | JWT, OAuth, RBAC, Security | 40-60h | Project 7 |
| 31 | [CI/CD Pipeline](#project-31-cicd-pipeline-builder) | GitHub Actions, Testing, Deployment | 30-50h | Project 23 |
| 32 | [Kubernetes Operator](#project-32-kubernetes-operator) | K8s API, Controllers, CRDs | 60-90h | Projects 21, 28 |
| 33 | [Profiling & Optimization](#project-33-profiling--performance-optimization) | pprof, Benchmarks, Memory | 30-40h | Projects 7, 23 |
| 34 | [Payment Integration](#project-34-payment-processing-system) | Stripe API, Webhooks, Idempotency | 40-60h | Projects 7, 30 |
| 35 | [Multi-Cloud Storage](#project-35-multi-cloud-storage-abstraction) | S3, GCS, Azure, Abstractions | 35-50h | Projects 7, 9 |

**🎓 After Specialized**: You can deploy to production, work in DevOps, handle real-world integrations, optimize at scale.

---

## Why These Projects Matter

You're about to embark on something real. Not another tutorial hell where you copy-paste code and forget it in a week. These projects will make you **competent**—the kind of developer who can build, deploy, and maintain production systems.

**The Reality:**
- 90% of developers never build complete systems. They know syntax but freeze when faced with real problems.
- Go powers Docker, Kubernetes, Terraform, Prometheus, and half the cloud infrastructure you use daily. Learning it isn't a hobby—it's a career investment.
- These **54 projects** cover everything from CLI tools to distributed systems: REST APIs, WebSockets, databases (SQL + NoSQL), caching, message queues, microservices, Kubernetes operators, kernel programming (eBPF, FUSE), and cloud-native patterns (CQRS, Saga, Circuit Breaker).
- You don't need all 54—focus on **20-30 projects** aligned with your career goals (backend, DevOps, systems programming, or distributed systems).
- You'll learn production best practices including the [12-Factor App methodology](https://12factor.net/)—the industry standard for building modern, scalable, maintainable services.
- Includes **advanced patterns**: Design Patterns (GoF + Go-specific), distributed transactions (Saga), event sourcing (CQRS), resilience patterns (Bulkhead, Circuit Breaker), and service mesh concepts (Sidecar, Strangler Fig).

**What You'll Actually Gain:**

*Technical Depth:*
- **Systems thinking**: You'll understand how software actually works—not just frameworks, but TCP, HTTP, filesystems, memory, processes, distributed coordination.
- **Production skills**: Error handling, logging, testing, performance, concurrency, observability, security—things that separate hobbyists from professionals.
- **Tool building**: By project 5, you'll be building tools that solve your own problems. By project 15, you'll be contributing to open source. By project 30, you'll be designing architectures at scale.

*Career Impact:*
- Go developers earn 20-40% more than average. It's in high demand and undersupplied.
- These projects give you portfolio pieces that prove competence. A working REST API with tests beats 100 tutorials on a resume. A distributed tracing system gets you senior roles.
- You'll speak the language of backend, DevOps, SRE, and infrastructure teams—where the high-leverage problems and compensation are.

**The Honest Truth:**
- This will be hard. You'll get stuck. You'll debug for hours. You'll question if you're "smart enough."
- That struggle is the point. Every bug you fix, every feature you implement, every concept that finally clicks—that's your brain rewiring itself to think like an engineer.
- Most people quit at project 3. If you finish 10, you're in the top 5% of self-taught developers. If you complete 20-30 core projects aligned with your goals, you're employable at top-tier companies and can command senior-level compensation.

**What Makes This Different:**
- **No hand-holding**: You get guidance, not solutions. You'll have to think, search, experiment. That's how real skills form. (Solutions repo available at end for verification)
- **Progressive complexity**: Starts with CLI tools, builds through web services and systems programming, culminates in distributed systems, cloud-native architectures, and advanced patterns.
- **Real-world focus**: Every project solves actual problems. You'll build things you can use, deploy to production, show in interviews, and be genuinely proud of.
- **Modular path**: 54 projects covering everything from basics to expert-level distributed patterns. Pick 20-30 that align with your career goals—you don't need all of them.

**A Challenge:**
- Commit to one project per week (basic), two weeks (intermediate), month (advanced/expert), or 6 weeks (specialized).
- Build every feature. Write comprehensive tests. Handle errors properly. Make it production-quality with observability and security.
- When you finish project 10, you'll look back at project 1 and cringe at your old code. That's growth.
- When you finish project 20, you'll be the developer who can build anything at the systems level.
- When you complete 30+ projects, you'll be the engineer companies fight to hire—with deep expertise in Go, distributed systems, cloud-native patterns, and production engineering.

**The projects are ordered by difficulty. Start at the beginning. Don't skip. Each one teaches concepts you'll need later.**

You won't become a master in 6 months. But in 12 months, you'll be dangerous. In 18-24 months, you'll be irreplaceable. In interviews, you'll confidently discuss distributed systems, performance optimization, and production war stories—because you've lived them.

**The reality:** Most developers focus on 20-30 projects aligned with their career goals. That's enough to go from beginner to employable senior engineer. The full 54 projects cover specialized topics (eBPF, hypervisors, advanced patterns) that you can explore based on your interests.

Now build something you can be proud of.

---

## How to Use This Guide

### For Complete Beginners
1. Start with **Project 1** (CLI Todo)
2. Complete all **Basic projects (1-6)** in order
3. Follow the **Foundations learning path**
4. Move to Intermediate only after completing all Basic
5. **Goal:** Projects 1-18 give you employable backend skills (12-18 months)

### For Experienced Developers
1. Review the [Prerequisites Flowchart](#prerequisites-flowchart)
2. Take the [Skill Assessment Quiz](#skill-assessment)
3. Jump to your level, but complete prerequisite projects first
4. Consider doing projects 23 (Testing) and 27 (Context) early
5. **Pick 20-30 projects** aligned with your career goals from the full catalog of 54

### For Career Switchers
1. Follow the [Backend Engineer Path](#backend-engineer-path) (Projects 1-18, 23, 27-30)
2. Budget 12-18 months of part-time work
3. Build a portfolio site showcasing 3-5 completed projects
4. Focus on projects 7, 17, 28, 30 for interviews
5. **20-25 projects** from the catalog will make you competitive

### For Systems Programmers
1. Complete Basic and Intermediate quickly (review if needed)
2. Focus on Advanced (19-21) and Expert (22-30) projects
3. Add Specialized projects (31-36) for production skills
4. Explore Bonus projects (37-54) for deep specialization: eBPF, generics, CGO, advanced patterns
5. **25-35 projects** will make you a systems expert

---

## Prerequisites Flowchart

```
START HERE
    ↓
[Project 1: CLI Todo] ← No prerequisites
    ↓
    ├→ [Project 2: Weather CLI]
    ├→ [Project 3: File Organizer]
    └→ [Project 4: URL Shortener]
         ↓
         ├→ [Project 5: RSS Aggregator] (needs 2, 4)
         └→ [Project 6: Markdown Blog] (needs 3, 4)
              ↓
         BASIC COMPLETE ✓
              ↓
         [Project 7: REST API] ← Prerequisite for most Intermediate+
              ↓
              ├→ [Project 8: WebSocket Chat]
              ├→ [Project 9: File Sync]
              ├→ [Project 10: Web Scraper]
              ├→ [Project 17: NoSQL API]
              └→ [Project 18: OpenSearch]
              ↓
         [Projects 11-16: Systems Projects] ← Can do in parallel
              ↓
         INTERMEDIATE COMPLETE ✓
              ↓
         [Project 19: FUSE FS] (needs 3, 9, 14)
              ↓
         [Project 20: eBPF] (needs 11-16)
              ↓
         [Project 21: Hypervisor] (needs 19-20)
              ↓
         ADVANCED COMPLETE ✓
              ↓
         ┌─────────────────────────────────────┐
         │ EXPERT & SPECIALIZED (22-36)        │
         │ Pick based on career goals          │
         └─────────────────────────────────────┘
              ↓
         ├→ [22: Design Patterns] (needs 7-18)
         ├→ [23: Testing Framework] (needs any 10 projects)
         ├→ [24: Message Queue] (needs 7, 17)
         ├→ [25: Distributed Cache] (needs 17)
         ├→ [26: Load Balancer] (needs 7, 24)
         ├→ [27: Context Patterns] (needs 7-10) ← Do early
         ├→ [28: gRPC Services] (needs 7, 26)
         ├→ [29: Distributed Tracing] (needs 28)
         ├→ [30: Auth System] (needs 7)
         ├→ [31: CI/CD Pipeline] (needs 23)
         ├→ [32: K8s Operator] (needs 21, 28)
         ├→ [33: Profiling] (needs 7, 23)
         ├→ [34: Payments] (needs 7, 30)
         ├→ [35: Multi-Cloud] (needs 7, 9)
         └→ [36: Reflection] (needs 7, 23)
              ↓
         ┌─────────────────────────────────────┐
         │ BONUS PROJECTS (37-54)              │
         │ Advanced specializations (optional) │
         └─────────────────────────────────────┘
              ↓
         ├→ [37-42: Language Features] (Generics, Embed, Build Tags, CGO, Modules, Assembly)
         ├→ [43-48: Advanced Patterns] (Saga, CQRS, Bulkhead, Sidecar, Strangler Fig, Database per Service)
         ├→ [49-54: Extended Services] (Email, Notifications, Workflow Engine, Rate Limiter, API Gateway, Service Mesh)
              ↓
         COMPLETE MASTERY ✓
         YOU'RE NOW A GO EXPERT!
```

---

### Dependency Matrix

**Independent Tracks** (can learn in parallel):
- **Web Track**: 1→4→7→8→17→18→28→30→34
- **Systems Track**: 1→3→11→12→13→14→15→16→19→20→21→32
- **Infrastructure Track**: 7→23→24→25→26→29→31→32→36
- **Optimization Track**: 23→27→33
- **Patterns Track**: 22→37-54 (Bonus projects: advanced patterns and features)

**Critical Path** (fastest to employability):
Projects: 1, 4, 7, 17, 23, 27, 28, 30 (≈300-400 hours)

**Specialized Extensions** (pick based on interests):
- **Cloud-Native**: 31→32→36 (CI/CD, K8s, Reflection)
- **Payments/Integration**: 30→34→35 (Auth, Payments, Cloud Storage)
### 🎯 Backend Engineer Path
**Goal**: Full-stack backend engineer ready for industry
**Time**: 12-18 months part-time
**Projects**: ~25 of 54 (focus on web track + production skills)

**Phase 1**: Foundations (Months 1-2)
- Projects 1-6 (all Basic)

**Phase 2**: Backend Core (Months 3-6)
- Projects 7 (REST API), 17 (NoSQL), 18 (Search)
- Project 23 (Testing)
- Add comprehensive tests to Phase 1 projects

**Phase 3**: Real-time & Distributed (Months 7-10)
- Projects 8 (WebSocket), 24 (Message Queue), 26 (Load Balancer)
- Projects 27 (Context), 28 (gRPC)

**Phase 4**: Production Ready (Months 11-15)
- Projects 29 (Tracing), 30 (Auth), 31 (CI/CD)
- Projects 34 (Payments), 35 (Cloud Storage)
- Add observability to all previous projects

**Phase 5**: Portfolio & Interview Prep (Months 16-18)
- Deploy 3-5 projects to production
- Document architecture decisions
- Practice system design interviews
- Contribute to open source

**Optional Extensions** (if time permits):
- Project 22 (Design Patterns) - Architecture skills
- Projects 43-45 (Saga, CQRS, Bulkhead) - Advanced distributed patterns
- Project 49 (Email Service) or 52 (Workflow Engine) - Business features

**Interview Focus**: Projects 7, 17, 28, 30, 26
**Phase 5**: Portfolio & Interview Prep (Months 16-18)
- Deploy 3-5 projects to production
- Document architecture decisions
- Practice system design interviews
### 🔧 Systems Programmer Path
**Goal**: Low-level systems, infrastructure, performance
**Time**: 15-24 months
**Projects**: ~30 of 54 (systems + low-level features)

**Phase 1**: Foundations (Months 1-2) - Projects 1-6

**Phase 2**: Systems Basics (Months 3-5)
- Projects 11-16 (all OS interaction)
- Project 14 (Shell) is critical

**Phase 3**: Advanced Systems (Months 6-12)
- Projects 19 (FUSE), 20 (eBPF), 21 (Hypervisor)
- These are challenging - take your time

**Phase 4**: Performance & Optimization (Months 13-18)
- Projects 23 (Testing), 27 (Context), 33 (Profiling)
- Optimize previous projects for performance

**Phase 5**: Production Systems (Months 19-24)
- Projects 22 (Patterns), 26 (Load Balancer), 32 (K8s)
- Project 36 (Reflection) - Metaprogramming
- Contribute to systems projects (containerd, runc, etc.)

**Deep Dive Extensions** (months 20-24):
- Project 40 (CGO) - Interface with C libraries
### ☁️ DevOps/SRE Path
**Goal**: Cloud-native operations, reliability engineering
**Time**: 12-18 months
**Projects**: ~28 of 54 (infrastructure + reliability)

**Phase 1**: Foundations (Months 1-2) - Projects 1-6

**Phase 2**: Backend Understanding (Months 3-5)
- Projects 7, 8, 17 (understand what you'll deploy)

**Phase 3**: Observability & Monitoring (Months 6-9)
- Project 13 (System Monitor)
- Complete **Observability section** (Prometheus, Grafana, Loki)
- Project 29 (Distributed Tracing)
- Add monitoring to all previous projects

**Phase 4**: Infrastructure (Months 10-15)
- Projects 24 (Message Queue), 26 (Load Balancer)
- Project 28 (gRPC - service mesh concepts)
- Project 31 (CI/CD Pipeline)
- Project 32 (Kubernetes Operator)

**Phase 5**: Production Mastery (Months 16-18)
- Projects 25 (Caching/Rate Limiting), 30 (Auth)
- Projects 33 (Profiling), 35 (Multi-Cloud)
- Implement on-call runbooks
- Chaos engineering experiments
- Multi-region deployments

**Resilience Extensions** (optional):
- Projects 43-45 (Saga, CQRS, Bulkhead) - Fault tolerance patterns
### 🚀 Full-Stack Path
**Goal**: Frontend + Backend + Deployment
**Time**: 15-20 months
**Projects**: ~22 of 54 (full-stack essentials)

**Phase 1**: Foundations (Months 1-2) - Projects 1-6

**Phase 2**: Backend (Months 3-8)
- Projects 7, 8, 17, 18, 23
- Learn React/Vue alongside (not covered here)

**Phase 3**: Integration (Months 9-14)
- Projects 28 (gRPC for BFF), 30 (Auth)
- Projects 34 (Payments), 35 (File Upload)
- Build frontend for projects 7, 8, 17

**Phase 4**: Production (Months 15-20)
- Projects 29 (Tracing), 31 (CI/CD)
- Projects 25 (Rate Limiting), 26 (Load Balancer)
- Deploy full-stack apps with CDN, edge

**User-Facing Extensions** (if time permits):
- Project 49 (Email Service) - Transactional emails
- Project 50 (Notifications) - Real-time notifications
- Project 53 (Rate Limiter) - API throttling for frontend
- Project 54 (API Gateway) - Backend for frontend pattern

**Interview Focus**: End-to-end system design, both frontend and backend, deployment strategies

### 🚀 Full-Stack Path
### 📊 Data Engineer Path
**Goal**: Data pipelines, ETL, analytics
**Time**: 12-16 months
**Projects**: ~20 of 54 (data-focused)

**Phase 1**: Foundations (Months 1-2) - Projects 1-6

**Phase 2**: Data Processing (Months 3-7)
- Projects 10 (Web Scraper), 12 (Log Analyzer)
- Projects 17 (NoSQL), 18 (OpenSearch)
- Learn Apache Kafka concepts in Project 24

**Phase 3**: Pipelines & Orchestration (Months 8-12)
- Project 24 (Message Queue - data streaming)
- Project 9 (File Sync - data transfer)
- Build ETL pipelines combining previous projects

**Phase 4**: Infrastructure (Months 13-16)
- Projects 25 (Caching), 31 (CI/CD for data pipelines)
- Projects 28 (gRPC for data services)
- Implement data warehouse patterns

**Data-Specific Extensions** (optional):
- Project 44 (CQRS) - Command Query Responsibility Segregation for analytics
- Project 48 (Database per Service) - Microservices data patterns
- Project 52 (Workflow Engine) - Data pipeline orchestration
- Project 35 (Multi-Cloud Storage) - Data lake patterns

**Interview Focus**: Projects 10, 12, 24, SQL optimization, streaming, CQRS patterns

### 📊 Data Engineer Path
**Goal**: Data pipelines, ETL, analytics
**Time**: 12-16 months

**Phase 1**: Foundations (Months 1-2) - Projects 1-6

**Phase 2**: Data Processing (Months 3-7)
- Projects 10 (Web Scraper), 12 (Log Analyzer)
- Projects 17 (NoSQL), 18 (OpenSearch)
- Learn Apache Kafka concepts in Project 24

**Phase 3**: Pipelines & Orchestration (Months 8-12)
- Project 24 (Message Queue - data streaming)
- Project 9 (File Sync - data transfer)
- Build ETL pipelines combining previous projects

**Phase 4**: Infrastructure (Months 13-16)
- Projects 25 (Caching), 31 (CI/CD for data pipelines)
- Projects 28 (gRPC for data services)
- Implement data warehouse patterns

**Interview Focus**: Projects 10, 12, 24, SQL optimization, streaming

---

## Skill Assessment

**Take this quiz to find your starting point:**

### Beginner (Start at Project 1)
- [ ] I've never written Go code
- [ ] I don't know what goroutines are
- [ ] I'm new to programming
- [ ] I've never built a web server

### Intermediate (Start at Project 7 after reviewing 1-6)
- [ ] I've built CLI tools in Go
- [ ] I understand goroutines and channels
- [ ] I've worked with JSON and HTTP
- [ ] I can write functions and structs

### Advanced (Start at Project 11 after completing 1-10)
- [ ] I've built REST APIs with databases
- [ ] I understand concurrency patterns
- [ ] I've deployed Go applications
- [ ] I'm comfortable with testing

### Expert (Start at Project 19 after completing 1-18)
- [ ] I've built production systems in Go
- [ ] I understand distributed systems concepts
- [ ] I've worked with multiple databases
- [ ] I can debug complex performance issues

### Master (Cherry-pick from projects 22-54)
- [ ] I've built systems programming projects
- [ ] I understand kernel interactions
- [ ] I've designed distributed architectures
- [ ] I contribute to major open source projects
- [ ] I want specialized skills: Kubernetes operators, profiling, advanced patterns (CQRS, Saga, Circuit Breaker)

---

## Common Development Environment Setup

**Complete this once**, then reference throughout projects.

### Initial Go Setup

```bash
# 1. Install Go (latest stable)
# macOS
brew install go

# Linux
wget https://go.dev/dl/go1.21.5.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.21.5.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin

# Windows
# Download installer from https://go.dev/dl/

# Verify
go version  # Should be 1.21+

# 2. Setup Go environment
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
# Add to ~/.bashrc or ~/.zshrc

# 3. Install common tools
go install golang.org/x/tools/gopls@latest        # Language server
go install golang.org/x/tools/cmd/goimports@latest # Import formatter
go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest # Linter
go install github.com/rakyll/hey@latest            # Load testing
```

### Editor Setup

**VS Code (Recommended for beginners):**
```bash
# Install VS Code from https://code.visualstudio.com/

# Install Go extension
code --install-extension golang.go

# Install useful extensions
code --install-extension ms-vscode.go
code --install-extension GitHub.copilot
code --install-extension eamodio.gitlens
```

**GoLand (Recommended for professionals):**
- Download from https://www.jetbrains.com/go/
- Free for students/open source
- Best debugging and refactoring tools

**Vim/Neovim:**
```bash
# Install vim-go
git clone https://github.com/fatih/vim-go.git ~/.vim/pack/plugins/start/vim-go

# Or use LazyVim/NvChad with Go LSP support
```

### Docker Setup

```bash
# macOS
brew install --cask docker

# Linux (Ubuntu/Debian)
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER

# Windows
# Download Docker Desktop from https://www.docker.com/products/docker-desktop

# Verify
docker --version
docker-compose --version

# Test
docker run hello-world
```

### Database Setup (for projects 7, 17, 18)

**PostgreSQL:**
```bash
# macOS
brew install postgresql@15
brew services start postgresql@15

# Linux
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql

# Create development database
createdb dev_db
psql dev_db
```

**Redis:**
```bash
# macOS
brew install redis
brew services start redis

# Linux
sudo apt install redis-server
sudo systemctl start redis-server

# Docker (all platforms)
docker run -d -p 6379:6379 redis:latest

# Test
redis-cli ping  # Should return PONG
```

**MongoDB:**
```bash
# macOS
brew tap mongodb/brew
brew install mongodb-community
brew services start mongodb-community

# Linux
# Follow: https://www.mongodb.com/docs/manual/installation/

# Docker (recommended)
docker run -d -p 27017:27017 mongo:latest

# Test
mongosh  # MongoDB shell
```

### API Testing Tools

```bash
# HTTPie (user-friendly curl)
brew install httpie  # macOS
pip install httpie   # Linux/Windows

# Test
http GET https://httpbin.org/get

# Postman (GUI)
# Download from https://www.postman.com/downloads/

# curl (pre-installed usually)
curl --version
```

### Monitoring Stack (for Observability section)

```bash
# Create docker-compose.yml for observability stack
cat > observability-stack.yml << 'EOF'
version: '3.8'
services:
  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml

  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin

  loki:
    image: grafana/loki:latest
    ports:
      - "3100:3100"

  jaeger:
    image: jaegertracing/all-in-one:latest
    ports:
      - "16686:16686"  # UI
      - "14268:14268"  # HTTP
      - "6831:6831/udp" # Agent

  redis:
    image: redis:latest
    ports:
      - "6379:6379"

  postgres:
    image: postgres:15
    ports:
      - "5432:5432"
    environment:
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: dev_db

  mongo:
    image: mongo:latest
    ports:
      - "27017:27017"
EOF

# Start all services
docker-compose -f observability-stack.yml up -d

# Access:
# Grafana: http://localhost:3000 (admin/admin)
# Prometheus: http://localhost:9090
# Jaeger: http://localhost:16686
```

### Git Setup

```bash
# Configure Git
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Generate SSH key for GitHub
ssh-keygen -t ed25519 -C "your.email@example.com"
cat ~/.ssh/id_ed25519.pub  # Add to GitHub

# Test
ssh -T git@github.com
```

### Project Template

```bash
# Create this template for new projects
mkdir -p ~/go-projects/template
cd ~/go-projects/template

cat > init_project.sh << 'EOF'
#!/bin/bash
if [ -z "$1" ]; then
    echo "Usage: ./init_project.sh project-name"
    exit 1
fi

PROJECT=$1
mkdir -p $PROJECT
cd $PROJECT

# Initialize Go module
go mod init github.com/yourusername/$PROJECT

# Create directory structure
mkdir -p cmd/$PROJECT
mkdir -p internal
mkdir -p pkg
mkdir -p api
mkdir -p web
mkdir -p scripts
mkdir -p deployments

# Create main.go
cat > cmd/$PROJECT/main.go << 'MAIN'
package main

import (
    "fmt"
    "log"
)

func main() {
    fmt.Println("$PROJECT starting...")
    log.Println("Ready!")
}
MAIN

# Create README
cat > README.md << 'README'
# $PROJECT

## Description
[Your project description]

## Prerequisites
- Go 1.21+
- [Other requirements]

## Installation
\`\`\`bash
go mod download
\`\`\`

## Usage
\`\`\`bash
go run cmd/$PROJECT/main.go
\`\`\`

## Testing
\`\`\`bash
go test ./...
\`\`\`

## License
MIT
README

# Create .gitignore
cat > .gitignore << 'IGNORE'
# Binaries
*.exe
*.exe~
*.dll
*.so
*.dylib
$PROJECT

# Test binary
*.test

# Output
*.out

# Go workspace file
go.work

# Environment
.env
.env.local

# IDE
.vscode/
.idea/
*.swp
*.swo
*~

# OS
.DS_Store
Thumbs.db

# Logs
*.log

# Database
*.db
*.sqlite
*.sqlite3
IGNORE

# Create Makefile
cat > Makefile << 'MAKE'
.PHONY: build run test lint clean

build:
\tgo build -o bin/$PROJECT cmd/$PROJECT/main.go

run:
\tgo run cmd/$PROJECT/main.go

test:
\tgo test -v ./...

test-coverage:
\tgo test -coverprofile=coverage.out ./...
\tgo tool cover -html=coverage.out

lint:
\tgolangci-lint run

clean:
\trm -rf bin/
\trm -f coverage.out
MAKE

# Initialize git
git init
git add .
git commit -m "Initial commit"

echo "Project $PROJECT initialized!"
echo "Next steps:"
echo "  cd $PROJECT"
echo "  make run"
EOF

chmod +x init_project.sh
```

### Troubleshooting Common Issues

**1. "go: command not found"**
```bash
# Add Go to PATH
export PATH=$PATH:/usr/local/go/bin
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc
```

**2. "cannot find package"**
```bash
# Update dependencies
go mod tidy
go mod download

# Clear cache if needed
go clean -modcache
```

**3. "port already in use"**
```bash
# Find process using port
lsof -i :8080  # macOS/Linux
netstat -ano | findstr :8080  # Windows

# Kill process
kill -9 <PID>
```

**4. Docker permission denied**
```bash
# Linux: Add user to docker group
sudo usermod -aG docker $USER
newgrp docker
```

**5. PostgreSQL connection refused**
```bash
# Check if running
brew services list  # macOS
sudo systemctl status postgresql  # Linux

# Start if not running
brew services start postgresql@15
sudo systemctl start postgresql
```

---

**✅ Setup Complete!** You can now start any project in this guide. Reference this section whenever you need to set up a new development environment.

---

# Golang Learning Projects - Basic Level

A comprehensive guide to hands-on Golang projects for beginners. Learn by building practical, useful applications.

---

## Project 1: CLI Todo Application

### Prerequisites & Requirements

**Before Starting:**
- Go installed (version 1.19 or later)
  - Check: `go version`
  - Install: Download from https://golang.org/dl/
- Basic command-line familiarity
  - Navigate directories (cd, ls/dir)
  - Run commands in terminal
- Text editor or IDE
  - VS Code with Go extension (recommended)
  - GoLand, Vim, Emacs, or any editor
- Understanding of:
  - Variables and data types
  - Functions and parameters
  - Basic control flow (if/else, loops)

**Knowledge Prerequisites:**
- **Must Know**:
  - How to declare variables and constants
  - Basic types: int, string, bool
  - How to write and call functions
  - Basic package imports
- **Should Know** (will learn if not):
  - Structs (will be thoroughly explained)
  - Slices vs arrays
  - Error handling with `if err != nil`
  - JSON concepts (objects, arrays)
- **Nice to Have**:
  - Used command-line flags before (like `ls -la`)
  - Read JSON format
  - Basic file operations concepts

**System Requirements:**
- **OS**: macOS, Linux, or Windows
- **Disk Space**: ~50MB for Go installation + project
- **RAM**: 2GB minimum (4GB recommended)
- **Terminal**: Bash, Zsh, PowerShell, or Command Prompt

**Go Concepts You'll Need:**
1. **Packages**: `package main`, imports
2. **Functions**: Basic function syntax
3. **Variables**: `var`, `:=` short declaration
4. **Strings**: String literals, concatenation
5. **Integers**: Basic arithmetic
6. **Booleans**: true/false logic

**External Dependencies:**
- **None!** Uses only Go standard library
- All packages included: `encoding/json`, `flag`, `os`, `time`, `fmt`

**Estimated Time:**
- Setup: 15-30 minutes
- Implementation: 3-6 hours (first time)
- Testing & debugging: 1-2 hours
- **Total**: 5-9 hours

**What to Install:**
```bash
# 1. Install Go
# macOS (using Homebrew)
brew install go

# Linux (Ubuntu/Debian)
sudo apt update
sudo apt install golang-go

# Windows
# Download installer from golang.org

# 2. Verify installation
go version  # Should show version 1.19+

# 3. Check Go environment
go env GOPATH  # Your Go workspace path
go env GOROOT  # Where Go is installed

# 4. (Optional) Install VS Code Go extension
code --install-extension golang.go
```

**Project Setup:**
```bash
# Create project directory
mkdir -p ~/projects/todo-cli
cd ~/projects/todo-cli

# Initialize Go module
go mod init github.com/yourusername/todo-cli

# This creates go.mod file (like package.json for Node.js)
```

**Files You'll Create:**
- `main.go` - 100-150 lines
- `todo.go` - 80-120 lines
- `storage.go` - 40-60 lines
- `go.mod` - Auto-generated
- `todos.json` - Created at runtime

**Common Setup Issues:**
1. **Go not in PATH**: Add Go bin directory to PATH
2. **Module not initialized**: Run `go mod init` first
3. **GOPATH confusion**: Not needed with modules (Go 1.11+)
4. **Permission errors**: Don't use sudo for Go commands

### Overview
Build a command-line todo list manager that persists tasks to a JSON file. This project teaches fundamental Go concepts through a practical tool you can actually use daily.

### What You'll Learn
- **Structs & Methods**: Define custom data types and attach behavior
- **File I/O**: Read from and write to files using `os` and `io/ioutil`
- **JSON Encoding/Decoding**: Marshal and unmarshal data structures
- **Flag Parsing**: Handle command-line arguments with `flag` package
- **Error Handling**: Go's explicit error handling pattern
- **Slices**: Dynamic arrays and slice operations
- **Time Package**: Work with dates and timestamps

### Core Features
1. Add new tasks with description and priority
2. List all tasks (pending/completed)
3. Mark tasks as complete
4. Delete tasks
5. Filter by status or priority
6. Persistent storage in JSON file

### Project Structure
```
todo-cli/
├── main.go           # Entry point and CLI handling
├── todo.go           # Todo struct and methods
├── storage.go        # File operations
├── go.mod            # Module definition
└── todos.json        # Data file (created at runtime)
```

### Implementation Guide

#### Step 1: Initialize the Project
```bash
mkdir todo-cli
cd todo-cli
go mod init github.com/yourusername/todo-cli
```

#### Step 2: Define the Todo Structure (`todo.go`)

**Key Concepts:**
- **Structs**: User-defined types that group related data
- **Tags**: Metadata for struct fields (used for JSON serialization)
- **Methods**: Functions associated with a type

**What you need to create:**
- A `Todo` struct with fields: ID, Title, Description, Completed, Priority, CreatedAt, CompletedAt
  - Use JSON tags for each field
  - CompletedAt should be a pointer to allow null values
- A `TodoList` struct that holds a slice of todos
- Methods on `TodoList`:
  - `Add(title, description, priority)` - Create and add a new todo
  - `Complete(id)` - Mark a todo as done (set Completed=true and CompletedAt)
  - `Delete(id)` - Remove a todo from the slice
  - `GetByID(id)` - Find and return a specific todo
  - `Filter(completed)` - Return only pending or completed todos

**Learning Notes:**
- **Pointer Receivers (`*TodoList`)**: Use when method needs to modify the struct or when struct is large
- **Value Receivers (`TodoList`)**: Use when method only reads data and struct is small
- **Error Handling**: Go returns errors explicitly, no exceptions
- **nil**: Go's zero value for pointers, meaning "no value"
- **Slice Manipulation**: Use `append()` to add, slice tricks like `append(slice[:i], slice[i+1:]...)` to remove

**Hints:**
- To generate unique IDs, loop through existing todos and find max ID + 1
- Use `time.Now()` to get current timestamp
- For Delete, you'll need to reconstruct the slice without the deleted item
- Methods that modify data should use pointer receivers: `func (tl *TodoList) Add(...)`

#### Step 3: Implement Storage (`storage.go`)

**Key Concepts:**
- **JSON Marshaling**: Convert Go objects to JSON
- **File Operations**: Read/write files safely
- **Error Propagation**: Handling and passing errors up the call stack

**What you need to create:**
- A constant for the data file name (e.g., "todos.json")
- `SaveToFile()` method on `TodoList`:
  - Marshal the TodoList to JSON with indentation
  - Write to file with appropriate permissions (0644)
  - Return errors if anything fails
- `LoadFromFile()` function that returns `(*TodoList, error)`:
  - Check if file exists (use `os.Stat`)
  - If doesn't exist, return empty TodoList
  - Read file contents
  - Unmarshal JSON into TodoList struct
  - Handle all errors appropriately

**Learning Notes:**
- **`json.MarshalIndent()`**: Makes JSON human-readable
- **`os.WriteFile()`**: One-step file writing
- **`os.ReadFile()`**: One-step file reading
- **`%w` Format Verb**: Wraps errors, preserving the error chain
- **File Permissions**: 0644 = owner can read/write, others can only read

**Hints:**
- Use `os.IsNotExist(err)` to check if file doesn't exist
- Wrap errors with context: `fmt.Errorf("error reading file: %w", err)`
- Initialize empty slice: `&TodoList{Todos: []Todo{}}`

#### Step 4: Build the CLI (`main.go`)

**Key Concepts:**
- **Flag Package**: Parse command-line arguments
- **Switch Statements**: Multi-way conditional logic
- **Defer**: Ensure code runs at function exit (cleanup)

**What you need to create:**
- Use `flag.NewFlagSet()` to create separate flag sets for each command:
  - **add**: flags for -title, -desc, -priority
  - **list**: flags for -all, -pending, -completed
  - **complete**: takes ID as argument
  - **delete**: takes ID as argument
- Main function flow:
  1. Check if subcommand provided
  2. Load existing todos from file
  3. Switch on subcommand (add/list/complete/delete)
  4. For each command: parse flags, execute operation, save if modified
- Helper functions:
  - `displayTodos()` - Format and print todos in a table
  - `printUsage()` - Show help information

**Learning Notes:**
- **`flag.NewFlagSet`**: Creates independent flag sets for subcommands
- **`defer`**: Schedules function call to run when surrounding function returns
- **`text/tabwriter`**: Standard library package for aligned text output
- **`strconv.Atoi`**: Convert string to integer

**Hints:**
- Use `tabwriter.NewWriter()` for nice table formatting
- Check `os.Args[1]` for the subcommand name
- Parse flags with `flagSet.Parse(os.Args[2:])`
- Get positional arguments with `flagSet.Arg(0)`
- Always save after modifying todos

#### Step 5: Build and Run

```bash
# Build the application
go build -o todo-cli

# Run examples
./todo-cli add -title "Learn Go" -desc "Complete basic projects" -priority 3
./todo-cli add -title "Buy groceries" -priority 2
./todo-cli list
./todo-cli complete 1
./todo-cli list --pending
./todo-cli delete 2
```

### Challenge Yourself
Once you've built the basic version, try adding:

1. **Edit Command**: Modify existing todos
2. **Search**: Find todos by keyword
3. **Due Dates**: Add deadlines and sort by urgency
4. **Tags/Categories**: Organize todos with labels
5. **Color Output**: Use ANSI colors for priority levels (github.com/fatih/color)
6. **Export**: Generate HTML or markdown reports
7. **Undo**: Keep operation history and reverse last N operations

### Common Gotchas to Watch For

**Problem**: Changes don't persist
**Why**: Forgot to call `SaveToFile()` after modifications
**Fix**: Always save after add/complete/delete operations

**Problem**: "slice bounds out of range"
**Why**: Accessing slice index without checking length
**Fix**: Check `len(slice) > 0` before accessing, or use range loops

**Problem**: JSON file gets corrupted
**Why**: Crash or error during write
**Fix**: Write to temporary file first, then rename (atomic operation):
```go
tmpFile := dataFile + ".tmp"
os.WriteFile(tmpFile, data, 0644)
os.Rename(tmpFile, dataFile)
```

**Problem**: Can't find todo by ID
**Why**: ID generation creates duplicates or IDs don't match
**Fix**: Use consistent ID generation (max ID + 1)

---

## Project 2: URL Shortener Service

### Prerequisites & Requirements

**Before Starting:**
- **Completed**: Project 1 (Todo CLI) or equivalent Go experience
- Go installed (version 1.19+)
- Basic HTTP/web concepts
  - What is a URL
  - HTTP methods (GET, POST)
  - Status codes (200, 404, 500)
  - JSON format
- Web browser for testing
- Tool for API testing:
  - curl (command-line)
  - Postman (GUI)
  - HTTPie (command-line, user-friendly)

**Knowledge Prerequisites:**
- **Must Know**:
  - Everything from Project 1
  - Structs and methods
  - Maps (Go's hash table): `map[string]string`
  - Pointers and why they matter
  - JSON marshaling/unmarshaling
- **Should Know**:
  - What a web server does
  - Client-server architecture
  - What an API is
  - HTTP request/response cycle
- **Will Learn**:
  - `net/http` package
  - HTTP handlers
  - Routing
  - Concurrency with mutexes
  - Hash functions

**New Go Concepts:**
1. **HTTP Server**: `http.ListenAndServe()`
2. **Handlers**: Functions that handle HTTP requests
3. **Maps**: Key-value storage
4. **Mutexes**: `sync.RWMutex` for thread safety
5. **Goroutines**: Background execution (basic)
6. **Interfaces**: `http.Handler` interface
7. **Methods on Structs**: More advanced usage

**External Dependencies:**
- **None required** - Can use standard library only
- **Optional enhancements**:
  - `github.com/gorilla/mux` - Better routing (install: `go get github.com/gorilla/mux`)
  - `github.com/rs/cors` - CORS handling

**System Requirements:**
- **OS**: Any (macOS, Linux, Windows)
- **RAM**: 2GB minimum
- **Network**: Port 8080 available (or any unused port)
- **Browser**: Any modern browser (Chrome, Firefox, Safari)

**Tools You'll Need:**
```bash
# 1. curl (testing API endpoints)
# macOS/Linux - usually pre-installed
curl --version

# Windows - Install via Chocolatey
choco install curl

# Or use Windows native: Invoke-WebRequest in PowerShell

# 2. (Optional) httpie - user-friendly curl alternative
pip install httpie
# Or: brew install httpie

# 3. (Optional) Postman
# Download from: https://www.postman.com/downloads/
```

**Estimated Time:**
- Setup: 15 minutes
- Implementation: 4-8 hours
- Testing & refinement: 2-3 hours
- **Total**: 7-12 hours

**What to Install:**
```bash
# Create project
mkdir url-shortener
cd url-shortener
go mod init github.com/yourusername/url-shortener

# If using gorilla/mux (optional)
go get github.com/gorilla/mux

# Verify web tools
curl --version

# Test Go's HTTP capabilities
go doc net/http
```

**Files You'll Create:**
- `main.go` - 80-120 lines (server setup)
- `shortener.go` - 120-180 lines (core logic)
- `handlers.go` - 150-200 lines (HTTP handlers)
- `templates/index.html` - 100-150 lines (web UI)
- `go.mod` - Auto-managed

**Skills Built on Project 1:**
- Structs → More complex structs with methods
- Maps → Thread-safe maps with mutexes
- JSON → HTTP JSON APIs
- Error handling → HTTP error responses
- File I/O → Optional persistence

**New Challenges:**
- **Concurrency**: Multiple users accessing simultaneously
- **Thread Safety**: Protecting shared data with mutexes
- **HTTP Protocol**: Request/response handling
- **Hashing**: Generate short codes from URLs
- **State Management**: In-memory data structure

**Testing Your Setup:**
```bash
# Quick HTTP test
go run -e 'package main; import ("fmt"; "net/http"); func main() { http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) { fmt.Fprintf(w, "Hello") }); http.ListenAndServe(":8080", nil) }' &

# Test it
curl http://localhost:8080
# Should output: Hello

# Kill test server
killall go
```

**Common Setup Issues:**
1. **Port already in use**: Change port or kill process using it
   - macOS/Linux: `lsof -ti:8080 | xargs kill`
   - Windows: `netstat -ano | findstr :8080` then kill PID
2. **Firewall blocking**: Allow Go through firewall
3. **Can't access from browser**: Check http://localhost:8080 not https
4. **CORS errors**: Add CORS headers (explained in project)

### Overview
Build a web service that creates short aliases for long URLs (like bit.ly). This introduces web development concepts, HTTP handling, and basic data structures in Go.

### What You'll Learn
- **net/http Package**: Go's powerful HTTP server and client
- **HTTP Methods**: GET, POST, and RESTful principles
- **Routing**: Map URLs to handler functions
- **JSON APIs**: Build and consume JSON endpoints
- **Maps**: Go's built-in hash table type
- **Concurrency**: Thread-safe data structures with mutexes
- **Base62 Encoding**: Generate short, URL-safe IDs
- **HTML Templates**: Render dynamic web pages

### Core Features
1. Shorten a long URL and get a short code
2. Redirect from short code to original URL
3. View statistics (click count)
4. List all shortened URLs
5. REST API for programmatic access
6. Simple web interface

### Project Structure
```
url-shortener/
├── main.go           # HTTP server and routes
├── shortener.go      # Core shortening logic
├── storage.go        # Data storage (in-memory map)
├── handlers.go       # HTTP handlers
├── templates/        # HTML templates
│   └── index.html
├── go.mod
└── urls.json         # Optional: persistence
```

### Implementation Guide

#### Step 1: Initialize Project
```bash
mkdir url-shortener
cd url-shortener
go mod init github.com/yourusername/url-shortener
```

#### Step 2: Core Data Structures (`shortener.go`)

**Key Concepts:**
- **Maps**: Key-value data structure (`map[KeyType]ValueType`)
- **Mutexes**: Locks for thread-safe access to shared data
- **Base Encoding**: Convert numbers to different bases

**What you need to create:**
- `URLData` struct with fields: ID, OriginalURL, ShortCode, Clicks, CreatedAt
- `URLShortener` struct with:
  - `urls` map: `map[string]*URLData` (shortCode -> URLData)
  - `mu` mutex: `sync.RWMutex` for thread-safe access
- `NewURLShortener()` function that initializes the shortener with empty map
- Methods on `URLShortener`:
  - `Shorten(originalURL)` - Generate short code, store mapping, return code
  - `Resolve(shortCode)` - Look up original URL
  - `IncrementClick(shortCode)` - Thread-safe counter increment
  - `GetStats(shortCode)` - Return URLData for analytics
  - `GetAll()` - Return all shortened URLs
- Helper functions:
  - `generateShortCode(url)` - Hash URL and encode to short string
  - `base62Encode(num)` - Convert number to base62 (0-9, a-z, A-Z)

**Learning Notes:**
- **`sync.RWMutex`**: Allows multiple readers OR one writer (not both)
- **`defer`**: Unlocking with defer ensures mutex is released even if function panics
- **Maps**: Not thread-safe by default, need protection for concurrent access
- **Hash Functions**: MD5 creates fixed-size fingerprint of data

**Hints:**
- Use `us.mu.Lock()` and `defer us.mu.Unlock()` for write operations
- Use `us.mu.RLock()` and `defer us.mu.RUnlock()` for read operations
- For hashing: `crypto/md5` with `encoding/binary` to convert to uint64
- Base62 encoding uses repeated division by 62
- Handle collisions by checking if short code already exists before storing

#### Step 3: HTTP Handlers (`handlers.go`)

**Key Concepts:**
- **HTTP Handlers**: Functions that respond to HTTP requests
- **Request/Response**: Reading input and writing output
- **Status Codes**: HTTP response codes (200, 404, 500, etc.)
- **Content Types**: Tell client what format data is in

**What you need to create:**
- Request/Response structs:
  - `ShortenRequest` with URL field
  - `ShortenResponse` with ShortCode and ShortURL fields
  - `ErrorResponse` with Error field
- Handler methods on `URLShortener`:
  - `homeHandler()` - Serve the HTML template
  - `shortenHandler()` - Accept POST with JSON, validate, shorten, return JSON
  - `redirectHandler()` - Extract short code from URL, lookup, increment clicks, redirect
  - `statsHandler()` - Return JSON stats for a short code
  - `listHandler()` - Return JSON array of all URLs
- Helper functions:
  - `respondWithJSON()` - Set headers, write status code, encode JSON
  - `respondWithError()` - Send error as JSON

**Learning Notes:**
- **`http.ResponseWriter`**: Interface for sending HTTP response
- **`*http.Request`**: Contains all info about incoming request
- **`http.StatusXXX`**: Constants for HTTP status codes (200, 404, 500, etc.)
- **`json.NewDecoder(r.Body)`**: Parse JSON from request body

**Hints:**
- Check HTTP method: `if r.Method != http.MethodPost { ... }`
- Decode JSON: `json.NewDecoder(r.Body).Decode(&struct)`
- Validate URLs with `strings.HasPrefix()`
- Extract path parts: `strings.TrimPrefix(r.URL.Path, "/s/")`
- Redirect: `http.Redirect(w, r, url, http.StatusFound)`
- Set JSON header: `w.Header().Set("Content-Type", "application/json")`

#### Step 4: HTML Template (`templates/index.html`)

**What you need to create:**
Create a simple HTML page with:
- Form with URL input field
- Submit button
- Result div to show shortened URL
- JavaScript to:
  - Prevent form default submission
  - POST to `/api/shorten` with fetch API
  - Display result or error
  - Copy to clipboard functionality

**Example structure:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>URL Shortener</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
            background: #f5f5f5;
        }
        .container {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        h1 {
            color: #333;
            margin-bottom: 30px;
        }
        input[type="url"] {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
            box-sizing: border-box;
        }
        button {
            width: 100%;
            padding: 12px;
            background: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            margin-top: 10px;
        }
        button:hover {
            background: #0056b3;
        }
        #result {
            margin-top: 20px;
            padding: 15px;
            background: #e8f5e9;
            border-radius: 5px;
            display: none;
        }
        #shortUrl {
            color: #007bff;
            font-weight: bold;
            word-break: break-all;
        }
        .error {
            background: #ffebee !important;
            color: #c62828;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🔗 URL Shortener</h1>
        <form id="shortenForm">
            <input
                type="url"
                id="urlInput"
                placeholder="Enter a long URL to shorten..."
                required
            >
            <button type="submit">Shorten URL</button>
        </form>
        <div id="result"></div>
    </div>

    <script>
        document.getElementById('shortenForm').addEventListener('submit', async (e) => {
            e.preventDefault();

            const url = document.getElementById('urlInput').value;
            const resultDiv = document.getElementById('result');

            try {
                const response = await fetch('/api/shorten', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({ url: url })
                });

                const data = await response.json();

                if (response.ok) {
                    resultDiv.className = '';
                    resultDiv.innerHTML = `
                        <strong>Short URL created!</strong><br>
                        <a href="${data.short_url}" target="_blank" id="shortUrl">${data.short_url}</a>
                        <br><br>
                        <button onclick="copyToClipboard('${data.short_url}')">Copy to Clipboard</button>
                    `;
                    resultDiv.style.display = 'block';
                } else {
                    throw new Error(data.error || 'Something went wrong');
                }
            } catch (error) {
                resultDiv.className = 'error';
                resultDiv.textContent = error.message;
                resultDiv.style.display = 'block';
            }
        });

        function copyToClipboard(text) {
            navigator.clipboard.writeText(text).then(() => {
                alert('Copied to clipboard!');
            });
        }
    </script>
</body>
</html>
```

#### Step 5: Main Server (`main.go`)

**Key Concepts:**
- **HTTP Server**: Start and configure a web server
- **Routing**: Map URL patterns to handlers
- **Middleware**: Functions that wrap handlers (logging, auth, etc.)

**What you need to create:**
- Main function that:
  - Creates a `URLShortener` instance
  - Creates `http.ServeMux` for routing
  - Registers all handler functions:
    - `/` -> homeHandler
    - `/api/shorten` -> shortenHandler
    - `/api/list` -> listHandler
    - `/s/` -> redirectHandler (handles /s/anything)
    - `/stats/` -> statsHandler
  - Wraps mux with logging middleware
  - Starts server on port 8080
- Middleware function:
  - `loggingMiddleware()` - Logs each request, then calls next handler

**Learning Notes:**
- **`http.ServeMux`**: Request router, matches URLs to handlers
- **`http.ListenAndServe(":8080", handler)`**: Starts server, blocks until error
- **Middleware Pattern**: Wrap handlers to add functionality (logging, auth, etc.)
- **`http.Handler` Interface**: Any type with `ServeHTTP(ResponseWriter, *Request)` method

**Hints:**
- Register routes: `mux.HandleFunc("/path", handler)`
- Middleware wraps handler: return `http.HandlerFunc(func(w, r) { /* log */ next.ServeHTTP(w, r) })`
- Methods on structs can be used as handlers: `shortener.homeHandler`

#### Step 6: Run the Server

```bash
# Create templates directory
mkdir templates

# Copy the HTML template to templates/index.html
# (use the HTML code from Step 4)

# Run the server
go run .

# Test with curl
curl -X POST http://localhost:8080/api/shorten \
  -H "Content-Type: application/json" \
  -d '{"url":"https://www.golang.org/doc/"}'

# Or open http://localhost:8080 in your browser
```

### Testing the API

```bash
# Shorten a URL
curl -X POST http://localhost:8080/api/shorten \
  -H "Content-Type: application/json" \
  -d '{"url":"https://github.com/golang/go"}'
# Response: {"short_code":"abc123","short_url":"http://localhost:8080/s/abc123"}

# Visit the short URL (redirects)
curl -L http://localhost:8080/s/abc123

# Get statistics
curl http://localhost:8080/stats/abc123
# Response: {"id":"abc123","original_url":"https://github.com/golang/go","short_code":"abc123","clicks":1,"created_at":"..."}

# List all URLs
curl http://localhost:8080/api/list
```

### Enhancement Ideas

1. **Custom Short Codes**: Allow users to specify their own short codes
2. **Expiration**: Auto-delete URLs after certain time
3. **QR Codes**: Generate QR codes for short URLs
4. **Analytics**: Track referrers, user agents, geographic data
5. **Authentication**: User accounts and private URLs
6. **Database**: Use PostgreSQL or Redis instead of in-memory map
7. **Rate Limiting**: Prevent abuse with request throttling
8. **URL Validation**: Check if URLs are reachable before shortening

### Common Gotchas & Solutions

**Problem**: Race conditions with map access
**Solution**: Always use mutex locks (RLock for reads, Lock for writes)

**Problem**: Lost data when server restarts
**Solution**: Implement persistence (save to JSON file periodically or use database)

```go
// Add to URLShortener
func (us *URLShortener) SaveToFile(filename string) error {
    us.mu.RLock()
    defer us.mu.RUnlock()

    data, err := json.MarshalIndent(us.urls, "", "  ")
    if err != nil {
        return err
    }

    return os.WriteFile(filename, data, 0644)
}
```

**Problem**: Short codes collide
**Solution**: Already handled in `Shorten()` method with collision detection

---

## Project 3: File Organizer

### Prerequisites & Requirements

**Before Starting:**
- **Completed**: Projects 1 & 2, or equivalent experience
- Solid understanding of:
  - Goroutines and channels
  - File system concepts (files, directories, paths)
  - Concurrent programming basics
- Comfortable with command-line operations
- Basic regex knowledge helpful (not required)

**Knowledge Prerequisites:**
- **Must Know**:
  - All concepts from Projects 1 & 2
  - Goroutines: `go func() { ... }()`
  - Channels: `make(chan type)`, `<-channel`
  - Select statements: `select { case <-ch1: ... }`
  - File operations: create, move, delete
  - Paths: absolute vs relative
- **Should Know**:
  - What file watching means
  - File extensions and MIME types
  - Regular expressions basics
  - Signals (SIGINT, SIGTERM)
- **Will Learn**:
  - File system watching with fsnotify
  - Complex concurrent patterns
  - Signal handling
  - Configuration files
  - Advanced file operations

**New Go Concepts:**
1. **Channels**: Communication between goroutines
2. **Select**: Multiplexing channel operations
3. **Signals**: `os/signal` package
4. **Context**: Cancellation and timeouts
5. **Filepath**: Cross-platform path handling
6. **Regex**: `regexp` package
7. **YAML/JSON Config**: Configuration parsing

**External Dependencies:**
- **Required**:
  - `github.com/fsnotify/fsnotify` - File system watching
    - Cross-platform file system notifications
    - Install: `go get github.com/fsnotify/fsnotify`
- **Optional**:
  - `gopkg.in/yaml.v3` - YAML config files
  - `github.com/spf13/cobra` - Better CLI
  - `github.com/spf13/viper` - Configuration management

**System Requirements:**
- **OS**: macOS, Linux, or Windows
  - File watching APIs differ per OS (fsnotify handles this)
- **RAM**: 2GB minimum (4GB recommended)
- **Disk Space**: Depends on files being organized
- **Permissions**: Write access to target directories
- **Test Directory**: A folder with files to organize (Downloads, etc.)

**Platform-Specific Notes:**
- **macOS**: Uses FSEvents API
- **Linux**: Uses inotify
- **Windows**: Uses ReadDirectoryChangesW
- All handled by fsnotify transparently

**What to Install:**
```bash
# Create project
mkdir file-organizer
cd file-organizer
go mod init github.com/yourusername/file-organizer

# Install fsnotify (required)
go get github.com/fsnotify/fsnotify

# Verify installation
go list -m github.com/fsnotify/fsnotify

# Optional: CLI framework
go get github.com/spf13/cobra

# Optional: Configuration
go get github.com/spf13/viper
go get gopkg.in/yaml.v3
```

**Estimated Time:**
- Setup: 20-30 minutes
- Core implementation: 6-10 hours
- File watching: 2-4 hours
- Testing: 2-3 hours
- Configuration: 1-2 hours
- **Total**: 12-20 hours

**Files You'll Create:**
- `main.go` - 100-150 lines
- `watcher.go` - 100-150 lines
- `organizer.go` - 150-250 lines
- `rules.go` - 80-120 lines
- `config.go` - 60-100 lines
- `config.yaml` - Configuration file
- `go.mod`, `go.sum` - Dependency management

**Concepts Building on Previous Projects:**
- **Structs** → More complex, nested structs
- **Methods** → Advanced method patterns
- **Error Handling** → Graceful degradation
- **Concurrency** → Multiple goroutines, channels, select
- **File I/O** → Moving, watching, organizing
- **CLI** → More sophisticated command-line interface

**New Challenges:**
- **Concurrency Patterns**: Producer-consumer, worker pools
- **Event Handling**: React to file system events
- **Debouncing**: Handle rapid repeated events
- **Signal Handling**: Graceful shutdown on Ctrl+C
- **File Safety**: Atomic operations, conflict resolution
- **Cross-Platform**: Code works on all OS

**Testing Your Setup:**
```bash
# Test fsnotify installation
cat > test_watch.go << 'EOF'
package main
import (
    "log"
    "github.com/fsnotify/fsnotify"
)
func main() {
    watcher, err := fsnotify.NewWatcher()
    if err != nil {
        log.Fatal(err)
    }
    defer watcher.Close()
    log.Println("fsnotify working!")
}
EOF

go run test_watch.go
# Should output: "fsnotify working!"

rm test_watch.go
```

**Create Test Environment:**
```bash
# Create test directory with sample files
mkdir ~/test-organize
cd ~/test-organize

# Create sample files
touch image1.jpg image2.png
touch document1.pdf document2.txt
touch video1.mp4 archive1.zip
touch song1.mp3 code1.go

# This will be your test directory
```

**Safety Considerations:**
- **Backup Important Files**: Test on non-critical files first
- **Dry-Run Mode**: Implement preview mode before actual moves
- **Undo Feature**: Track operations for reversal
- **Don't Organize System Folders**: Exclude /System, /Windows, etc.
- **Hidden Files**: Skip files starting with `.` by default
- **Permissions**: Check write permissions before moving

**Common Setup Issues:**
1. **fsnotify install fails**:
   - Check Go version (need 1.16+)
   - Run `go mod tidy`
2. **File watching doesn't work**:
   - Check directory exists
   - Verify read permissions
   - Some network drives may not support watching
3. **Permission denied errors**:
   - Don't run as root/admin unless necessary
   - Check folder permissions
4. **Too many open files** (macOS/Linux):
   - Increase limit: `ulimit -n 10000`
5. **Events firing twice**:
   - Normal on some systems (editors create temp files)
   - Implement debouncing

**Performance Considerations:**
- Watching many files: Use limits or selective watching
- Large directories: Consider scanning in batches
- Network drives: May have delays or not support watching
- SSD vs HDD: File operations much faster on SSD

### Overview
Build a tool that watches a directory (like Downloads) and automatically organizes files into subdirectories based on file type, date, or custom rules. This teaches file system operations, path manipulation, and goroutines.

### What You'll Learn
- **filepath Package**: Cross-platform path operations
- **os Package**: File system operations (move, copy, stat)
- **File Watching**: Monitor directory for changes (using fsnotify)
- **Goroutines**: Lightweight threads for concurrent operations
- **Channels**: Communication between goroutines
- **Select Statement**: Multiplex channel operations
- **Regular Expressions**: Pattern matching for file rules
- **Configuration**: Load rules from config file (YAML/JSON)

### Core Features
1. Watch a directory for new files
2. Organize files by extension (images/, documents/, videos/, etc.)
3. Organize by date (2024/12/, 2025/01/, etc.)
4. Custom rules based on filename patterns
5. Dry-run mode to preview changes
6. Undo recent operations
7. Configuration file for custom rules

### Project Structure
```
file-organizer/
├── main.go           # Entry point and CLI
├── watcher.go        # File system watching
├── organizer.go      # Organization logic
├── rules.go          # Rule definitions and matching
├── config.go         # Configuration loading
├── config.yaml       # User configuration
└── go.mod
```

### Detailed Implementation Guide

#### Step 1: Initialize and Install Dependencies

```bash
mkdir file-organizer
cd file-organizer
go mod init github.com/yourusername/file-organizer

# Install file watching library
go get github.com/fsnotify/fsnotify
```

#### Step 2: Define Rules (`rules.go`)

**Key Concepts:**
- **Type Definitions**: Create custom types for clarity
- **Regular Expressions**: Pattern matching with `regexp` package
- **String Operations**: Manipulating file paths and names

**What you need to create:**
- `Rule` struct with fields:
  - Name (e.g., "Images")
  - Extensions (slice of strings like [".jpg", ".png"])
  - Pattern (optional regex for filename matching)
  - Destination (target folder name)
- `RuleSet` struct:
  - Rules (slice of Rule)
- `DefaultRules()` function that returns a RuleSet with common categories:
  - Images (.jpg, .png, .gif, etc.)
  - Documents (.pdf, .doc, .txt, etc.)
  - Videos, Audio, Archives, Code, Executables, etc.
- Methods on `RuleSet`:
  - `MatchRule(filename)` - Find first matching rule, return (destination, found)
  - `AddCustomRule(rule)` - Add user-defined rule

**Learning Notes:**
- **YAML Tags**: Similar to JSON tags, used by YAML parser (if you add config file support)
- **`filepath.Ext()`**: Extracts file extension including the dot
- **`strings.ToLower()`**: Case-insensitive matching
- **`regexp.MatchString()`**: Quick regex match without pre-compiling

**Hints:**
- Loop through rules, check if file extension matches any in rule.Extensions
- Use `filepath.Ext(filename)` to get extension
- Compare extensions case-insensitively
- If no extension matches, try pattern matching with regex
- Return empty string and false if no match found

#### Step 3: File Operations (`organizer.go`)

**Key Concepts:**
- **File Operations**: Moving, copying, and checking files
- **Error Handling**: Robust error checking for file operations
- **Atomic Operations**: Ensuring operations complete fully or not at all

**What you need to create:**
- `Operation` struct for undo tracking:
  - SourcePath, DestPath, Timestamp
- `Organizer` struct with:
  - WatchDir (directory to organize)
  - Rules (pointer to RuleSet)
  - DryRun (bool for preview mode)
  - History (slice of Operations)
- `NewOrganizer()` constructor function
- Methods on `Organizer`:
  - `OrganizeFile(filePath)` - Main logic:
    - Get file info, skip if directory or hidden
    - Match against rules to get destination
    - Build destination path
    - Handle dry-run mode (just print, don't move)
    - Create destination folder if needed
    - Handle filename conflicts
    - Move file with os.Rename
    - Record operation in History
  - `resolveConflict(path)` - If file exists, append (1), (2), etc.
  - `OrganizeAll()` - Process all files in watch directory
  - `Undo(count)` - Reverse last N operations

**Learning Notes:**
- **`os.Stat()`**: Get file information (returns FileInfo with IsDir(), Size(), ModTime())
- **`os.IsNotExist(err)`**: Check if error is "file does not exist"
- **`os.MkdirAll()`**: Create directory and all parents (like `mkdir -p`)
- **`os.Rename()`**: Move/rename files (atomic on same filesystem)
- **`os.ReadDir()`**: List directory contents

**Hints:**
- Use `filepath.Base()` to get filename from full path
- Skip hidden files: check if `filename[0] == '.'`
- If no rule matches, use default destination like "Other"
- Check if file already in correct location before moving
- For conflicts: loop with counter, check `file (1).ext`, `file (2).ext`, etc.
- Split filename: `filepath.Ext()` for extension, `strings.TrimSuffix()` for name part

#### Step 4: File Watching (`watcher.go`)

**Key Concepts:**
- **Goroutines**: Lightweight concurrent execution
- **Channels**: Type-safe communication between goroutines
- **Select Statement**: Wait on multiple channel operations
- **File System Events**: React to file system changes

**What you need to create:**
- Install dependency: `go get github.com/fsnotify/fsnotify`
- `Watcher` struct with:
  - organizer (pointer to Organizer)
  - watcher (pointer to fsnotify.Watcher)
  - done (channel for shutdown signal: `chan bool`)
- `NewWatcher(organizer)` constructor that creates fsnotify watcher
- Methods:
  - `Start()` - Add directory to watcher, launch event loop goroutine
  - `eventLoop()` - Runs in goroutine:
    - Use `select` to multiplex channels
    - Listen to `watcher.Events` for file system changes
    - Listen to `watcher.Errors` for errors
    - Listen to `done` channel for shutdown
    - On CREATE or WRITE events: organize the file
    - Add debouncing (wait 500ms before processing)
  - `Stop()` - Close channels and stop watching

**Learning Notes:**
- **`go func() { ... }()`**: Launch anonymous function in goroutine
- **`select { case ... }`**: Like switch but for channel operations (blocks until one is ready)
- **`<-channel`**: Receive from channel (blocks until data available)
- **`close(channel)`**: Close channel, signals receivers no more data coming
- **Debouncing**: Delay processing to handle rapid file changes (copy operations)

**Hints:**
- Create watcher: `fsnotify.NewWatcher()`
- Add directory: `watcher.Add(path)`
- Check event type: `event.Op & fsnotify.Create == fsnotify.Create`
- Use timer: `time.NewTimer()` and `timer.Reset()` for debouncing
- Launch processing in separate goroutine to avoid blocking event loop
- Check channel closed: `value, ok := <-channel` (ok is false if closed)

#### Step 5: Configuration (`config.go`)

**What you need to create:**
- `Config` struct with:
  - WatchDirectory (string)
  - Rules (pointer to RuleSet)
- `LoadConfig(filename)` function:
  - Check if file exists
  - If not, return default config (~/Downloads, DefaultRules)
  - If exists, read and unmarshal JSON
- `SaveConfig(filename, config)` function:
  - Marshal config to JSON with indentation
  - Write to file

**Hints:**
- Use `os.UserHomeDir()` to get home directory
- Use same JSON patterns from todo app
- Return default config if file doesn't exist (not an error)

#### Step 6: Main Application (`main.go`)

**What you need to create:**
- Define command-line flags:
  - `-dir`: Directory to watch
  - `-dry-run`: Preview mode (bool)
  - `-organize`: Run once and exit (bool)
  - `-watch`: Watch continuously (bool)
  - `-undo`: Undo last N operations (int)
  - `-config`: Config file path (string)
- Main flow:
  1. Parse flags
  2. Load config from file
  3. Override config with flags if provided
  4. Expand `~/` in paths to full home directory path
  5. Create organizer instance
  6. Handle different modes (undo, organize, watch)
  7. For watch mode: wait for Ctrl+C signal before stopping

**Learning Notes:**
- **`flag.String()`, `flag.Bool()`, `flag.Int()`**: Define flags, returns pointer to value
- **`flag.Parse()`**: Parse command-line arguments
- **`signal.Notify()`**: Register to receive OS signals
- **`<-channel`**: Block until signal received

**Hints:**
- Access flag values: `*flagName` (flags return pointers)
- Expand home: check if path starts with `~/`, use `os.UserHomeDir()`
- For watch mode: create channel, use `signal.Notify()`, block on channel
- Handle signals: `os.Interrupt` (Ctrl+C), `syscall.SIGTERM`
- If no mode flag, print usage with `flag.PrintDefaults()`

#### Step 7: Build and Use

```bash
# Build
go build -o file-organizer

# Organize Downloads folder once
./file-organizer -dir ~/Downloads -organize

# Preview changes (dry-run)
./file-organizer -dir ~/Downloads -organize -dry-run

# Watch directory continuously
./file-organizer -dir ~/Downloads -watch

# Undo last 3 operations
./file-organizer -dir ~/Downloads -undo 3
```

### Enhancement Ideas

1. **Date-based Organization**: Group by year/month
2. **Size Filters**: Handle large files differently
3. **Duplicate Detection**: Find and merge duplicate files (by hash)
4. **Cloud Sync**: Upload organized files to cloud storage
5. **GUI**: Build a desktop interface with fyne or webview
6. **Smart Rules**: ML-based file categorization
7. **Compression**: Auto-compress old files

### Common Gotchas

**Problem**: Watcher triggers for own moves
**Solution**: Keep track of recently moved files and ignore them

**Problem**: Permission errors
**Solution**: Check permissions before operations, provide clear error messages

**Problem**: Infinite loops with symbolic links
**Solution**: Check for symlinks and handle appropriately

---

## Project 4: System Process Monitor

### Prerequisites & Requirements

**Before Starting:**
- **Completed**: All 3 basic projects OR
- **Equivalent Experience**:
  - File I/O in Go
  - Basic understanding of processes
  - Command-line interfaces

**Knowledge Prerequisites:**
- **Must Know**:
  - Basic Go syntax
  - File reading (`os.ReadFile`, `bufio.Scanner`)
  - String parsing (`strings.Split`, `strconv`)
  - Goroutines basics
  - Time and duration
- **Should Know**:
  - Process concepts (PID, CPU, memory)
  - Operating system basics
  - Signal handling
- **Will Learn**:
  - `/proc` filesystem (Linux)
  - `ps` command internals
  - Process information gathering
  - Cross-platform process APIs
  - Real-time monitoring
  - Terminal UI basics

**New Go Concepts:**
1. **os.Process**: Process management
2. **os.FindProcess**: Find running process
3. **syscall.Getrusage**: Resource usage (Linux/macOS)
4. **time.Ticker**: Periodic updates
5. **Signal Handling**: os/signal package
6. **Cross-platform builds**: Build tags

**External Dependencies:**
- **Required**:
  - `github.com/shirou/gopsutil/v3` - Cross-platform system info
- **Optional**:
  - `github.com/gizak/termui/v3` - Terminal UI
  - `github.com/nsf/termbox-go` - Alternative terminal UI

**System Requirements:**
- **OS**: Linux, macOS, Windows, BSD (cross-platform)
- **RAM**: 512MB minimum
- **Tools**: Standard terminal

**What to Install:**
```bash
mkdir process-monitor
cd process-monitor
go mod init github.com/yourusername/process-monitor

# Cross-platform system info
go get github.com/shirou/gopsutil/v3/process
go get github.com/shirou/gopsutil/v3/cpu
go get github.com/shirou/gopsutil/v3/mem

# Optional: Terminal UI
go get github.com/gizak/termui/v3

go mod tidy
```

**Testing:**
```bash
# Test gopsutil
cat > test_gopsutil.go << 'EOF'
package main
import (
    "fmt"
    "github.com/shirou/gopsutil/v3/process"
)
func main() {
    procs, _ := process.Processes()
    fmt.Printf("Found %d processes\n", len(procs))
    for i, p := range procs[:5] {
        name, _ := p.Name()
        fmt.Printf("%d. PID %d: %s\n", i+1, p.Pid, name)
    }
}
EOF

go run test_gopsutil.go
rm test_gopsutil.go
```

**Estimated Time:**
- Setup: 30 minutes
- List processes: 2-3 hours
- Process details (CPU, memory): 3-4 hours
- Sorting and filtering: 2-3 hours
- Real-time monitoring: 3-4 hours
- Terminal UI: 4-6 hours
- **Total**: 15-20 hours

**Files You'll Create:**
- `main.go` - 100-150 lines
- `monitor/process.go` - 150-250 lines
- `monitor/system.go` - 100-150 lines
- `ui/display.go` - 150-250 lines
- `utils/format.go` - 80-120 lines

### Overview
Build a cross-platform system process monitor (like `top` or Task Manager) that displays running processes with CPU, memory usage, and allows sorting/filtering. Learn to interact with OS process APIs and `/proc` filesystem.

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

### Project Structure
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

### Implementation Guide

#### Step 1: List Processes

**Key Concepts:**
- **gopsutil**: Cross-platform system/process library
- **Process struct**: PID, name, status, CPU, memory
- **Iteration**: Loop through all processes

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

#### Step 2: Display Process Table

**What to create:**
- Table formatter with columns
- Header row
- Data rows with alignment
- Color coding (optional)

**Hints:**
- Use `fmt.Sprintf()` for formatting
- Right-align numbers, left-align text
- `\r` to overwrite current line for live updates

#### Step 3: Sorting and Filtering

**What to create:**
- Sort by different fields
- Filter by name, user, or threshold
- Command-line flags for options

**Hints:**
- Use `sort.Slice()` with custom comparison
- `strings.Contains()` for name filtering
- Parse flags with `flag` package

#### Step 4: Real-time Monitoring

**What to create:**
- Refresh display every second
- Clear screen and redraw
- Handle Ctrl+C gracefully

**Hints:**
- `time.Ticker` for periodic updates
- `os/signal` to catch interrupts
- `\033[2J\033[H` to clear terminal (ANSI codes)

### Challenge Yourself

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

### Common Gotchas

**Problem**: Permission denied accessing some processes
**Fix**: Normal behavior, skip inaccessible processes or run with elevated privileges

**Problem**: CPU percentage over 100%
**Fix**: Multi-core systems can show >100% (per-core usage), divide by CPU count

**Problem**: Slow updates
**Fix**: Cache process info, only update changed processes

---

## Project 5: Log File Analyzer & Tail

### Prerequisites & Requirements

**Before Starting:**
- **Completed**: Basic projects
- **Equivalent Experience**: File I/O, string parsing

**Knowledge Prerequisites:**
- **Must Know**:
  - File reading (`os.Open`, `bufio.Scanner`)
  - Regular expressions (`regexp`)
  - String manipulation
  - Maps and slices
- **Should Know**:
  - Log formats (Apache, nginx, syslog)
  - File watching concepts
  - Text parsing patterns
- **Will Learn**:
  - File tailing (`tail -f` implementation)
  - Log parsing and analysis
  - Pattern matching with regex
  - Statistics calculation
  - File watching without fsnotify

**New Go Concepts:**
1. **File Seeking**: `file.Seek()` for reading from end
2. **io.SeekEnd**: Positioning file pointer
3. **bufio.Scanner**: Efficient line reading
4. **regexp.Compile**: Pattern matching
5. **time.ParseInLayout**: Parse log timestamps

**What to Install:**
```bash
mkdir log-analyzer
cd log-analyzer
go mod init github.com/yourusername/log-analyzer

# No external dependencies needed for basic version
# Optional: regex2 for advanced regex
go get github.com/dlclark/regexp2
```

**Estimated Time:**
- Setup: 30 minutes
- File reading: 1-2 hours
- Log parsing: 3-4 hours
- Statistics: 2-3 hours
- Tail functionality: 3-4 hours
- Filtering: 2-3 hours
- **Total**: 12-18 hours

**Files You'll Create:**
- `main.go` - 150-200 lines
- `parser/parser.go` - 200-300 lines
- `analyzer/stats.go` - 150-250 lines
- `tail/tail.go` - 150-200 lines
- `filter/filter.go` - 100-150 lines

### Overview
Build a log file analyzer and real-time tail utility that parses logs, extracts statistics, and follows files like `tail -f`. Learn file I/O, seeking, pattern matching, and log analysis.

### What You'll Learn
- **File Seeking**: Read from end of file
- **Log Parsing**: Extract structured data from logs
- **Regular Expressions**: Pattern matching
- **Statistics**: Count, aggregate, summarize
- **File Watching**: Detect new content without fsnotify
- **Real-time Processing**: Stream processing

### Core Features
1. Parse common log formats (Apache, nginx, JSON)
2. Extract fields (IP, timestamp, status, URL)
3. Calculate statistics (requests/sec, error rate, top IPs)
4. Filter by patterns, date range, status codes
5. Tail mode (`-f` flag) for real-time monitoring
6. Highlight errors/warnings
7. Export analysis to JSON/CSV

### Implementation Guide

#### Step 1: Basic File Reading

**What to create:**
```go
func ReadLogFile(path string) ([]string, error) {
    // Read entire file line by line
    // Return slice of lines
}
```

#### Step 2: Log Parsing

**Key Concepts:**
- **Apache Combined Log**: `127.0.0.1 - - [01/Jan/2024:00:00:00 +0000] "GET /path HTTP/1.1" 200 1234`
- **Regex patterns** for extraction
- **Timestamp parsing**

**What to create:**
```go
type LogEntry struct {
    IP        string
    Timestamp time.Time
    Method    string
    Path      string
    Status    int
    Size      int
    UserAgent string
}

func ParseApacheLog(line string) (*LogEntry, error) {
    // Use regex to extract fields
}
```

#### Step 3: Statistics

**What to calculate:**
- Total requests
- Requests per status code
- Top N IPs
- Top N URLs
- Error rate percentage
- Average response size
- Requests per hour/day

#### Step 4: Tail Implementation

**Key Concepts:**
- Start reading from end of file
- Periodically check for new content
- Only read new lines

**What to create:**
```go
func TailFile(path string, follow bool) {
    file, _ := os.Open(path)
    // Seek to end
    file.Seek(0, io.SeekEnd)

    for {
        // Read new lines
        // If no new lines, sleep
        time.Sleep(100 * time.Millisecond)
    }
}
```

### Challenge Yourself

1. **Multiple Formats**: Support nginx, JSON, syslog formats
2. **GeoIP**: Lookup IP locations
3. **Alerts**: Alert on error rate thresholds
4. **Web Dashboard**: Real-time web UI
5. **Multiple Files**: Tail multiple files simultaneously
6. **Log Rotation**: Handle rotated log files
7. **Compression**: Read gzipped logs
8. **Search**: Full-text search across logs

### Common Gotchas

**Problem**: Memory issues with large files
**Fix**: Read in chunks, don't load entire file into memory

**Problem**: Tail doesn't see new lines
**Fix**: Ensure you're checking file size, handle log rotation

**Problem**: Regex performance
**Fix**: Compile regex once, reuse; or use string operations if possible

---

## Project 6: System Resource Monitor (Cross-platform)

### Prerequisites & Requirements

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

### Overview
Build a system resource monitor showing CPU, memory, disk, and network usage. Cross-platform using gopsutil. Learn to read system information from various OS APIs.

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

### Challenge Yourself
1. Web dashboard with graphs
2. Historical data storage (time-series DB)
3. Alerts on thresholds
4. Compare with system tools (`top`, `htop`, `iostat`)
5. Battery status (laptops)
6. GPU usage (NVIDIA/AMD)

---

# Golang Learning Projects - Intermediate Level

Projects that build on the basics and introduce more complex patterns, external dependencies, and real-world architectures.

---

## Project 1: REST API with Database

### Prerequisites & Requirements

**Before Starting:**
- **Completed**: All 3 basic projects OR
- **Equivalent Experience**:
  - Built HTTP servers in Go
  - Worked with databases (any language)
  - Understand REST API principles
  - Comfortable with concurrent programming

**Knowledge Prerequisites:**
- **Must Know**:
  - HTTP methods and status codes
  - JSON encoding/decoding
  - Structs, interfaces, methods
  - Goroutines and mutexes
  - Error handling patterns
  - SQL basics (SELECT, INSERT, UPDATE, DELETE)
- **Should Know**:
  - REST API design principles
  - Database normalization
  - Authentication concepts (tokens, sessions)
  - CRUD operations
  - API testing
- **Will Learn**:
  - `database/sql` package
  - JWT authentication
  - Middleware patterns
  - Request validation
  - Database migrations
  - Production API structure

**New Go Concepts:**
1. **Database/SQL**: Standard database interface
2. **SQL Drivers**: PostgreSQL/SQLite drivers
3. **Context**: Request-scoped values and cancellation
4. **JWT**: JSON Web Tokens for authentication
5. **Validators**: Struct validation with tags
6. **Middleware**: Request/response interceptors
7. **Environment Variables**: Configuration management ([12-Factor: III. Config](https://12factor.net/config))

**External Dependencies:**
- **Required**:
  - `github.com/gorilla/mux` - HTTP router with better features
  - `github.com/lib/pq` - PostgreSQL driver OR `github.com/mattn/go-sqlite3` - SQLite driver
  - `github.com/golang-jwt/jwt/v5` - JWT tokens
  - `github.com/joho/godotenv` - Load .env files
  - `golang.org/x/crypto/bcrypt` - Password hashing
  - `github.com/go-playground/validator/v10` - Input validation

**System Requirements:**
- **OS**: macOS, Linux, Windows
- **RAM**: 4GB minimum (8GB recommended)
- **Database**:
  - **Option 1 - PostgreSQL** (recommended for production-like experience):
    - Version 12 or later
    - ~100MB disk space
  - **Option 2 - SQLite** (simpler, single-file database):
    - No separate installation needed
    - Good for learning, not production
- **Tools**:
  - API testing client (Postman, Insomnia, or curl)
  - Database client (optional but helpful)

**Database Installation:**

**PostgreSQL Setup:**
```bash
# macOS (using Homebrew)
brew install postgresql@15
brew services start postgresql@15

# Verify
psql --version

# Create database and user
psql postgres
CREATE DATABASE blog_db;
CREATE USER blog_user WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE blog_db TO blog_user;
\q

# Test connection
psql -h localhost -U blog_user -d blog_db

# Linux (Ubuntu/Debian)
sudo apt update
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql

# Create user and database
sudo -u postgres psql
CREATE DATABASE blog_db;
CREATE USER blog_user WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE blog_db TO blog_user;
\q

# Windows
# Download installer from:
# https://www.postgresql.org/download/windows/
# Follow installation wizard
# Use pgAdmin (included) to create database
```

**SQLite Setup (Alternative - Easier):**
```bash
# No installation needed!
# SQLite creates database file automatically
# Just install the Go driver:
go get github.com/mattn/go-sqlite3

# Note: On Windows, may need GCC:
# Install MinGW-w64 or TDM-GCC
```

**What to Install:**
```bash
# 1. Create project
mkdir blog-api
cd blog-api
go mod init github.com/yourusername/blog-api

# 2. Install all dependencies
go get github.com/gorilla/mux
go get github.com/lib/pq  # PostgreSQL
# OR
go get github.com/mattn/go-sqlite3  # SQLite

go get github.com/golang-jwt/jwt/v5
go get github.com/joho/godotenv
go get golang.org/x/crypto/bcrypt
go get github.com/go-playground/validator/v10

# 3. Verify dependencies
go mod tidy
go mod download
cat go.mod  # Check all dependencies listed
```

**Database Client Tools (Optional but Recommended):**
```bash
# PostgreSQL clients:
# - pgAdmin (GUI): https://www.pgadmin.org/
# - psql (CLI): Included with PostgreSQL
# - TablePlus (GUI, paid): https://tableplus.com/
# - DBeaver (GUI, free): https://dbeaver.io/

# SQLite clients:
# - DB Browser for SQLite: https://sqlitebrowser.org/
# - sqlite3 (CLI): Usually pre-installed
sqlite3 --version
```

**API Testing Tools:**
```bash
# Option 1: Postman (GUI, beginner-friendly)
# Download: https://www.postman.com/downloads/

# Option 2: Insomnia (GUI, similar to Postman)
# Download: https://insomnia.rest/download

# Option 3: curl (CLI, always available)
curl --version

# Option 4: httpie (CLI, user-friendly curl)
pip install httpie
# Or: brew install httpie

# Test tools work
curl -X GET http://httpbin.org/get
http GET http://httpbin.org/get  # httpie syntax
```

**Estimated Time:**
- Database setup: 1-2 hours (first time)
- Project setup: 30 minutes
- Models & database layer: 4-6 hours
- Authentication: 3-4 hours
- Handlers & routes: 4-6 hours
- Middleware: 2-3 hours
- Testing: 3-5 hours
- **Total**: 20-30 hours

**Files You'll Create:**
- `main.go` - 80-120 lines
- `config/config.go` - 50-80 lines
- `models/user.go` - 150-200 lines
- `models/post.go` - 200-300 lines
- `handlers/auth.go` - 120-180 lines
- `handlers/posts.go` - 200-300 lines
- `middleware/auth.go` - 80-120 lines
- `middleware/logger.go` - 40-60 lines
- `database/database.go` - 100-150 lines
- `database/migrations/*.sql` - Several files
- `utils/jwt.go` - 60-100 lines
- `.env` - Configuration file

**New Challenges:**
- **Database Connections**: Connection pooling, error handling
- **SQL Queries**: Writing safe, efficient queries
- **Authentication**: Secure password handling, token management
- **Validation**: Input sanitization and validation
- **API Design**: REST principles, versioning, documentation
- **Security**: SQL injection, XSS, CSRF protection
- **Error Handling**: Consistent error responses
- **Testing**: Unit tests, integration tests with database

**Testing Your Setup:**
```bash
# Test PostgreSQL connection
cat > test_db.go << 'EOF'
package main
import (
    "database/sql"
    "fmt"
    "log"
    _ "github.com/lib/pq"
)
func main() {
    db, err := sql.Open("postgres", "postgres://blog_user:your_password@localhost/blog_db?sslmode=disable")
    if err != nil {
        log.Fatal(err)
    }
    defer db.Close()
    if err := db.Ping(); err != nil {
        log.Fatal(err)
    }
    fmt.Println("Database connection successful!")
}
EOF

go run test_db.go
rm test_db.go

# Test SQLite (alternative)
cat > test_sqlite.go << 'EOF'
package main
import (
    "database/sql"
    "fmt"
    "log"
    _ "github.com/mattn/go-sqlite3"
)
func main() {
    db, err := sql.Open("sqlite3", "./test.db")
    if err != nil {
        log.Fatal(err)
    }
    defer db.Close()
    fmt.Println("SQLite working!")
}
EOF

go run test_sqlite.go
rm test_sqlite.go test.db
```

**Environment Setup:**
```bash
# Create .env file
cat > .env << 'EOF'
DATABASE_URL=postgres://blog_user:your_password@localhost/blog_db?sslmode=disable
# Or for SQLite:
# DATABASE_URL=sqlite3://./blog.db

JWT_SECRET=your-secret-key-min-32-chars-change-me
PORT=8080
ENV=development
EOF

# IMPORTANT: Add to .gitignore
echo ".env" >> .gitignore
echo "*.db" >> .gitignore
```

**12-Factor App Compliance:**
This project follows [12-Factor App](https://12factor.net/) principles:
- **III. Config**: Store config in environment variables, not code
- **VI. Processes**: App is stateless (use DB/cache for state)
- **VII. Port binding**: Self-contained service exports HTTP
- **VIII. Concurrency**: Scale via process model (multiple instances)
- **XI. Logs**: Treat logs as event streams (stdout/stderr)

**Common Setup Issues:**

1. **PostgreSQL connection refused**:
   - Check if running: `brew services list` or `sudo systemctl status postgresql`
   - Verify port: `psql -h localhost -p 5432`
   - Check credentials in connection string

2. **"pq: password authentication failed"**:
   - Reset password: `ALTER USER blog_user WITH PASSWORD 'new_password';`
   - Check pg_hba.conf settings

3. **SQLite "undefined symbol" error**:
   - Need CGO: `export CGO_ENABLED=1`
   - Windows: Install MinGW-w64 or TDM-GCC
   - macOS: Install Xcode Command Line Tools

4. **Dependencies not downloading**:
   - Check proxy settings
   - Try: `go env -w GOPROXY=https://proxy.golang.org,direct`
   - Clear cache: `go clean -modcache`

5. **bcrypt errors**:
   - Ensure using `golang.org/x/crypto/bcrypt` (not other packages)
   - May need: `go get -u golang.org/x/crypto/bcrypt`

6. **Port 8080 in use**:
   - Change PORT in .env
   - Or kill process: `lsof -ti:8080 | xargs kill`

**Security Considerations:**
- Never commit `.env` file (contains secrets)
- Use strong JWT secrets (32+ random characters)
- Always hash passwords (never store plain text)
- Validate all inputs
- Use HTTPS in production
- Implement rate limiting
- Sanitize error messages (don't leak details)

**Learning Resources:**
- PostgreSQL Tutorial: https://www.postgresqltutorial.com/
- REST API Best Practices: https://restfulapi.net/
- JWT Explained: https://jwt.io/introduction
- SQL Injection Prevention: https://cheatsheetseries.owasp.org/

### Overview
Build a full-featured REST API for a blog or notes application with PostgreSQL/SQLite backend, user authentication, and proper API design. This teaches database integration, API patterns, and production-ready code structure.

### What You'll Learn
- **Database/SQL**: Work with relational databases in Go
- **SQL Queries**: CRUD operations, joins, transactions
- **HTTP Routing**: Advanced routing with gorilla/mux or chi
- **Middleware**: Authentication, logging, CORS, rate limiting
- **JWT Authentication**: Stateless authentication tokens
- **Request Validation**: Input validation and sanitization
- **Error Responses**: Structured error handling for APIs
- **Database Migrations**: Version control for database schema
- **Environment Variables**: Configuration management
- **Testing**: Unit and integration tests for APIs

### Core Features
1. User registration and login with JWT
2. CRUD operations for blog posts/notes
3. User-specific content (only see/edit your own)
4. Search and filtering
5. Pagination for list endpoints
6. Input validation and error handling
7. Rate limiting to prevent abuse
8. Database migrations

### Project Structure
```
blog-api/
├── main.go                 # Entry point
├── config/
│   └── config.go          # Configuration loading
├── models/
│   ├── user.go            # User struct and DB methods
│   └── post.go            # Post struct and DB methods
├── handlers/
│   ├── auth.go            # Registration, login
│   ├── posts.go           # Post CRUD handlers
│   └── users.go           # User management
├── middleware/
│   ├── auth.go            # JWT validation
│   ├── logger.go          # Request logging
│   └── ratelimit.go       # Rate limiting
├── database/
│   ├── database.go        # DB connection and setup
│   └── migrations/        # SQL migration files
├── utils/
│   ├── jwt.go             # JWT token generation/validation
│   └── validator.go       # Input validation helpers
├── go.mod
├── go.sum
└── .env                   # Environment variables
```

### Implementation Guide

#### Step 1: Setup and Dependencies

```bash
mkdir blog-api
cd blog-api
go mod init github.com/yourusername/blog-api

# Install dependencies
go get github.com/gorilla/mux           # HTTP router
go get github.com/lib/pq                # PostgreSQL driver
go get github.com/golang-jwt/jwt/v5     # JWT authentication
go get github.com/joho/godotenv         # Environment variables
go get golang.org/x/crypto/bcrypt       # Password hashing
go get github.com/go-playground/validator/v10  # Validation
```

**Alternative**: Use SQLite instead of PostgreSQL for simpler setup:
```bash
go get github.com/mattn/go-sqlite3
```

#### Step 2: Database Models (`models/`)

**Key Concepts:**
- **Database Tags**: Struct tags for SQL column mapping
- **Pointers for NULL**: Use pointers for nullable database fields
- **Prepared Statements**: Prevent SQL injection
- **Scanning Rows**: Convert SQL results to Go structs

**What you need to create:**

**`models/user.go`:**
- `User` struct with fields: ID, Username, Email, PasswordHash, CreatedAt, UpdatedAt
- Methods:
  - `Create(db)` - Insert new user, hash password with bcrypt
  - `GetByID(db, id)` - Retrieve user by ID
  - `GetByEmail(db, email)` - Retrieve user by email (for login)
  - `Update(db)` - Update user fields
  - `Delete(db)` - Delete user
  - `ValidatePassword(password)` - Compare password with hash

**`models/post.go`:**
- `Post` struct: ID, UserID, Title, Content, Published, CreatedAt, UpdatedAt
- Methods:
  - `Create(db)` - Insert new post
  - `GetByID(db, id)` - Retrieve post with user info (JOIN)
  - `GetAll(db, filters)` - List posts with pagination and filters
  - `GetByUser(db, userID)` - Get all posts by user
  - `Update(db)` - Update post
  - `Delete(db)` - Delete post
  - `Search(db, query)` - Search posts by title/content

**Learning Notes:**
- **SQL Injection Prevention**: Always use `db.Query()` with `?` placeholders, never string concatenation
- **bcrypt**: Use `bcrypt.GenerateFromPassword()` to hash, `bcrypt.CompareHashAndPassword()` to verify
- **NULL handling**: Use `sql.NullString`, `sql.NullTime`, or pointers for nullable fields
- **Scanning**: Use `row.Scan(&field1, &field2, ...)` to read query results

**Hints:**
- Hash password before storing: `bcrypt.GenerateFromPassword([]byte(password), bcrypt.DefaultCost)`
- For lists, add LIMIT and OFFSET for pagination
- Use `db.QueryRow()` for single results, `db.Query()` for multiple
- Close rows: `defer rows.Close()`
- Use transactions for operations that need atomicity

#### Step 3: Database Connection (`database/database.go`)

**What you need to create:**
- `InitDB(connectionString)` function that:
  - Opens database connection with `sql.Open()`
  - Tests connection with `db.Ping()`
  - Sets connection pool settings (MaxOpenConns, MaxIdleConns)
  - Returns `*sql.DB` or error
- `RunMigrations(db)` function:
  - Read migration files from `migrations/` directory
  - Execute SQL statements in order
  - Track which migrations have run (create migrations table)

**Migration files** (`migrations/001_initial.sql`):
```sql
CREATE TABLE IF NOT EXISTS users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS posts (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    title VARCHAR(200) NOT NULL,
    content TEXT,
    published BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_posts_user_id ON posts(user_id);
CREATE INDEX idx_posts_published ON posts(published);
```

**Hints:**
- Connection string format (PostgreSQL): `"postgres://user:password@localhost/dbname?sslmode=disable"`
- Connection string format (SQLite): `"./blog.db"`
- Set reasonable pool limits: `db.SetMaxOpenConns(25)`, `db.SetMaxIdleConns(5)`
- For migrations, sort files alphabetically and execute in order

#### Step 4: Authentication & JWT (`utils/jwt.go`, `handlers/auth.go`)

**Key Concepts:**
- **JWT Tokens**: Self-contained tokens with user info (no server-side session)
- **Claims**: Data stored in JWT (user ID, expiration time)
- **Signing**: Use secret key to sign token, verify authenticity
- **Bearer Token**: Send token in `Authorization: Bearer <token>` header

**What you need to create:**

**`utils/jwt.go`:**
- `GenerateToken(userID, username)` - Create JWT with claims:
  - User ID
  - Username
  - Expiration time (e.g., 24 hours)
  - Issued at time
- `ValidateToken(tokenString)` - Parse and verify token, return claims or error

**`handlers/auth.go`:**
- `Register` handler (POST /api/register):
  - Parse JSON request (username, email, password)
  - Validate input (email format, password strength)
  - Check if user already exists
  - Create user in database
  - Return success or error
- `Login` handler (POST /api/login):
  - Parse credentials
  - Find user by email
  - Validate password
  - Generate JWT token
  - Return token and user info

**Learning Notes:**
- **JWT Structure**: `header.payload.signature`
- **Claims**: Use `jwt.MapClaims` or custom struct
- **Signing Method**: `jwt.SigningMethodHS256` with secret key
- **Validation**: Check expiration, signature, and required claims

**Hints:**
- Store secret key in environment variable
- Set token expiration: `time.Now().Add(24 * time.Hour)`
- Parse token: `jwt.ParseWithClaims(tokenString, &claims, func(token) { return []byte(secret), nil })`
- Return token to client in JSON: `{"token": "...", "user": {...}}`

#### Step 5: Middleware (`middleware/`)

**Key Concepts:**
- **Middleware Pattern**: Wrap handlers to add functionality
- **Context**: Pass data between middleware and handlers
- **Handler Chain**: Multiple middleware can wrap a handler

**What you need to create:**

**`middleware/auth.go`:**
- `RequireAuth` middleware that:
  - Extracts token from `Authorization` header
  - Validates token
  - Extracts user ID from claims
  - Stores user ID in request context
  - Calls next handler or returns 401 Unauthorized

**`middleware/logger.go`:**
- `Logger` middleware that:
  - Logs request method, path, IP
  - Records start time
  - Calls next handler
  - Logs response status and duration

**`middleware/ratelimit.go`:**
- `RateLimit` middleware that:
  - Tracks requests per IP address
  - Uses map or external store (Redis)
  - Limits to N requests per time window
  - Returns 429 Too Many Requests if exceeded

**Learning Notes:**
- **Context**: Use `context.WithValue()` to store, `r.Context().Value()` to retrieve
- **Middleware Signature**: `func(http.Handler) http.Handler`
- **Chaining**: Wrap handlers: `logger(auth(handler))`

**Hints:**
- Extract token: `strings.TrimPrefix(r.Header.Get("Authorization"), "Bearer ")`
- Store in context: Define custom key type to avoid collisions
- Rate limiting: Use `sync.Map` with timestamp cleanup, or Redis for distributed systems
- Middleware order matters: logger → rate limit → auth → handler

#### Step 6: Handlers (`handlers/posts.go`)

**What you need to create:**
- `CreatePost` (POST /api/posts):
  - Extract user ID from context (set by auth middleware)
  - Parse request body (title, content, published)
  - Validate input
  - Create post in database
  - Return created post with 201 status

- `GetPosts` (GET /api/posts):
  - Parse query parameters (page, limit, published, search)
  - Query database with filters and pagination
  - Return JSON array of posts

- `GetPost` (GET /api/posts/{id}):
  - Extract post ID from URL
  - Query database
  - Return post or 404

- `UpdatePost` (PUT /api/posts/{id}):
  - Extract user ID from context
  - Find post by ID
  - Check if user owns post (authorization)
  - Parse update data
  - Update in database
  - Return updated post

- `DeletePost` (DELETE /api/posts/{id}):
  - Extract user ID
  - Check ownership
  - Delete from database
  - Return 204 No Content

**Hints:**
- Get URL params with gorilla/mux: `mux.Vars(r)["id"]`
- Parse JSON body: `json.NewDecoder(r.Body).Decode(&struct)`
- Query params: `r.URL.Query().Get("page")`
- Check ownership: `if post.UserID != userID { return 403 Forbidden }`
- Use validator package: `validate.Struct(post)`

#### Step 7: Main Application (`main.go`)

**What you need to create:**
- Load environment variables from `.env` file
- Initialize database connection
- Run migrations
- Create router (gorilla/mux)
- Register routes:
  - Public routes: `/api/register`, `/api/login`
  - Protected routes (with auth middleware): `/api/posts/*`, `/api/users/*`
- Apply global middleware (logger, CORS)
- Start HTTP server

**Environment variables** (`.env`):
```
DATABASE_URL=postgres://user:password@localhost/blog?sslmode=disable
JWT_SECRET=your-secret-key-change-in-production
PORT=8080
```

**Hints:**
- Use subrouters for different route groups
- Protected routes: `api := router.PathPrefix("/api").Subrouter()` then `api.Use(middleware.RequireAuth)`
- Handle preflight requests for CORS
- Graceful shutdown: Listen for signals, close DB connection

#### Step 8: Testing

**What you need to create:**
- Unit tests for models (test database operations with test DB)
- Handler tests (use `httptest.NewRecorder()` and `httptest.NewRequest()`)
- Integration tests (test full request flow)

**Example test structure:**
```go
func TestCreatePost(t *testing.T) {
    // Setup test database
    // Create test user
    // Create post via handler
    // Assert response
    // Verify in database
}
```

**Hints:**
- Use separate test database or in-memory SQLite
- Generate test JWT tokens for protected endpoints
- Use table-driven tests for multiple scenarios
- Clean up test data after each test

### Build and Run

```bash
# Create .env file with your config

# Run migrations
go run main.go migrate

# Start server
go run main.go

# Test endpoints
curl -X POST http://localhost:8080/api/register \
  -H "Content-Type: application/json" \
  -d '{"username":"john","email":"john@example.com","password":"secret123"}'

curl -X POST http://localhost:8080/api/login \
  -H "Content-Type: application/json" \
  -d '{"email":"john@example.com","password":"secret123"}'

# Use token from login response
curl -X POST http://localhost:8080/api/posts \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -d '{"title":"My First Post","content":"Hello World!","published":true}'
```

### Challenge Yourself

1. **Comments System**: Add comments on posts with nested replies
2. **File Uploads**: Store images/files for posts (use S3 or local storage)
3. **Email Verification**: Send confirmation email on registration
4. **Password Reset**: Forgot password flow with email tokens
5. **OAuth Integration**: Login with Google/GitHub
6. **WebSockets**: Real-time notifications for new posts/comments
7. **Caching**: Add Redis caching for frequently accessed data
8. **Full-Text Search**: Use PostgreSQL full-text search or Elasticsearch
9. **API Versioning**: Support multiple API versions
10. **GraphQL Alternative**: Build GraphQL API instead of REST

### Common Gotcas

**Problem**: SQL injection vulnerability
**Fix**: Always use parameterized queries with `?` placeholders

**Problem**: Password stored in plain text
**Fix**: Use `bcrypt.GenerateFromPassword()` before storing

**Problem**: JWT token never expires
**Fix**: Set expiration claim in token, validate on each request

**Problem**: Race conditions in rate limiter
**Fix**: Use mutex or atomic operations for counter access

**Problem**: Database connection leaks
**Fix**: Always defer `rows.Close()` and `stmt.Close()`

---

## Project 2: Web Scraper & Alert System

### Prerequisites & Requirements

**Before Starting:**
- **Completed**:
  - All basic projects OR
  - REST API project (intermediate)
- **Equivalent Experience**:
  - HTTP clients and servers in Go
  - HTML/CSS basics
  - Goroutines and channels
  - Database operations

**Knowledge Prerequisites:**
- **Must Know**:
  - HTTP requests/responses
  - HTML structure and DOM
  - CSS selectors basics
  - Goroutines, channels, sync primitives
  - Error handling and retry logic
  - Time and duration handling
- **Should Know**:
  - Web scraping ethics and legality
  - User-Agent headers and rate limiting
  - Parsing JSON and XML
  - SMTP basics for email
  - Webhook concepts
- **Will Learn**:
  - HTML parsing with goquery
  - Advanced concurrency patterns
  - Scheduling and cron expressions
  - Change detection algorithms
  - Circuit breaker pattern
  - Email sending via SMTP
  - Webhook implementations
  - Rate limiting strategies

**New Go Concepts:**
1. **goquery**: jQuery-like HTML parsing for Go
2. **cron**: Schedule tasks with cron expressions
3. **Worker Pools**: Concurrency pattern for parallel work
4. **Fan-out/Fan-in**: Distribute work across workers
5. **Circuit Breaker**: Prevent cascading failures
6. **SMTP**: Email sending protocol
7. **Context with Timeout**: Request cancellation
8. **Select with Multiple Channels**: Coordinating goroutines

**External Dependencies:**
- **Required**:
  - `github.com/PuerkitoBio/goquery` - HTML parsing (jQuery-like)
  - `github.com/robfig/cron/v3` - Cron scheduler
  - `github.com/go-sql-driver/mysql` or SQLite driver - Data storage
  - `golang.org/x/net/html` - HTML tokenization
- **Optional (for notifications)**:
  - `gopkg.in/mail.v2` - Email library (SMTP helper)
  - `github.com/slack-go/slack` - Slack API client
  - Standard library `net/smtp` works too

**System Requirements:**
- **OS**: macOS, Linux, Windows
- **RAM**: 4GB minimum (8GB for heavy scraping)
- **Network**: Stable internet connection
- **Disk**: 500MB for data storage
- **Database**: SQLite (simple) or PostgreSQL (production)
- **Optional**: Email account with SMTP access (Gmail, SendGrid, etc.)

**Web Scraping Considerations:**
- **Legal**: Check website's `robots.txt` and terms of service
- **Ethical**: Respect rate limits, don't overload servers
- **Technical**: Handle dynamic content, JavaScript rendering
- **Blocking**: Rotate User-Agents, use proxies if needed

**What to Install:**
```bash
# 1. Create project
mkdir scraper-alert
cd scraper-alert
go mod init github.com/yourusername/scraper-alert

# 2. Install dependencies
go get github.com/PuerkitoBio/goquery
go get github.com/robfig/cron/v3
go get github.com/mattn/go-sqlite3  # Or PostgreSQL driver
go get gopkg.in/mail.v2  # Optional: easier email handling
go get github.com/slack-go/slack  # Optional: Slack integration

# 3. Verify
go mod tidy
cat go.mod
```

**Notification Service Setup:**

**Email (SMTP):**
```bash
# Gmail setup (requires App Password)
# 1. Go to Google Account settings
# 2. Enable 2-Factor Authentication
# 3. Generate App Password:
#    https://myaccount.google.com/apppasswords
# 4. Use this in your .env:

cat >> .env << 'EOF'
# Email settings
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USERNAME=your-email@gmail.com
SMTP_PASSWORD=your-app-password-16-chars
SMTP_FROM=your-email@gmail.com
EOF

# Alternative: SendGrid (free 100 emails/day)
# 1. Sign up: https://sendgrid.com/
# 2. Create API key
# 3. Use API instead of SMTP

# Alternative: Mailtrap (testing only)
# https://mailtrap.io/ - fake SMTP for development
```

**Slack Webhook:**
```bash
# 1. Create Slack App:
#    https://api.slack.com/apps
# 2. Enable Incoming Webhooks
# 3. Add webhook to workspace
# 4. Copy webhook URL

cat >> .env << 'EOF'
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
EOF
```

**Database Setup:**
```bash
# SQLite (easiest)
go get github.com/mattn/go-sqlite3
touch scraper.db

# Or PostgreSQL (from previous project)
# Use same setup as REST API project
```

**Testing Tools:**
```bash
# Test website for scraping (legal, designed for testing)
echo "Test scraping on:"
echo "  - https://books.toscrape.com/"
echo "  - https://quotes.toscrape.com/"
echo "  - http://httpbin.org/html"

# Check robots.txt before scraping any site
curl https://example.com/robots.txt

# Test HTML parsing locally
cat > test_scrape.go << 'EOF'
package main
import (
    "fmt"
    "log"
    "net/http"
    "github.com/PuerkitoBio/goquery"
)
func main() {
    res, err := http.Get("https://quotes.toscrape.com/")
    if err != nil {
        log.Fatal(err)
    }
    defer res.Body.Close()
    doc, err := goquery.NewDocumentFromReader(res.Body)
    if err != nil {
        log.Fatal(err)
    }
    doc.Find(".quote").Each(func(i int, s *goquery.Selection) {
        text := s.Find(".text").Text()
        author := s.Find(".author").Text()
        fmt.Printf("%d. %s - %s\n", i+1, text, author)
    })
}
EOF

go run test_scrape.go
rm test_scrape.go
```

**Environment Configuration:**
```bash
cat > .env << 'EOF'
# Database
DATABASE_URL=sqlite3://./scraper.db
# Or: postgres://user:pass@localhost/scraper_db?sslmode=disable

# Scraping settings
USER_AGENT=Mozilla/5.0 (compatible; YourScraperBot/1.0)
MAX_CONCURRENT_SCRAPES=5
REQUEST_TIMEOUT_SECONDS=30
RETRY_ATTEMPTS=3
RATE_LIMIT_DELAY_MS=1000

# Email notifications
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USERNAME=your-email@gmail.com
SMTP_PASSWORD=your-app-password
SMTP_FROM=your-email@gmail.com
NOTIFY_EMAIL=recipient@example.com

# Slack notifications (optional)
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL

# Webhook notifications (optional)
WEBHOOK_URL=https://yourapi.com/webhook

# Scheduler
SCRAPE_INTERVAL_MINUTES=60

# Server
PORT=8080
EOF

echo ".env" >> .gitignore
echo "*.db" >> .gitignore
```

**Estimated Time:**
- Setup and dependencies: 1-2 hours
- HTML parser and scraper: 4-6 hours
- Change detection: 2-3 hours
- Email notifications: 2-3 hours
- Webhook/Slack: 1-2 hours each
- Scheduling system: 3-4 hours
- Database integration: 3-4 hours
- Concurrency and rate limiting: 4-6 hours
- Web UI: 4-6 hours (optional)
- Testing: 4-6 hours
- **Total**: 30-45 hours

**Files You'll Create:**
- `main.go` - 100-150 lines
- `config/config.go` - 60-100 lines
- `scraper/scraper.go` - 200-300 lines
- `scraper/parser.go` - 150-200 lines
- `scraper/differ.go` - 100-150 lines
- `scheduler/scheduler.go` - 150-250 lines
- `notifiers/email.go` - 80-120 lines
- `notifiers/webhook.go` - 50-80 lines
- `notifiers/slack.go` - 60-100 lines
- `models/target.go` - 100-150 lines
- `models/result.go` - 80-120 lines
- `database/database.go` - 150-200 lines
- `workers/pool.go` - 100-150 lines
- `api/handlers.go` - 200-300 lines (if building UI)

**New Challenges:**
- **HTML Parsing**: Understanding CSS selectors, DOM traversal
- **Concurrency**: Managing worker pools, preventing race conditions
- **Rate Limiting**: Avoiding IP bans, respecting servers
- **Change Detection**: Comparing text, handling minor variations
- **Scheduling**: Running tasks reliably at intervals
- **Error Handling**: Network failures, timeouts, retries
- **Resource Management**: Memory with large HTML docs
- **Legal/Ethical**: Respecting robots.txt, terms of service

**Testing Your Setup:**
```bash
# Test goquery installation
cat > test_goquery.go << 'EOF'
package main
import (
    "fmt"
    "strings"
    "github.com/PuerkitoBio/goquery"
)
func main() {
    html := `<html><body><div class="test">Hello World</div></body></html>`
    doc, _ := goquery.NewDocumentFromReader(strings.NewReader(html))
    text := doc.Find(".test").Text()
    fmt.Println("Parsed:", text)
}
EOF
go run test_goquery.go
# Should print: Parsed: Hello World
rm test_goquery.go

# Test cron scheduler
cat > test_cron.go << 'EOF'
package main
import (
    "fmt"
    "time"
    "github.com/robfig/cron/v3"
)
func main() {
    c := cron.New()
    c.AddFunc("@every 2s", func() { fmt.Println("Task executed") })
    c.Start()
    time.Sleep(5 * time.Second)
    c.Stop()
}
EOF
go run test_cron.go
# Should print "Task executed" 2-3 times
rm test_cron.go

# Test SMTP connection
cat > test_smtp.go << 'EOF'
package main
import (
    "fmt"
    "net/smtp"
)
func main() {
    client, err := smtp.Dial("smtp.gmail.com:587")
    if err != nil {
        fmt.Println("Cannot reach SMTP server:", err)
        return
    }
    defer client.Quit()
    fmt.Println("SMTP connection successful")
}
EOF
go run test_smtp.go
rm test_smtp.go
```

**Common Setup Issues:**

1. **goquery not installing**:
   - Try: `go get -u github.com/PuerkitoBio/goquery`
   - Check internet connection
   - Verify GOPROXY: `go env GOPROXY`

2. **Gmail SMTP not working**:
   - Must use App Password, not regular password
   - Enable 2FA first
   - Check "Less secure app access" (deprecated, use App Password)
   - Port 587 for TLS, 465 for SSL

3. **goquery.Selection returns empty**:
   - Inspect actual HTML: `doc.Html()`
   - Test selectors in browser DevTools first
   - Website may use JavaScript (goquery doesn't run JS)
   - Check for dynamic content loading

4. **Getting blocked while scraping**:
   - Add delays between requests: `time.Sleep(2 * time.Second)`
   - Set proper User-Agent header
   - Respect robots.txt
   - Reduce concurrent requests

5. **Memory issues with large pages**:
   - Close response bodies: `defer res.Body.Close()`
   - Limit concurrent scrapes
   - Use streaming for large documents

6. **Cron not triggering**:
   - Check cron expression syntax
   - Verify timezone settings
   - Keep program running: `select {}`

**Web Scraping Best Practices:**

**Legal & Ethical:**
- Check `robots.txt`: `curl https://site.com/robots.txt`
- Read terms of service
- Don't scrape personal data without consent
- Some sites explicitly prohibit scraping

**Technical:**
- Set descriptive User-Agent:
  ```go
  req.Header.Set("User-Agent", "YourBot/1.0 (+https://yoursite.com/bot)")
  ```
- Add delays: `time.Sleep(1 * time.Second)` between requests
- Use timeouts:
  ```go
  client := &http.Client{Timeout: 30 * time.Second}
  ```
- Handle rate limits:
  - 429 status code → back off exponentially
  - Implement token bucket algorithm
- Cache results to avoid duplicate requests

**Error Handling:**
- Retry on network errors (3-5 attempts)
- Exponential backoff: `time.Sleep(2^attempt * time.Second)`
- Circuit breaker: Stop after N consecutive failures
- Log failures for debugging

**CSS Selector Resources:**
- MDN CSS Selectors: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors
- CSS Selector Tester: https://try.jsoup.org/ (similar syntax)
- Chrome DevTools: Right-click element → Copy → Copy selector

**Learning Resources:**
- goquery documentation: https://github.com/PuerkitoBio/goquery
- Cron expressions: https://crontab.guru/
- SMTP tutorial: https://mailtrap.io/blog/golang-send-email/
- Web scraping guide: https://www.scraperapi.com/blog/web-scraping-guide/

### Overview
Build a web scraper that monitors websites for changes (like price drops, new content, etc.) and sends notifications via email, Slack, or webhooks. Teaches HTML parsing, concurrent scraping, data persistence, and scheduling.

### What You'll Learn
- **HTML Parsing**: Extract data from web pages (goquery)
- **HTTP Clients**: Custom clients with headers, cookies, timeouts
- **Concurrency Patterns**: Worker pools, fan-out/fan-in
- **Channels**: Coordinating concurrent operations
- **Scheduling**: Run tasks on schedule (cron-like)
- **Notifications**: Send emails (SMTP) and webhook requests
- **Data Diffing**: Detect changes between scrapes
- **Error Recovery**: Retry logic and circuit breakers

### Core Features
1. Define scraping targets (URL, selectors, frequency)
2. Extract data using CSS selectors
3. Detect changes from previous scrape
4. Send notifications on changes
5. Schedule periodic scraping
6. Concurrent scraping with rate limiting
7. Store scrape history in database
8. Web UI to manage targets and view history

### Project Structure
```
scraper-alert/
├── main.go
├── scraper/
│   ├── scraper.go         # Core scraping logic
│   ├── parser.go          # HTML parsing helpers
│   └── differ.go          # Change detection
├── scheduler/
│   └── scheduler.go       # Cron-like scheduling
├── notifiers/
│   ├── email.go           # Email notifications
│   ├── webhook.go         # Webhook notifications
│   └── slack.go           # Slack integration
├── models/
│   ├── target.go          # Scraping target definition
│   └── result.go          # Scrape result storage
├── api/
│   └── handlers.go        # REST API for managing targets
├── web/
│   └── templates/         # HTML templates for UI
└── go.mod
```

### Implementation Guide

#### Step 1: Setup and Dependencies

```bash
mkdir scraper-alert
cd scraper-alert
go mod init github.com/yourusername/scraper-alert

go get github.com/PuerkitoBio/goquery       # HTML parsing
go get github.com/robfig/cron/v3            # Scheduling
go get github.com/go-resty/resty/v2         # HTTP client
go get github.com/mattn/go-sqlite3          # Database
go get gopkg.in/gomail.v2                   # Email sending
```

#### Step 2: Core Scraper (`scraper/scraper.go`)

**Key Concepts:**
- **HTTP GET**: Fetch web pages with custom headers
- **HTML Parsing**: Navigate DOM tree with CSS selectors
- **User-Agent**: Identify as browser to avoid blocks
- **Rate Limiting**: Respect website load

**What you need to create:**
- `Target` struct: URL, Selector (CSS), CheckInterval, LastValue, NotifyOnChange
- `Scraper` struct with HTTP client configuration
- `NewScraper()` - Initialize with custom user-agent, timeouts
- Methods:
  - `Fetch(url)` - GET request, return HTML document
  - `Extract(doc, selector)` - Use goquery to find and extract text/attributes
  - `Scrape(target)` - Fetch page, extract data, return result
  - `ScrapeWithRetry(target, maxRetries)` - Retry on failures with exponential backoff

**Learning Notes:**
- **goquery**: jQuery-like API for Go: `doc.Find(selector).Each(func(i, s) {...})`
- **CSS Selectors**: `.class`, `#id`, `tag`, `[attribute=value]`
- **HTTP Headers**: Set User-Agent to avoid bot detection
- **Context**: Use `context.WithTimeout()` for request timeouts

**Hints:**
- Create custom HTTP client with timeout: `&http.Client{Timeout: 30 * time.Second}`
- Load HTML: `goquery.NewDocumentFromReader(response.Body)`
- Extract text: `selection.Text()`
- Extract attributes: `selection.Attr("href")` or `selection.AttrOr("src", "")`
- Rate limit: Add `time.Sleep()` between requests or use token bucket

#### Step 3: Change Detection (`scraper/differ.go`)

**What you need to create:**
- `CompareResults(old, new)` - Return bool if changed + description of changes
- `HashContent(content)` - Generate hash for quick comparison
- Different comparison strategies:
  - Exact match
  - Threshold-based (e.g., price changed by >10%)
  - Regex pattern matching
  - Keyword presence

**Hints:**
- Use `crypto/sha256` for hashing
- Store previous result in database or memory
- For numeric values: parse strings to floats, compare difference
- For text: use string comparison or fuzzy matching

#### Step 4: Notifications (`notifiers/`)

**Key Concepts:**
- **SMTP**: Send emails via mail server
- **Webhooks**: POST JSON to external services
- **Templates**: Format notification messages

**What you need to create:**

**`notifiers/email.go`:**
- `EmailNotifier` struct with SMTP config (host, port, username, password)
- `Send(to, subject, body)` - Send email using gomail

**`notifiers/webhook.go`:**
- `WebhookNotifier` struct with webhook URL
- `Send(payload)` - POST JSON to webhook endpoint

**`notifiers/slack.go`:**
- `SlackNotifier` struct with webhook URL
- `SendMessage(text, attachments)` - Format and send Slack message

**Hints:**
- SMTP config: `gomail.NewDialer("smtp.gmail.com", 587, "user@gmail.com", "password")`
- Slack webhook format: `{"text": "message", "attachments": [...]}`
- Test with webhook.site for debugging
- Use HTML templates for rich email formatting

#### Step 5: Scheduling (`scheduler/scheduler.go`)

**Key Concepts:**
- **Cron Expressions**: Define schedules (e.g., "*/5 * * * *" = every 5 minutes)
- **Goroutines**: Each target scraped in separate goroutine
- **Context Cancellation**: Gracefully stop scheduled jobs

**What you need to create:**
- `Scheduler` struct with cron instance and target list
- `AddTarget(target)` - Register target with schedule
- `RemoveTarget(targetID)` - Unregister target
- `Start()` - Begin scheduling
- `Stop()` - Stop all jobs gracefully

For each scheduled scrape:
- Fetch and parse page
- Compare with previous result
- If changed, send notifications
- Store result in database
- Update last-check timestamp

**Hints:**
- Use `cron.New()` from robfig/cron
- Add job: `c.AddFunc("@every 1h", func() { scrapeTarget(target) })`
- Run in goroutines: `go scrapeTarget(target)`
- Use WaitGroup to track running jobs
- Cancel with context: pass `ctx` to scraper, check `ctx.Done()`

#### Step 6: Data Storage (`models/`)

**What you need to create:**
- Database schema:
  - `targets` table: id, url, selector, check_interval, last_value, last_checked, created_at
  - `results` table: id, target_id, value, changed, scraped_at
  - `notifications` table: id, target_id, notification_type, sent_at, success
- Models with CRUD methods:
  - `Target.Create()`, `Target.GetAll()`, `Target.Update()`, `Target.Delete()`
  - `Result.Create()`, `Result.GetByTarget()`

**Hints:**
- Use SQLite for simplicity or PostgreSQL for production
- Index `target_id` in results table for fast lookups
- Store check_interval as integer (minutes)
- Use TEXT for long content values

#### Step 7: API & Web UI (`api/handlers.go`)

**What you need to create:**
- REST API endpoints:
  - `POST /api/targets` - Create new scraping target
  - `GET /api/targets` - List all targets with status
  - `GET /api/targets/{id}` - Get target details and history
  - `PUT /api/targets/{id}` - Update target
  - `DELETE /api/targets/{id}` - Delete target
  - `POST /api/targets/{id}/test` - Test scrape immediately
- Web UI (optional):
  - Dashboard showing all targets and last check time
  - Form to add/edit targets
  - History view with timeline of changes

**Hints:**
- Use gorilla/mux for routing
- Return target status: "active", "error", "paused"
- Show last scrape result and timestamp
- Provide test endpoint to verify selectors work

#### Step 8: Concurrent Scraping

**Key Concepts:**
- **Worker Pool**: Fixed number of goroutines processing jobs
- **Channels**: Queue of targets to scrape
- **Rate Limiting**: Control requests per second

**What you need to create:**
- `WorkerPool` struct with:
  - Number of workers
  - Job queue (channel of targets)
  - Result channel
- `Start(workers)` - Launch N worker goroutines
- `Submit(target)` - Add target to queue
- `Stop()` - Drain queue and stop workers

Worker logic:
- Read from job queue
- Scrape target
- Send result to result channel
- Handle errors gracefully

**Hints:**
- Create buffered channels: `make(chan Target, 100)`
- Worker pattern:
```go
for target := range jobQueue {
    result := scrape(target)
    resultChan <- result
}
```
- Rate limit with ticker: `time.NewTicker(time.Second / requestsPerSecond)`
- Use `sync.WaitGroup` to wait for all workers to finish

### Build and Run

```bash
# Initialize database
go run main.go migrate

# Start server
go run main.go

# Add a target via API
curl -X POST http://localhost:8080/api/targets \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://example.com/product",
    "selector": ".price",
    "check_interval": 60,
    "notify_email": "you@example.com"
  }'

# Test immediate scrape
curl -X POST http://localhost:8080/api/targets/1/test
```

### Challenge Yourself

1. **JavaScript Rendering**: Use chromedp or rod to scrape JS-heavy sites
2. **Proxy Support**: Rotate proxies to avoid rate limits/blocks
3. **CAPTCHA Handling**: Integrate CAPTCHA solving service
4. **Diff Visualization**: Show visual diff of HTML changes
5. **RSS Feed**: Expose changes as RSS feed
6. **Browser Extension**: Chrome extension to easily add scraping targets
7. **AI Extraction**: Use LLMs to extract data without selectors
8. **Distributed Scraping**: Scale across multiple machines with Redis queue
9. **Historical Charts**: Graph price/value changes over time
10. **Mobile App**: React Native or Flutter app for notifications

### Common Gotchas

**Problem**: Getting blocked by websites
**Fix**: Rotate user agents, add delays, use proxies, respect robots.txt

**Problem**: Selectors break when site changes
**Fix**: Support multiple fallback selectors, send alert if extraction fails

**Problem**: Memory leaks from goroutines
**Fix**: Always close channels, use context for cancellation

**Problem**: Database locks with SQLite
**Fix**: Use WAL mode or switch to PostgreSQL for concurrent writes

---

## Project 3A: NoSQL Database Integration (MongoDB & Redis)

### Prerequisites & Requirements

**Before Starting:**
- **Completed**: REST API with Database project
- **Equivalent Experience**:
  - SQL database experience
  - REST API development
  - Data modeling

**Knowledge Prerequisites:**
- **Must Know**:
  - Database concepts (CRUD operations)
  - JSON data structures
  - Go structs and interfaces
  - Error handling
  - HTTP servers
- **Should Know**:
  - SQL vs NoSQL differences
  - Document databases
  - Key-value stores
  - Data modeling patterns
- **Will Learn**:
  - MongoDB operations (documents, collections)
  - Redis data structures (strings, lists, sets, hashes, sorted sets)
  - NoSQL data modeling
  - Caching strategies
  - Session management
  - Pub/Sub messaging
  - Full-text search basics

**New Go Concepts:**
1. **mongo.Client**: MongoDB driver
2. **bson**: Binary JSON for MongoDB
3. **redis.Client**: Redis driver
4. **Pipeline**: Batch Redis operations
5. **Context with Timeout**: Database operation timeouts
6. **Aggregation Pipelines**: MongoDB queries
7. **TTL**: Time-to-live for cache entries

**External Dependencies:**
- **Required**:
  - `go.mongodb.org/mongo-driver` - Official MongoDB driver
  - `github.com/redis/go-redis/v9` - Redis client
- **Optional**:
  - `github.com/go-playground/validator/v10` - Validation

**System Requirements:**
- **OS**: Linux, macOS, Windows
- **RAM**: 4GB minimum (8GB recommended)
- **Disk**: 1GB+ for databases
- **Databases**:
  - MongoDB 4.4+ (500MB-1GB storage)
  - Redis 6.0+ (minimal storage for cache)

**What to Install:**

**MongoDB Installation:**
```bash
# macOS
brew tap mongodb/brew
brew install mongodb-community
brew services start mongodb-community

# Linux (Ubuntu/Debian)
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt update
sudo apt install -y mongodb-org
sudo systemctl start mongod
sudo systemctl enable mongod

# Windows
# Download installer from: https://www.mongodb.com/try/download/community
# Follow installation wizard

# Verify MongoDB
mongosh
# Should connect to MongoDB shell
# Type: exit

# Create database and user
mongosh
use myapp
db.createUser({
  user: "appuser",
  pwd: "password123",
  roles: [{role: "readWrite", db: "myapp"}]
})
exit
```

**Redis Installation:**
```bash
# macOS
brew install redis
brew services start redis

# Linux (Ubuntu/Debian)
sudo apt update
sudo apt install redis-server
sudo systemctl start redis-server
sudo systemctl enable redis-server

# Windows
# Download from: https://github.com/microsoftarchive/redis/releases
# Or use WSL2

# Verify Redis
redis-cli ping
# Should return: PONG

# Test basic commands
redis-cli
127.0.0.1:6379> SET mykey "Hello"
127.0.0.1:6379> GET mykey
127.0.0.1:6379> EXIT
```

**Go Dependencies:**
```bash
mkdir nosql-app
cd nosql-app
go mod init github.com/yourusername/nosql-app

# MongoDB driver
go get go.mongodb.org/mongo-driver/mongo
go get go.mongodb.org/mongo-driver/bson

# Redis driver
go get github.com/redis/go-redis/v9

go mod tidy
```

**Testing Setup:**
```bash
# Test MongoDB connection
cat > test_mongo.go << 'EOF'
package main
import (
    "context"
    "fmt"
    "log"
    "time"
    "go.mongodb.org/mongo-driver/mongo"
    "go.mongodb.org/mongo-driver/mongo/options"
)
func main() {
    ctx, cancel := context.WithTimeout(context.Background(), 10*time.Second)
    defer cancel()

    client, err := mongo.Connect(ctx, options.Client().ApplyURI("mongodb://localhost:27017"))
    if err != nil {
        log.Fatal(err)
    }
    defer client.Disconnect(ctx)

    if err := client.Ping(ctx, nil); err != nil {
        log.Fatal(err)
    }
    fmt.Println("MongoDB connection successful!")
}
EOF

go run test_mongo.go
rm test_mongo.go

# Test Redis connection
cat > test_redis.go << 'EOF'
package main
import (
    "context"
    "fmt"
    "github.com/redis/go-redis/v9"
)
func main() {
    ctx := context.Background()
    rdb := redis.NewClient(&redis.Options{
        Addr: "localhost:6379",
    })

    pong, err := rdb.Ping(ctx).Result()
    if err != nil {
        panic(err)
    }
    fmt.Println("Redis:", pong)
}
EOF

go run test_redis.go
rm test_redis.go
```

**Environment Configuration:**
```bash
cat > .env << 'EOF'
# MongoDB
MONGODB_URI=mongodb://localhost:27017
MONGODB_DATABASE=myapp
MONGODB_USERNAME=appuser
MONGODB_PASSWORD=password123

# Redis
REDIS_ADDR=localhost:6379
REDIS_PASSWORD=
REDIS_DB=0

# Server
PORT=8080

# Cache
CACHE_TTL_SECONDS=300
CACHE_ENABLED=true
EOF

echo ".env" >> .gitignore
```

**Estimated Time:**
- MongoDB setup: 1-2 hours
- Redis setup: 1 hour
- MongoDB CRUD: 4-6 hours
- Redis operations: 3-4 hours
- Caching layer: 3-4 hours
- Session management: 2-3 hours
- Pub/Sub: 2-3 hours
- REST API integration: 4-6 hours
- **Total**: 20-30 hours

**Files You'll Create:**
- `main.go` - 100-150 lines
- `config/config.go` - 80-120 lines
- `database/mongodb.go` - 150-250 lines
- `database/redis.go` - 150-250 lines
- `models/user.go` - 100-150 lines
- `models/post.go` - 100-150 lines
- `handlers/handlers.go` - 250-400 lines
- `cache/cache.go` - 150-250 lines
- `session/session.go` - 100-150 lines

### Overview
Build a REST API that uses MongoDB for document storage and Redis for caching, sessions, and real-time features. Learn NoSQL data modeling, caching strategies, and distributed data patterns.

### What You'll Learn
- **MongoDB**: Document database operations
- **BSON**: Binary JSON encoding
- **Collections & Documents**: NoSQL data modeling
- **Indexes**: Query optimization
- **Aggregation Pipeline**: Complex queries
- **Redis Data Structures**: Strings, lists, sets, hashes, sorted sets
- **Caching Strategies**: Cache-aside, write-through
- **Session Management**: Distributed sessions with Redis
- **Pub/Sub**: Real-time messaging
- **TTL**: Automatic expiration

### Core Features
1. User management with MongoDB
2. Blog posts with MongoDB
3. Redis caching layer (cache-aside pattern)
4. Session storage in Redis
5. Rate limiting with Redis
6. Real-time notifications (Pub/Sub)
7. Leaderboard with sorted sets
8. Recent activity with lists
9. Full CRUD REST API
10. Search functionality

### Project Structure
```
nosql-app/
├── main.go
├── config/
│   └── config.go           # Configuration
├── database/
│   ├── mongodb.go          # MongoDB connection
│   └── redis.go            # Redis connection
├── models/
│   ├── user.go             # User model
│   ├── post.go             # Post model
│   └── session.go          # Session model
├── handlers/
│   ├── users.go            # User handlers
│   ├── posts.go            # Post handlers
│   └── auth.go             # Auth handlers
├── cache/
│   └── cache.go            # Caching logic
├── session/
│   └── session.go          # Session management
├── middleware/
│   ├── auth.go             # Auth middleware
│   └── ratelimit.go        # Rate limiting
└── pubsub/
    └── pubsub.go           # Pub/Sub messaging
```

### Implementation Guide

#### Step 1: MongoDB Setup and CRUD

**Key Concepts:**
- **Documents**: JSON-like records
- **Collections**: Groups of documents (like tables)
- **BSON**: Binary JSON format
- **ObjectID**: MongoDB's unique identifier

**What you need to create:**
- User model with BSON tags (`_id`, `username`, `email`, etc.)
- MongoDB struct with `CreateUser(user)` function:
  - Get collection using `client.Database(name).Collection("users")`
  - Set timestamps
  - Use `collection.InsertOne()` to insert
  - Extract inserted ID from result
- `GetUserByID(id)` function:
  - Convert string ID to ObjectID using `primitive.ObjectIDFromHex()`
  - Use `collection.FindOne()` with filter
  - Decode result into User struct
- `UpdateUser(id, updates)` function:
  - Convert ID, create filter
  - Use `collection.UpdateOne()` with `$set` operator
  - Update `updated_at` timestamp
- `DeleteUser(id)` function:
  - Convert ID, use `collection.DeleteOne()`

**Hints:**
- Use `primitive.ObjectID` for IDs
- Use `bson` tags for MongoDB field mapping
- Always use `context.Background()` or context with timeout
- Handle `mongo.ErrNoDocuments` for not found
- BSON tags: `bson:"field_name"` for MongoDB fields

#### Step 2: MongoDB Queries and Indexes

**What you need to create:**

**Find with Filters:**
- `FindUsers(filter)` function
- Use `collection.Find()` with bson.M filter (e.g., `bson.M{"email": "test@example.com"}`)
- Returns cursor - iterate with `cursor.All()` to decode into slice
- Remember to `defer cursor.Close()`

**Pagination:**
- `GetPostsPaginated(page, limit)` function
- Use `options.Find()` to configure query:
  - `SetSkip()` - calculate skip from page number: `(page-1) * limit`
  - `SetLimit()` - max results per page
  - `SetSort()` - sort by field: `bson.D{{Key: "created_at", Value: -1}}` (descending)
- Execute with `collection.Find(ctx, filter, opts)`

**Indexes:**
- `CreateIndexes()` function
- Create `[]mongo.IndexModel` with:
  - `Keys`: field and direction (1 = ascending, -1 = descending)
  - `Options`: `SetUnique(true)` for unique indexes
- Use `collection.Indexes().CreateMany()` to create
- Common indexes: email (unique), username (unique), created_at

#### Step 3: Redis Caching Layer

**Key Concepts:**
- **Cache-Aside Pattern**: Check cache, if miss, fetch from DB and populate cache
- **TTL**: Automatic expiration
- **Cache Invalidation**: Delete cache on updates

**What you need to create:**

**Cache struct:**
- Wrapper around `redis.Client`
- Store TTL duration
- Methods: `Get(key)`, `Set(key, value)`, `Delete(key)`
- Use `redis.Get()`, `redis.Set(key, value, ttl)`, `redis.Del()`

**Cache-Aside Pattern in Handler:**
- Build cache key: `fmt.Sprintf("user:%s", userID)`
- Try `cache.Get(key)` first
- If found (no error): unmarshal JSON and return
- If not found (redis.Nil error):
  - Fetch from MongoDB
  - Marshal to JSON
  - Store in cache with `cache.Set(key, json)`
  - Return result

**Cache Invalidation:**
- On update/delete: `cache.Delete(key)`
- Ensures cache stays fresh

**Hints:**
- Check for `redis.Nil` error (key not found)
- Set reasonable TTL (e.g., 5 minutes)
- Cache key naming: use prefixes like `user:`, `post:`

#### Step 4: Redis Data Structures

**What you need to create:**

**Lists (Recent Activity):**
- Use for ordered list of recent items
- `LPush(key, value)` - Add to front
- `LTrim(key, start, stop)` - Keep only N items (e.g., 0-99 for last 100)
- `LRange(key, start, stop)` - Get range of items
- Example: Recent posts, activity feed

**Sorted Sets (Leaderboard):**
- Use for rankings, scored data
- `ZAdd(key, redis.Z{Score: score, Member: userID})` - Add with score
- `ZRevRange(key, start, stop)` - Get top N (descending)
- `ZRevRank(key, member)` - Get member's rank
- `ZScore(key, member)` - Get member's score
- Example: Leaderboards, trending items

**Hashes (User Profile):**
- Use for storing objects with fields
- `HSet(key, field, value)` or `HSet(key, map)` - Set fields
- `HGet(key, field)` - Get single field
- `HGetAll(key)` - Get all fields as map
- Example: User profiles, settings

**Sets (Tags, Categories):**
- `SAdd(key, members...)` - Add members
- `SMembers(key)` - Get all members
- `SIsMember(key, member)` - Check membership
- Example: Tags, unique items

#### Step 5: Session Management

**What you need to create:**

**SessionManager struct:**
- Holds redis client and TTL duration
- Methods: `Create(userID)`, `Get(sessionID)`, `Destroy(sessionID)`

**Create Session:**
- Generate random session ID (32 chars, use crypto/rand)
- Build key: `session:{sessionID}`
- Store as hash with fields: `user_id`, `created_at`
- Use `HSet()` to store data
- Set TTL with `Expire(key, duration)`
- Return session ID

**Get Session:**
- Build key from session ID
- Use `HGet(key, "user_id")` to retrieve user ID
- If found, refresh TTL with `Expire()`
- Return user ID or error

**Destroy Session:**
- Simply `Del(key)`

**Usage Pattern:**
- Login: Create session, return session ID in cookie
- Request: Get session from cookie, validate
- Logout: Destroy session

**Hints:**
- Use HTTP-only secure cookies for session IDs
- Set reasonable TTL (e.g., 24 hours)
- Refresh TTL on each request (sliding expiration)

#### Step 6: Rate Limiting with Redis

**What you need to create:**

**Rate Limit Middleware:**
- Extract client identifier (IP address from `r.RemoteAddr`)
- Build key: `ratelimit:{ip}`
- Use `Incr(key)` to increment counter atomically
- On first request (count == 1), set expiration with `Expire(key, time.Minute)`
- Check if count exceeds limit (e.g., 100)
- If exceeded: return 429 Too Many Requests
- If OK: call next handler

**Algorithm:**
- Fixed window counter
- Each minute gets new window
- Counter resets automatically via TTL

**Advanced Options:**
- Per-user rate limiting (use user ID instead of IP)
- Different limits for different endpoints
- Token bucket algorithm for smoother limiting
- Sliding window with sorted sets

**Hints:**
- `Incr()` is atomic - safe for concurrent requests
- Set TTL immediately on first request
- Consider X-RateLimit headers for clients

#### Step 7: Pub/Sub for Real-time Updates

**What you need to create:**

**PubSub wrapper:**
- `Subscribe(channel, handler)` method
- Use `redis.Subscribe(ctx, channel)` to get pubsub object
- Loop over `pubsub.Channel()` to receive messages
- Call handler function for each message payload
- Run in goroutine for async receiving

**Publish method:**
- `Publish(channel, message)` method
- Use `redis.Publish(ctx, channel, message)`
- Returns number of subscribers who received message

**Usage Pattern:**
- Publisher: After creating post, publish notification
- Subscriber: Start goroutine listening on channel
- Handler: Process messages (send emails, push notifications, etc.)

**Use Cases:**
- New post notifications
- Real-time chat
- System events
- Cache invalidation across servers

**Hints:**
- Pub/Sub is fire-and-forget (no message persistence)
- Subscriber must be running to receive messages
- For reliable messaging, use Redis Streams instead
- Can have multiple subscribers on same channel

### Challenge Yourself

1. **MongoDB Aggregation**: Complex analytics queries
2. **Transactions**: Multi-document ACID transactions
3. **Change Streams**: Real-time data changes from MongoDB
4. **Redis Streams**: Message queue with consumer groups
5. **Geospatial**: Location-based queries with MongoDB
6. **Full-Text Search**: MongoDB text indexes
7. **Redis Lua Scripts**: Atomic complex operations
8. **Sharding**: Distribute data across multiple servers
9. **Replica Sets**: High availability for MongoDB
10. **Redis Cluster**: Distributed Redis

### Common Gotchas

**Problem**: MongoDB connection timeout
**Fix**: Check MongoDB is running, firewall settings, connection string

**Problem**: Redis connection refused
**Fix**: Check Redis is running, use correct port (6379)

**Problem**: Cache stampede (thundering herd)
**Fix**: Use lock/mutex when populating cache

**Problem**: Stale cache after updates
**Fix**: Invalidate cache on write operations

**Problem**: Memory issues with large MongoDB results
**Fix**: Use cursors with batching, pagination

**Problem**: Redis memory full
**Fix**: Set maxmemory, configure eviction policy

---

## Project 3B: OpenSearch / Elasticsearch Integration

### Prerequisites & Requirements

**Before Starting:**
- **Completed**: NoSQL Database Integration project (recommended)
- **Equivalent Experience**:
  - REST API development
  - JSON handling
  - Database queries

**Knowledge Prerequisites:**
- **Must Know**:
  - JSON structures
  - HTTP requests
  - Basic database concepts
  - Go structs and interfaces
- **Should Know**:
  - Full-text search concepts
  - Indexing basics
  - Query languages
- **Will Learn**:
  - OpenSearch/Elasticsearch architecture
  - Document indexing
  - Full-text search queries
  - Aggregations and analytics
  - Relevance scoring
  - Autocomplete and suggestions
  - Faceted search

**New Go Concepts:**
1. **opensearch.Client**: OpenSearch driver
2. **Bulk Operations**: Batch indexing
3. **Query DSL**: Domain-specific language for queries
4. **Scroll API**: Pagination for large result sets
5. **Analyzers**: Text processing pipelines

**External Dependencies:**
- **Required**:
  - `github.com/opensearch-project/opensearch-go/v2` - OpenSearch client
  - OR `github.com/elastic/go-elasticsearch/v8` - Elasticsearch client

**System Requirements:**
- **OS**: Linux, macOS, Windows
- **RAM**: 4GB minimum (8GB+ recommended for OpenSearch/Elasticsearch)
- **Disk**: 2GB+ for indices
- **Java**: JDK 11+ (required for OpenSearch/Elasticsearch)

**What to Install:**

**OpenSearch Installation:**
```bash
# macOS (using Docker - easiest)
docker pull opensearchproject/opensearch:latest
docker run -d -p 9200:9200 -p 9600:9600 \
  -e "discovery.type=single-node" \
  -e "OPENSEARCH_INITIAL_ADMIN_PASSWORD=Admin@123" \
  --name opensearch \
  opensearchproject/opensearch:latest

# Linux (Docker)
sudo docker pull opensearchproject/opensearch:latest
sudo docker run -d -p 9200:9200 -p 9600:9600 \
  -e "discovery.type=single-node" \
  -e "OPENSEARCH_INITIAL_ADMIN_PASSWORD=Admin@123" \
  --name opensearch \
  opensearchproject/opensearch:latest

# Verify OpenSearch
curl -X GET "https://localhost:9200" -ku admin:Admin@123
# Should return cluster info

# Alternative: Direct installation
# Download from: https://opensearch.org/downloads.html
```

**Elasticsearch Installation (Alternative):**
```bash
# macOS
brew tap elastic/tap
brew install elastic/tap/elasticsearch-full
brew services start elastic/tap/elasticsearch-full

# Linux
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
echo "deb https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list
sudo apt update
sudo apt install elasticsearch
sudo systemctl start elasticsearch

# Docker (easiest)
docker pull docker.elastic.co/elasticsearch/elasticsearch:8.11.0
docker run -d -p 9200:9200 -e "discovery.type=single-node" \
  -e "xpack.security.enabled=false" \
  --name elasticsearch \
  docker.elastic.co/elasticsearch/elasticsearch:8.11.0

# Verify
curl http://localhost:9200
```

**Go Dependencies:**
```bash
mkdir search-app
cd search-app
go mod init github.com/yourusername/search-app

# OpenSearch
go get github.com/opensearch-project/opensearch-go/v2

# OR Elasticsearch
go get github.com/elastic/go-elasticsearch/v8

go mod tidy
```

**Testing Setup:**
```bash
# Test OpenSearch connection
cat > test_opensearch.go << 'EOF'
package main
import (
    "crypto/tls"
    "fmt"
    "net/http"
    opensearch "github.com/opensearch-project/opensearch-go/v2"
)
func main() {
    client, err := opensearch.NewClient(opensearch.Config{
        Transport: &http.Transport{
            TLSClientConfig: &tls.Config{InsecureSkipVerify: true},
        },
        Addresses: []string{"https://localhost:9200"},
        Username:  "admin",
        Password:  "Admin@123",
    })
    if err != nil {
        panic(err)
    }

    res, err := client.Info()
    if err != nil {
        panic(err)
    }
    defer res.Body.Close()

    fmt.Println("OpenSearch connection successful!")
}
EOF

go run test_opensearch.go
rm test_opensearch.go
```

**Environment Configuration:**
```bash
cat > .env << 'EOF'
# OpenSearch
OPENSEARCH_URL=https://localhost:9200
OPENSEARCH_USERNAME=admin
OPENSEARCH_PASSWORD=Admin@123

# OR Elasticsearch
ELASTICSEARCH_URL=http://localhost:9200

# Index settings
INDEX_NAME=products
BULK_SIZE=500

# Server
PORT=8080
EOF

echo ".env" >> .gitignore
```

**Estimated Time:**
- OpenSearch setup: 1-2 hours
- Basic indexing: 3-4 hours
- Search queries: 4-6 hours
- Aggregations: 3-4 hours
- Autocomplete: 2-3 hours
- Faceted search: 3-4 hours
- REST API: 4-6 hours
- **Total**: 20-30 hours

**Files You'll Create:**
- `main.go` - 100-150 lines
- `config/config.go` - 60-100 lines
- `search/client.go` - 150-250 lines
- `search/index.go` - 200-300 lines
- `search/query.go` - 250-400 lines
- `models/product.go` - 80-120 lines
- `handlers/search.go` - 200-300 lines

### Overview
Build a full-text search application using OpenSearch (or Elasticsearch). Implement product search with autocomplete, filters, facets, and analytics. Learn modern search engine technology.

### What You'll Learn
- **Document Indexing**: Store and index documents
- **Full-Text Search**: Relevance-based queries
- **Query DSL**: Complex search queries
- **Aggregations**: Analytics and facets
- **Analyzers**: Text processing (tokenization, stemming)
- **Autocomplete**: Search-as-you-type
- **Faceted Search**: Filter by categories
- **Highlighting**: Highlight search terms in results
- **Relevance Tuning**: Boost fields, custom scoring

### Core Features
1. Index products (name, description, category, price)
2. Full-text search across multiple fields
3. Autocomplete/suggestions
4. Faceted search (filters by category, price range)
5. Sorting (relevance, price, date)
6. Pagination
7. Aggregations (category counts, price stats)
8. Highlighting search terms
9. Fuzzy search (typo tolerance)
10. REST API for search

### Project Structure
```
search-app/
├── main.go
├── config/
│   └── config.go           # Configuration
├── search/
│   ├── client.go           # OpenSearch client
│   ├── index.go            # Indexing operations
│   ├── query.go            # Search queries
│   └── aggregation.go      # Aggregations
├── models/
│   ├── product.go          # Product model
│   └── search_result.go    # Search results
└── handlers/
    └── search.go           # HTTP handlers
```

### Implementation Guide

#### Step 1: Create Index and Mappings

**Key Concepts:**
- **Index**: Like a database table
- **Document**: A JSON record
- **Mapping**: Schema definition (field types, analyzers)

**What you need to create:**

**Index Settings JSON:**
- `settings` section:
  - `number_of_shards`: How many shards (1 for development)
  - `number_of_replicas`: Backup copies (0 for development)
  - `analysis`: Custom analyzers for autocomplete
    - Define `autocomplete` analyzer with `edge_ngram` filter
    - `edge_ngram`: min_gram=2, max_gram=20 for partial matching

**Mappings Section:**
- Define field types in `properties`:
  - `name`: type `text` with autocomplete analyzer
    - Add `fields.keyword` for exact matching
  - `description`: type `text` for full-text search
  - `category`: type `keyword` for filtering
  - `price`: type `float`
  - `stock`: type `integer`
  - `created_at`: type `date`

**CreateIndex function:**
- Build JSON mapping string
- Call `client.Indices.Create(indexName, options)`
- Pass mapping in body

**Hints:**
- `text` type: Full-text search, analyzed
- `keyword` type: Exact match, good for aggregations/filters
- `edge_ngram`: For autocomplete (partial word matching)
- Multi-fields: name.keyword for both searching and exact match

#### Step 2: Index Documents

**What you need to create:**

**Product Model:**
- Struct with fields: ID, Name, Description, Category, Price, Stock, CreatedAt
- Use JSON tags for field names

**IndexProduct function:**
- Marshal product to JSON
- Call `client.Index(indexName, jsonReader, options)`
- Options: `WithDocumentID(id)`, `WithRefresh("true")` for immediate availability
- Handle response and errors

**Bulk Indexing (Better Performance):**
- For indexing many documents at once
- Format: alternating action/document lines
- Action line: `{"index": {"_index": "products", "_id": "123"}}`
- Document line: actual JSON document
- Build buffer with all documents
- Call `client.Bulk(bufferReader)`
- Much faster than individual Index calls

**Hints:**
- Single index: use for real-time updates
- Bulk index: use for importing large datasets
- `WithRefresh("true")`: makes document searchable immediately (slower)
- `WithRefresh("false")`: eventual consistency (faster)
- Bulk API can handle thousands of documents in one request

#### Step 3: Basic Search Queries

**What you need to create:**

**SearchParams struct:**
- Fields: Query, Category, MinPrice, MaxPrice, Page, Size, SortBy

**Build Query JSON:**
- Root `query` with `bool` clause:
  - `must`: Required matches (affects relevance score)
    - Use `multi_match` to search across fields
    - Specify `fields`: ["name^2", "description"] (^2 = boost)
    - Add `fuzziness: "AUTO"` for typo tolerance
  - `filter`: Filters (no score impact, faster)
    - Add `term` query for category: `{"term": {"category": value}}`
    - Add `range` query for price: `{"range": {"price": {"gte": min, "lte": max}}}`

**Pagination:**
- `from`: Page offset (page * size)
- `size`: Results per page

**Sorting:**
- Add `sort` array with field and order
- Example: `[{"price": {"order": "asc"}}]`

**Highlighting:**
- Add `highlight` section with fields to highlight
- Results will include highlighted snippets

**Execute Search:**
- Marshal query to JSON
- Call `client.Search(WithIndex(), WithBody())`
- Decode response JSON

**Query DSL Concepts:**
- `multi_match`: Search across multiple fields
- `^2`: Boost field (name is 2x more important)
- `fuzziness`: Typo tolerance (AUTO adjusts based on word length)
- `bool`: Combine queries (must, should, filter, must_not)
- `must`: AND condition, affects relevance score
- `filter`: Filter results, no score impact, cached
- `term`: Exact match for keywords
- `range`: Numeric/date ranges (gte, lte, gt, lt)

#### Step 4: Autocomplete

**What you need to create:**

**Autocomplete function:**
- Build query with `match` on name field
- Set `size` to limit suggestions (e.g., 10)
- Use `_source` to return only name field (faster)
- Execute search
- Extract names from hits
- Return as string array

**How Autocomplete Works:**
- Uses `edge_ngram` analyzer (configured in Step 1)
- Indexes partial words: "laptop" → "la", "lap", "lapt", "lapto", "laptop"
- Query "lap" matches all products starting with "lap"
- Returns results fast (prefix matching)

**Improvements:**
- Use `completion` suggester for better performance
- Add `prefix` query for exact prefix matching
- Sort by popularity or relevance
- Return additional fields (category, image)

**Hints:**
- Limit results to 5-10 for UI
- Add debouncing on frontend (wait 300ms after typing)
- Cache popular queries

#### Step 5: Aggregations (Facets)

**What you need to create:**

**Facets function:**
- Build query with search terms
- Set `size: 0` (don't return documents, only aggregations)
- Add `aggs` section with multiple aggregations:

**Terms Aggregation (Categories):**
- `"categories": {"terms": {"field": "category", "size": 20}}`
- Groups by category, returns top 20
- Shows count per category

**Range Aggregation (Price Ranges):**
- `"price_ranges": {"range": {"field": "price", "ranges": [...]}}`
- Define ranges: 0-50, 50-100, 100-200, 200+
- Shows count in each price bucket

**Stats Aggregation (Price Statistics):**
- `"price_stats": {"stats": {"field": "price"}}`
- Returns min, max, avg, sum, count

**Parse Results:**
- Response has `aggregations` section
- Each aggregation has `buckets` array
- Each bucket has `key` and `doc_count`

**Usage in UI:**
- Show categories with counts as checkboxes
- Show price ranges as filters
- Display min/max price for slider

**Aggregation Types:**
- `terms`: Group by field (like SQL GROUP BY)
- `range`: Numeric/date ranges
- `stats`: Min, max, avg, sum statistics
- `date_histogram`: Time-based grouping
- `nested`: Aggregate nested objects

**Hints:**
- Aggregations work on original query results
- Can combine multiple aggregations
- Use `keyword` fields for terms aggregations (not `text`)

### Challenge Yourself

1. **Synonyms**: Configure synonym analyzer
2. **Did You Mean**: Spelling suggestions
3. **More Like This**: Find similar products
4. **Geospatial Search**: Location-based search
5. **Boosting**: Custom relevance scoring
6. **Percolate**: Reverse search (saved queries)
7. **Nested Objects**: Complex document structures
8. **Parent-Child**: Relationships between documents
9. **Machine Learning**: Anomaly detection, recommendations
10. **Multi-tenancy**: Search across multiple indices

### Common Gotchas

**Problem**: Connection refused
**Fix**: Ensure OpenSearch/Elasticsearch is running, check port (9200)

**Problem**: Mapping conflicts
**Fix**: Can't change existing field types, need to reindex

**Problem**: Too many results
**Fix**: Use pagination, increase page size limit if needed

**Problem**: Slow queries
**Fix**: Add filters (faster than queries), use caching, optimize mappings

**Problem**: Memory issues
**Fix**: Increase JVM heap size in OpenSearch config

**Problem**: Inaccurate autocomplete
**Fix**: Tune edge_ngram settings, use phrase suggestions

---

## Project 3: File Sync Tool

### Prerequisites & Requirements

**Before Starting:**
- **Completed**:
  - REST API project (database operations)
  - Web Scraper project (concurrency patterns)
  - OR significant Go experience with networking
- **Equivalent Experience**:
  - Built client-server applications
  - Worked with file I/O
  - Network programming (TCP/HTTP)
  - Concurrent programming with channels

**Knowledge Prerequisites:**
- **Must Know**:
  - File I/O operations (reading, writing, seeking)
  - File system operations (walk, stat, permissions)
  - Goroutines, channels, select statements
  - Mutexes and atomic operations
  - TCP/HTTP networking basics
  - Hashing algorithms (purpose and usage)
  - Error handling patterns
- **Should Know**:
  - Binary serialization (encoding/gob, JSON)
  - Buffered I/O for large files
  - File system events (create, modify, delete)
  - Network protocols design
  - Conflict resolution strategies
- **Will Learn**:
  - File system watching with fsnotify
  - Delta synchronization algorithms
  - Chunked file transfers
  - Binary protocol design
  - Merkle trees for change detection
  - Conflict detection and resolution
  - Incremental hashing
  - Network state management

**New Go Concepts:**
1. **fsnotify**: File system event notifications
2. **io.ReaderAt/WriterAt**: Random access I/O
3. **crypto/hash**: Cryptographic hashing (SHA256, BLAKE2b)
4. **encoding/gob**: Binary serialization for Go types
5. **net.Conn**: Low-level TCP connections
6. **io.Copy with Buffers**: Efficient large file transfers
7. **filepath.Walk**: Directory tree traversal
8. **os.FileInfo**: File metadata inspection
9. **sync.WaitGroup**: Coordinating goroutines
10. **Context Cancellation**: Graceful shutdown

**External Dependencies:**
- **Required**:
  - `github.com/fsnotify/fsnotify` - File system notifications
  - `github.com/zeebo/blake3` or `golang.org/x/crypto/blake2b` - Fast hashing
- **Optional**:
  - `github.com/gorilla/websocket` - WebSocket support (alternative to TCP)
  - `github.com/pkg/sftp` - SFTP support for cloud sync
  - `github.com/aws/aws-sdk-go-v2` - AWS S3 integration
  - `google.golang.org/grpc` - gRPC for RPC protocol
  - `github.com/vmihailenco/msgpack` - Alternative serialization

**System Requirements:**
- **OS**: macOS, Linux, Windows (fsnotify works on all)
- **RAM**: 4GB minimum (8GB for large file syncing)
- **Disk**:
  - 1GB+ free space for testing
  - SSD recommended for better performance
- **Network**:
  - LAN access for machine-to-machine sync
  - Stable connection for cloud sync
- **Filesystem**:
  - UNIX permissions understanding (macOS/Linux)
  - Windows ACL knowledge (Windows)

**What to Install:**
```bash
# 1. Create project
mkdir file-sync-tool
cd file-sync-tool
go mod init github.com/yourusername/file-sync

# 2. Install dependencies
go get github.com/fsnotify/fsnotify
go get github.com/zeebo/blake3  # Fast hashing
# OR
go get golang.org/x/crypto/blake2b

# Optional dependencies
go get github.com/gorilla/websocket  # WebSocket alternative
go get github.com/vmihailenco/msgpack/v5  # Alternative to gob

# 3. Verify
go mod tidy
cat go.mod
```

**Testing Tools:**
```bash
# Create test directories
mkdir -p ~/sync-test/{dir1,dir2}

# Watch filesystem events
if command -v inotifywait &> /dev/null; then
    # Linux
    inotifywait -m ~/sync-test/dir1
elif command -v fswatch &> /dev/null; then
    # macOS (install: brew install fswatch)
    fswatch ~/sync-test/dir1
else
    echo "No filesystem watch tool installed"
fi

# Monitor network connections
netstat -an | grep :8080  # Check if port is listening
lsof -i :8080  # See what's using port 8080

# Test TCP connection
nc -zv localhost 8080  # Check if server is reachable

# Monitor file changes
watch -n 1 'ls -lR ~/sync-test/dir1'  # Linux/macOS
```

**Environment Configuration:**
```bash
cat > .env << 'EOF'
# Server mode settings
SERVER_MODE=false  # true for server, false for client
SERVER_HOST=0.0.0.0
SERVER_PORT=8080

# Client mode settings
REMOTE_HOST=localhost
REMOTE_PORT=8080

# Sync settings
WATCH_DIRECTORY=./sync-folder
SYNC_INTERVAL_SECONDS=30  # Full sync interval
CHUNK_SIZE_MB=5  # File chunk size
MAX_CONCURRENT_TRANSFERS=3

# Hashing
HASH_ALGORITHM=blake3  # blake3, blake2b, or sha256
USE_INCREMENTAL_HASH=true

# Conflict resolution
CONFLICT_STRATEGY=newest  # newest, ask, rename

# Performance
BUFFER_SIZE_KB=64
MAX_MEMORY_MB=512

# Logging
LOG_LEVEL=info  # debug, info, warn, error
LOG_FILE=./sync.log
EOF

echo ".env" >> .gitignore
echo "sync-folder/" >> .gitignore
echo "*.log" >> .gitignore
```

**Testing Filesystem Notifications:**
```bash
# Test fsnotify
cat > test_fsnotify.go << 'EOF'
package main
import (
    "fmt"
    "log"
    "github.com/fsnotify/fsnotify"
)
func main() {
    watcher, err := fsnotify.NewWatcher()
    if err != nil {
        log.Fatal(err)
    }
    defer watcher.Close()

    go func() {
        for {
            select {
            case event := <-watcher.Events:
                fmt.Println("Event:", event)
            case err := <-watcher.Errors:
                fmt.Println("Error:", err)
            }
        }
    }()

    err = watcher.Add(".")
    if err != nil {
        log.Fatal(err)
    }
    fmt.Println("Watching current directory. Make changes...")
    select {}  // Block forever
}
EOF

go run test_fsnotify.go &
PID=$!
sleep 2

# Create test events
echo "test" > test.txt
rm test.txt

kill $PID
rm test_fsnotify.go
```

**Testing File Hashing:**
```bash
cat > test_hashing.go << 'EOF'
package main
import (
    "crypto/sha256"
    "encoding/hex"
    "fmt"
    "io"
    "os"
    "time"
)
func hashFile(path string) (string, error) {
    f, err := os.Open(path)
    if err != nil {
        return "", err
    }
    defer f.Close()

    h := sha256.New()
    if _, err := io.Copy(h, f); err != nil {
        return "", err
    }

    return hex.EncodeToString(h.Sum(nil)), nil
}

func main() {
    // Create test file
    data := make([]byte, 10*1024*1024) // 10MB
    os.WriteFile("testfile.bin", data, 0644)

    start := time.Now()
    hash, err := hashFile("testfile.bin")
    if err != nil {
        panic(err)
    }
    fmt.Printf("Hash: %s (took %v)\n", hash[:16], time.Since(start))

    os.Remove("testfile.bin")
}
EOF

go run test_hashing.go
rm test_hashing.go
```

**Testing TCP Connection:**
```bash
# Simple TCP server test
cat > test_tcp_server.go << 'EOF'
package main
import (
    "fmt"
    "net"
)
func main() {
    ln, err := net.Listen("tcp", ":8080")
    if err != nil {
        panic(err)
    }
    defer ln.Close()
    fmt.Println("Server listening on :8080")

    conn, err := ln.Accept()
    if err != nil {
        panic(err)
    }
    fmt.Println("Client connected")
    conn.Write([]byte("Hello from server\n"))
    conn.Close()
}
EOF

go run test_tcp_server.go &
SERVER_PID=$!
sleep 1

# Simple TCP client test
cat > test_tcp_client.go << 'EOF'
package main
import (
    "fmt"
    "io"
    "net"
)
func main() {
    conn, err := net.Dial("tcp", "localhost:8080")
    if err != nil {
        panic(err)
    }
    defer conn.Close()
    data, _ := io.ReadAll(conn)
    fmt.Printf("Received: %s", data)
}
EOF

go run test_tcp_client.go

kill $SERVER_PID
rm test_tcp_server.go test_tcp_client.go
```

**Estimated Time:**
- Setup and dependencies: 1-2 hours
- File watching: 4-6 hours
- File hashing and comparison: 4-6 hours
- TCP server/client: 4-6 hours
- Binary protocol design: 4-6 hours
- File transfer (chunked): 6-8 hours
- Conflict detection: 4-6 hours
- Conflict resolution UI: 3-5 hours
- Delta sync algorithm: 6-10 hours (advanced)
- Testing and debugging: 8-12 hours
- **Total**: 45-70 hours

**Files You'll Create:**
- `main.go` - 150-200 lines
- `config/config.go` - 80-120 lines
- `watcher/watcher.go` - 200-300 lines
- `hasher/hasher.go` - 150-250 lines
- `hasher/merkle.go` - 150-200 lines (for merkle trees)
- `syncer/syncer.go` - 300-400 lines
- `syncer/protocol.go` - 200-300 lines
- `syncer/chunked_transfer.go` - 200-300 lines
- `server/server.go` - 200-300 lines
- `client/client.go` - 200-300 lines
- `conflict/resolver.go` - 150-250 lines
- `models/file.go` - 100-150 lines
- `models/sync_state.go` - 80-120 lines
- `database/database.go` - 150-200 lines
- `utils/network.go` - 100-150 lines

**New Challenges:**
- **File System Watching**: Handling rapid events, debouncing
- **Efficient Hashing**: Incremental hashing for large files
- **Network Protocol**: Designing efficient binary protocol
- **Chunked Transfer**: Resuming interrupted transfers
- **Conflict Detection**: Detecting simultaneous edits
- **Conflict Resolution**: UI and strategies for handling conflicts
- **Delta Sync**: Sending only changed portions (like rsync)
- **Memory Management**: Handling large files without exhausting RAM
- **Race Conditions**: File modified while syncing
- **Cross-Platform**: Different path separators, permissions

**Testing Your Setup:**
```bash
# Full integration test
mkdir -p test-sync/{client,server}

# Create test files
for i in {1..5}; do
    echo "File $i content" > test-sync/client/file$i.txt
done

# Create subdirectories
mkdir -p test-sync/client/subdir
echo "Nested file" > test-sync/client/subdir/nested.txt

# Create a large file
dd if=/dev/urandom of=test-sync/client/largefile.bin bs=1M count=10

# List all files with sizes
find test-sync/client -type f -exec ls -lh {} \;

# Cleanup
rm -rf test-sync
```

**Common Setup Issues:**

1. **fsnotify events not firing**:
   - Check if directory exists and is accessible
   - On Linux, check inotify limits: `cat /proc/sys/fs/inotify/max_user_watches`
   - Increase if needed: `sudo sysctl fs.inotify.max_user_watches=524288`
   - macOS/Windows usually don't have limits

2. **"too many open files" error**:
   - Check limit: `ulimit -n`
   - Increase: `ulimit -n 4096` (temporary) or edit `/etc/security/limits.conf` (permanent)
   - Always close file handles: `defer f.Close()`

3. **Permission denied errors**:
   - Ensure read/write permissions on sync directories
   - Run with appropriate user permissions
   - On Windows, check if files are locked by another process

4. **Port already in use**:
   - Check what's using port: `lsof -i :8080` (macOS/Linux) or `netstat -ano | findstr :8080` (Windows)
   - Kill process or use different port
   - Set `SO_REUSEADDR` socket option

5. **Hash mismatches**:
   - Ensure same hash algorithm on both sides
   - Check for text mode vs binary mode file reads
   - Verify file wasn't modified during hashing

6. **Slow file transfers**:
   - Increase chunk size: 5-10MB works well
   - Increase buffer size: 64KB or 128KB
   - Use io.Copy with custom buffer
   - Check network bandwidth

7. **Race conditions**:
   - File modified while being hashed: use file locking or copy
   - Use `sync.Mutex` to protect shared state
   - Consider using channels for coordination

**Performance Optimization:**

**Hashing:**
```go
// Use BLAKE3 (fastest)
import "github.com/zeebo/blake3"

// Read file in larger chunks
buf := make([]byte, 64*1024) // 64KB buffer
io.CopyBuffer(hasher, file, buf)

// Skip hashing if mod time unchanged
if newModTime.Equal(oldModTime) {
    return cachedHash, nil
}
```

**File Transfer:**
```go
// Send files concurrently (but limit concurrency)
semaphore := make(chan struct{}, 3) // Max 3 concurrent

// Use larger chunks for large files
chunkSize := 5 * 1024 * 1024 // 5MB

// Compress before sending (optional)
import "compress/gzip"
gzipWriter := gzip.NewWriter(conn)
```

**Network:**
```go
// Enable TCP keepalive
if tcpConn, ok := conn.(*net.TCPConn); ok {
    tcpConn.SetKeepAlive(true)
    tcpConn.SetKeepAlivePeriod(30 * time.Second)
}

// Set read/write deadlines
conn.SetDeadline(time.Now().Add(30 * time.Second))
```

**File System Watching:**
```go
// Debounce rapid events
timer := time.NewTimer(100 * time.Millisecond)
defer timer.Stop()

for {
    select {
    case event := <-watcher.Events:
        timer.Reset(100 * time.Millisecond)
    case <-timer.C:
        // Process accumulated events
    }
}

// Ignore temp files
if strings.HasSuffix(path, ".swp") ||
   strings.HasSuffix(path, "~") ||
   strings.HasPrefix(filepath.Base(path), ".") {
    continue  // Skip
}
```

**Security Considerations:**
- Validate file paths (prevent directory traversal)
- Limit file sizes
- Authenticate connections (add token/password)
- Encrypt network traffic (TLS)
- Verify hashes after transfer
- Sandbox sync directory (don't allow escaping)

**Learning Resources:**
- fsnotify documentation: https://github.com/fsnotify/fsnotify
- rsync algorithm: https://rsync.samba.org/tech_report/
- BLAKE3 hashing: https://github.com/BLAKE3-team/BLAKE3
- TCP programming in Go: https://pkg.go.dev/net
- Binary protocols: https://en.wikipedia.org/wiki/Binary_protocol

### Overview
Build a Dropbox-like file synchronization tool that watches directories and syncs changes between machines or to cloud storage. Teaches file system watching, hashing, network programming, and conflict resolution.

### What You'll Learn
- **File System Watching**: Monitor directories for changes
- **File Hashing**: Detect changes efficiently with checksums
- **Network Programming**: TCP/WebSocket communication
- **Binary Protocols**: Efficient data serialization
- **Conflict Resolution**: Handle simultaneous edits
- **Chunked Transfer**: Send large files in pieces
- **Delta Sync**: Only send changed portions
- **Encryption**: Secure file transmission

### Core Features
1. Watch local directory for file changes
2. Detect changes via file hashing (MD5/SHA256)
3. Sync changes to remote server or peer
4. Handle conflicts (last-write-wins, manual resolution, merge)
5. Resume interrupted transfers
6. Incremental sync (only changed files)
7. Compression for transfer
8. Optional encryption

### Project Structure
```
file-sync/
├── main.go
├── watcher/
│   └── watcher.go         # File system monitoring
├── hasher/
│   └── hasher.go          # File hashing and comparison
├── syncer/
│   ├── client.go          # Sync client
│   ├── server.go          # Sync server
│   └── protocol.go        # Sync protocol definition
├── storage/
│   ├── local.go           # Local file operations
│   └── remote.go          # Remote storage abstraction
├── models/
│   ├── file.go            # File metadata
│   └── syncstate.go       # Sync state tracking
└── go.mod
```

### Implementation Guide

#### Step 1: Setup

```bash
mkdir file-sync
cd file-sync
go mod init github.com/yourusername/file-sync

go get github.com/fsnotify/fsnotify        # File watching
go get github.com/gorilla/websocket         # WebSocket communication
go get golang.org/x/crypto/blake2b         # Fast hashing
go get github.com/klauspost/compress/zstd  # Compression
```

#### Step 2: File Hashing (`hasher/hasher.go`)

**Key Concepts:**
- **Hashing**: Generate unique fingerprint for file contents
- **Chunking**: Process large files in blocks
- **Merkle Trees**: Hierarchical hashing for change detection

**What you need to create:**
- `FileHash` struct: Path, Hash, Size, ModTime
- `HashFile(path)` - Calculate hash of entire file
- `HashDirectory(path)` - Hash all files recursively, return map
- `CompareHashes(local, remote)` - Find added/modified/deleted files
- `ChunkFile(path, chunkSize)` - Split file into chunks with individual hashes

**Learning Notes:**
- **BLAKE2b**: Faster than SHA256, good for file hashing
- **Incremental Hashing**: Hash file in chunks to save memory
- **Modification Time**: Quick check before hashing

**Hints:**
- Read file in buffers: `io.Copy(hasher, file)`
- Use `filepath.Walk()` to traverse directory tree
- Compare mod times first (cheaper than hashing)
- Store hashes in database or JSON file for persistence
- For large files, use chunk hashing to detect partial changes

#### Step 3: File Watching (`watcher/watcher.go`)

**What you need to create:**
- `FileWatcher` struct with fsnotify watcher and event queue
- `Watch(directory)` - Start watching directory recursively
- Event handling:
  - CREATE: New file added
  - WRITE: File modified
  - REMOVE: File deleted
  - RENAME: File moved
- Debounce rapid events (multiple writes during save)
- Queue events for processing by syncer

**Hints:**
- Watch all subdirectories: walk tree and add each to watcher
- Debounce: Wait 100ms after event before processing
- Ignore temp files (`.swp`, `.tmp`, `~`)
- Handle directory creation: recursively watch new directories

#### Step 4: Sync Protocol (`syncer/protocol.go`)

**Key Concepts:**
- **Message Types**: Define protocol messages (SYNC_REQUEST, FILE_DATA, ACK, etc.)
- **Binary Encoding**: Efficient serialization (gob, protobuf, or custom)
- **Flow Control**: Handle bandwidth and buffering

**What you need to create:**
- Message types:
  - `SyncRequest`: Request to sync directory
  - `FileList`: List of files with hashes
  - `FileDelta`: Which files need transfer
  - `FileChunk`: Chunk of file data
  - `FileComplete`: File transfer complete
  - `Error`: Error message
- Encoding/decoding functions for each message type
- Protocol state machine

**Hints:**
- Use `encoding/gob` for simple binary encoding
- Each message: `[length:4bytes][type:1byte][payload:N bytes]`
- Include sequence numbers for ordering
- Add checksums to verify data integrity

#### Step 5: Sync Server (`syncer/server.go`)

**What you need to create:**
- TCP or WebSocket server listening for connections
- Handle multiple clients concurrently
- For each client:
  - Receive file list with hashes
  - Compare with server's file list
  - Send delta (files client needs)
  - Receive files from client (bidirectional sync)
  - Store files in designated directory
- Conflict detection and resolution
- Authentication (optional: token-based)

**Hints:**
- Use goroutine per client connection
- Store files with temporary names during transfer
- Verify hash after receiving file
- Atomic rename after complete transfer
- Use mutex to protect file list during concurrent access

#### Step 6: Sync Client (`syncer/client.go`)

**What you need to create:**
- Connect to sync server (TCP/WebSocket)
- Send local file list with hashes
- Receive delta from server
- Request missing files
- Send changed local files
- Apply received files to local directory
- Handle connection drops and resume

**Hints:**
- Maintain sync state in database: which files synced, when
- Resume: Check which chunks received, request remaining
- Retry with exponential backoff on connection failure
- Verify received files against expected hash

#### Step 7: Conflict Resolution

**What you need to create:**
- Detect conflicts: same file modified on both sides
- Resolution strategies:
  - **Last-Write-Wins**: Keep file with newest timestamp
  - **Keep Both**: Rename one file (e.g., `file.conflict.txt`)
  - **Manual**: Prompt user to choose
  - **Merge**: Attempt automatic merge for text files (like git)
- Track conflict history

**Hints:**
- Compare timestamps and hashes
- For merge: use diff libraries or line-by-line comparison
- Store conflicts in queue for user review
- Provide API/CLI to resolve pending conflicts

#### Step 8: Main Application

**What you need to create:**
- CLI commands:
  - `file-sync watch <dir>` - Watch and sync directory
  - `file-sync server` - Start sync server
  - `file-sync status` - Show sync status
  - `file-sync resolve <conflict>` - Resolve conflict
- Configuration file for:
  - Watch directories
  - Server address
  - Sync interval
  - Conflict resolution strategy
  - Ignored patterns (like .gitignore)

### Build and Run

```bash
# Start server on machine 1
./file-sync server --port 8080

# On machine 2, sync a directory
./file-sync watch ~/Documents --remote server1.example.com:8080

# Check status
./file-sync status

# Resolve conflicts
./file-sync conflicts list
./file-sync conflicts resolve file.txt --keep local
```

### Challenge Yourself

1. **Encryption**: Encrypt files before transfer (AES-256)
2. **Compression**: Compress during transfer to save bandwidth
3. **Delta Sync**: Only send changed bytes (rsync algorithm)
4. **P2P Mode**: Direct peer-to-peer sync without central server
5. **Cloud Storage**: Sync to S3, Google Drive, or Dropbox
6. **Version History**: Keep old versions of files
7. **Selective Sync**: Choose which folders to sync
8. **Mobile App**: iOS/Android app for mobile access
9. **File Sharing**: Share files with links (like Dropbox)
10. **Real-Time Collaboration**: Multiple users editing simultaneously

### Common Gotchas

**Problem**: Race condition when file changes during hashing
**Fix**: Copy file to temp location, then hash

**Problem**: Running out of memory with large files
**Fix**: Stream files in chunks, don't load entirely into memory

**Problem**: Symlink loops causing infinite recursion
**Fix**: Track visited inodes, skip symlinks, or limit depth

**Problem**: Partial writes leaving corrupted files
**Fix**: Write to temp file, then atomic rename

**Problem**: Network interruption mid-transfer
**Fix**: Track transferred chunks, resume from last chunk

---

## Next Steps - Intermediate Projects

After these three intermediate projects, you'll have learned:

✅ Database integration and SQL
✅ Authentication and authorization (JWT)
✅ API design and middleware patterns
✅ Concurrent programming patterns
✅ Network protocols and communication
✅ File system operations and monitoring
✅ Error handling and retry logic
✅ Production-ready code structure

---

## Project 7: Shell/Terminal Implementation

### Prerequisites & Requirements

**Before Starting:**
- **Completed**: All basic projects and some intermediate projects
- **Equivalent Experience**: CLI tools, process management, I/O

**Knowledge Prerequisites:**
- **Must Know**:
  - os/exec package
  - String parsing
  - Environment variables
  - Process management
- **Should Know**:
  - Shell concepts (pipes, redirects, variables)
  - UNIX commands
  - Signal handling
- **Will Learn**:
  - Command parsing and execution
  - Pipe implementation
  - I/O redirection
  - Job control (background processes)
  - Shell scripting basics
  - TTY and terminal control

**New Go Concepts:**
1. **os/exec.Cmd**: Execute external commands
2. **io.Pipe**: Create pipes between commands
3. **cmd.StdinPipe/StdoutPipe**: Connect command I/O
4. **os.Environ**: Environment variables
5. **filepath.Glob**: Pattern matching for wildcards
6. **syscall.Exec**: Replace process (exec family)

**External Dependencies:**
- Standard library only!
- **Optional**:
  - `github.com/chzyer/readline` - Better input editing
  - `github.com/fatih/color` - Colored output

**What to Install:**
```bash
mkdir myshell
cd myshell
go mod init github.com/yourusername/myshell

# Optional dependencies
go get github.com/chzyer/readline
go get github.com/fatih/color

go mod tidy
```

**Estimated Time:**
- Basic command execution: 3-4 hours
- Built-in commands: 3-4 hours
- Pipes: 4-6 hours
- Redirects: 3-4 hours
- Environment variables: 2-3 hours
- Job control: 4-6 hours
- Tab completion: 3-5 hours
- **Total**: 25-35 hours

**Files You'll Create:**
- `main.go` - 100-150 lines
- `shell/shell.go` - 200-300 lines
- `parser/parser.go` - 200-300 lines
- `executor/executor.go` - 250-400 lines
- `builtins/builtins.go` - 200-300 lines
- `jobs/jobs.go` - 150-250 lines

### Overview
Build your own Unix-like shell with command execution, pipes, redirects, environment variables, and job control. Learn process management and inter-process communication.

### What You'll Learn
- **Command Parsing**: Tokenize and parse shell commands
- **Process Execution**: Run external programs
- **Pipes**: Connect stdout of one command to stdin of another
- **I/O Redirection**: `>`, `<`, `>>`, `2>`
- **Environment Variables**: `export`, `$VAR`
- **Job Control**: Background jobs (`&`), `fg`, `bg`, `jobs`
- **Built-in Commands**: `cd`, `exit`, `export`, `alias`
- **Signal Handling**: Ctrl+C, Ctrl+Z

### Core Features
1. REPL (Read-Eval-Print-Loop)
2. Execute external commands
3. Built-ins: `cd`, `pwd`, `exit`, `echo`, `export`
4. Pipes: `cmd1 | cmd2 | cmd3`
5. Redirects: `cmd > file`, `cmd < file`, `cmd 2> errors.txt`
6. Environment variables
7. Background jobs: `cmd &`
8. Command history
9. Tab completion (paths, commands)
10. Prompt customization

### Project Structure
```
myshell/
├── main.go
├── shell/
│   ├── shell.go         # Main shell loop
│   ├── prompt.go        # Prompt rendering
│   └── history.go       # Command history
├── parser/
│   ├── lexer.go         # Tokenize input
│   └── parser.go        # Parse command structure
├── executor/
│   ├── executor.go      # Execute commands
│   ├── pipe.go          # Pipe implementation
│   └── redirect.go      # I/O redirection
├── builtins/
│   └── builtins.go      # Built-in commands
└── jobs/
    └── jobs.go          # Job control
```

### Implementation Guide

#### Step 1: Basic REPL

**What to create:**
```go
func main() {
    reader := bufio.NewReader(os.Stdin)
    for {
        fmt.Print("myshell> ")
        input, _ := reader.ReadString('\n')
        input = strings.TrimSpace(input)

        if input == "exit" {
            break
        }

        // Execute command
    }
}
```

#### Step 2: Execute Simple Commands

**What to create:**
```go
func executeCommand(cmdLine string) error {
    parts := strings.Fields(cmdLine)
    cmd := exec.Command(parts[0], parts[1:]...)
    cmd.Stdin = os.Stdin
    cmd.Stdout = os.Stdout
    cmd.Stderr = os.Stderr
    return cmd.Run()
}
```

**Hints:**
- Use `exec.Command()` to run programs
- Handle `PATH` lookup automatically
- Set stdin/stdout/stderr

#### Step 3: Built-in Commands

**What to create:**
```go
var builtins = map[string]func([]string) error{
    "cd":     changeDirBuiltin,
    "pwd":    printWorkingDir,
    "exit":   exitShell,
    "export": exportVar,
    "echo":   echoBuiltin,
}

func changeDirBuiltin(args []string) error {
    if len(args) == 0 {
        home, _ := os.UserHomeDir()
        return os.Chdir(home)
    }
    return os.Chdir(args[0])
}
```

**Why built-ins?**
- `cd` must run in shell process (can't change parent's directory)
- Some commands need shell state access

#### Step 4: Pipes

**Key Concepts:**
- Create pipe: `io.Pipe()`
- Connect stdout of cmd1 to stdin of cmd2
- Run commands concurrently

**What to create:**
```go
func executePipeline(commands [][]string) error {
    // commands = [["ls", "-l"], ["grep", "go"], ["wc", "-l"]]

    var cmds []*exec.Cmd
    for _, cmdParts := range commands {
        cmd := exec.Command(cmdParts[0], cmdParts[1:]...)
        cmds = append(cmds, cmd)
    }

    // Connect pipes
    for i := 0; i < len(cmds)-1; i++ {
        stdout, _ := cmds[i].StdoutPipe()
        cmds[i+1].Stdin = stdout
    }

    // Start all commands
    for _, cmd := range cmds {
        cmd.Start()
    }

    // Wait for all
    for _, cmd := range cmds {
        cmd.Wait()
    }
}
```

#### Step 5: I/O Redirection

**What to create:**
- Parse `>`, `<`, `>>`, `2>`
- Open files for reading/writing
- Set cmd.Stdin/Stdout/Stderr to files

**Hints:**
```go
// For `cmd > output.txt`
outFile, _ := os.Create("output.txt")
cmd.Stdout = outFile
defer outFile.Close()

// For `cmd < input.txt`
inFile, _ := os.Open("input.txt")
cmd.Stdin = inFile
defer inFile.Close()

// For `cmd >> output.txt` (append)
outFile, _ := os.OpenFile("output.txt", os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0644)
```

#### Step 6: Environment Variables

**What to create:**
```go
func expandVariables(input string) string {
    // Replace $VAR with value from environment
    re := regexp.MustCompile(`\$([A-Za-z_][A-Za-z0-9_]*)`)
    return re.ReplaceAllStringFunc(input, func(match string) string {
        varName := match[1:] // Remove $
        return os.Getenv(varName)
    })
}
```

#### Step 7: Job Control

**What to create:**
- Track background jobs
- `&` at end runs in background
- `jobs` command lists background jobs
- `fg` brings job to foreground

**Hints:**
```go
type Job struct {
    ID      int
    Cmd     *exec.Cmd
    CmdLine string
}

var jobs []Job

// Run in background
if strings.HasSuffix(cmdLine, "&") {
    cmd.Start() // Don't Wait()
    jobs = append(jobs, Job{...})
    fmt.Printf("[%d] %d\n", len(jobs), cmd.Process.Pid)
} else {
    cmd.Run() // Run and Wait
}
```

### Challenge Yourself

1. **Command History**: Arrow keys, history search
2. **Tab Completion**: Complete commands and paths
3. **Wildcards**: `*.go`, `file?.txt`
4. **Subshells**: `(cmd1; cmd2)`
5. **Command Substitution**: `` `cmd` `` or `$(cmd)`
6. **Aliases**: `alias ll='ls -la'`
7. **Functions**: Define shell functions
8. **Scripting**: Read and execute shell scripts
9. **Ctrl+C Handling**: Don't exit shell, just kill current command
10. **Colorized Prompt**: PS1-like customization

### Common Gotchas

**Problem**: `cd` doesn't work
**Fix**: Must be built-in, can't be external command

**Problem**: Pipes hang
**Fix**: Close pipe writers after writing, ensure all goroutines finish

**Problem**: Ctrl+C exits shell
**Fix**: Set up signal handler, only kill foreground process

**Problem**: Can't find commands in PATH
**Fix**: Use `exec.LookPath()` to search PATH

---

## Project 8: Network Packet Sniffer

### Prerequisites & Requirements

**Before Starting:**
- **Completed**: Intermediate networking projects
- **Platform**: Linux/macOS/Windows (needs admin/root for packet capture)

**Knowledge Prerequisites:**
- **Must Know**:
  - Network basics (TCP/IP, UDP)
  - Binary data handling
  - Concurrency
- **Should Know**:
  - Network protocols (HTTP, DNS, etc.)
  - Packet structure
  - Wireshark basics
- **Will Learn**:
  - Raw socket programming
  - Packet capture (libpcap/WinPcap)
  - Protocol decoding
  - Network analysis

**New Go Concepts:**
1. **gopacket**: Packet capture and decoding
2. **Binary Parsing**: Reading network packets
3. **Layer Decoding**: Ethernet, IP, TCP, UDP
4. **BPF Filters**: Berkeley Packet Filter

**External Dependencies:**
- **Required**:
  - `github.com/google/gopacket` - Packet capture
  - `github.com/google/gopacket/pcap` - libpcap bindings
- **System Requirements**:
  - Linux: `libpcap-dev`
  - macOS: libpcap (pre-installed)
  - Windows: WinPcap or Npcap

**What to Install:**
```bash
# Linux
sudo apt install libpcap-dev

# macOS - already has libpcap
# No installation needed

# Windows
# Download and install Npcap: https://npcap.com/

# Go dependencies
mkdir packet-sniffer
cd packet-sniffer
go mod init github.com/yourusername/packet-sniffer

go get github.com/google/gopacket
go get github.com/google/gopacket/pcap
go get github.com/google/gopacket/layers

go mod tidy
```

**Estimated Time:**
- Setup: 1-2 hours
- Basic capture: 3-4 hours
- Protocol parsing: 6-8 hours
- Filtering: 3-4 hours
- Analysis: 4-6 hours
- UI/Export: 3-4 hours
- **Total**: 20-30 hours

**Files You'll Create:**
- `main.go` - 150-200 lines
- `capture/capture.go` - 200-300 lines
- `parser/protocols.go` - 300-500 lines
- `analyzer/stats.go` - 150-250 lines
- `filter/filter.go` - 100-150 lines

### Overview
Build a network packet sniffer (like Wireshark/tcpdump) that captures and analyzes network traffic. Learn raw packet capture, protocol parsing, and network analysis.

### What You'll Learn
- **Packet Capture**: Raw socket access
- **Protocol Layers**: Ethernet, IP, TCP, UDP, HTTP, DNS
- **Binary Parsing**: Read packet bytes
- **BPF Filters**: Filter traffic efficiently
- **Network Analysis**: Bandwidth, connections, protocols
- **Promiscuous Mode**: Capture all network traffic
- **PCAP Format**: Save/load packet captures

### Core Features
1. List network interfaces
2. Capture packets in promiscuous mode
3. Decode Ethernet, IP, TCP, UDP, ICMP
4. Parse application protocols (HTTP, DNS)
5. Filter by protocol, IP, port
6. Display packet details
7. Statistics (bandwidth, packet count, protocols)
8. Save captures to PCAP file
9. Load and analyze PCAP files

### Implementation Guide

#### Step 1: List Interfaces

**What to create:**
```go
func listInterfaces() {
    devices, err := pcap.FindAllDevs()
    if err != nil {
        log.Fatal(err)
    }

    for i, device := range devices {
        fmt.Printf("%d. %s\n", i+1, device.Name)
        for _, addr := range device.Addresses {
            fmt.Printf("   IP: %s\n", addr.IP)
        }
    }
}
```

#### Step 2: Capture Packets

**What to create:**
```go
func capturePackets(device string) {
    handle, err := pcap.OpenLive(device, 1600, true, pcap.BlockForever)
    if err != nil {
        log.Fatal(err)
    }
    defer handle.Close()

    packetSource := gopacket.NewPacketSource(handle, handle.LinkType())
    for packet := range packetSource.Packets() {
        fmt.Println(packet)
    }
}
```

**Note**: Requires root/admin privileges!

#### Step 3: Parse Protocols

**What to create:**
```go
func analyzePacket(packet gopacket.Packet) {
    // Ethernet layer
    if ethLayer := packet.Layer(layers.LayerTypeEthernet); ethLayer != nil {
        eth, _ := ethLayer.(*layers.Ethernet)
        fmt.Printf("Src MAC: %s, Dst MAC: %s\n", eth.SrcMAC, eth.DstMAC)
    }

    // IP layer
    if ipLayer := packet.Layer(layers.LayerTypeIPv4); ipLayer != nil {
        ip, _ := ipLayer.(*layers.IPv4)
        fmt.Printf("Src IP: %s, Dst IP: %s\n", ip.SrcIP, ip.DstIP)
    }

    // TCP layer
    if tcpLayer := packet.Layer(layers.LayerTypeTCP); tcpLayer != nil {
        tcp, _ := tcpLayer.(*layers.TCP)
        fmt.Printf("Src Port: %d, Dst Port: %d\n", tcp.SrcPort, tcp.DstPort)
    }

    // Application data
    if appLayer := packet.ApplicationLayer(); appLayer != nil {
        payload := appLayer.Payload()
        if strings.Contains(string(payload), "HTTP") {
            fmt.Println("HTTP traffic detected")
        }
    }
}
```

#### Step 4: BPF Filters

**What to create:**
```go
// Capture only HTTP traffic
handle.SetBPFFilter("tcp port 80")

// Capture DNS
handle.SetBPFFilter("udp port 53")

// Capture specific IP
handle.SetBPFFilter("host 192.168.1.1")

// Combine filters
handle.SetBPFFilter("tcp port 80 or tcp port 443")
```

### Challenge Yourself

1. **TLS/SSL**: Parse encrypted traffic metadata
2. **Deep Packet Inspection**: Extract files from traffic
3. **Protocol Stats**: Chart protocol distribution
4. **Connection Tracking**: Track TCP connections
5. **DNS Analysis**: Show DNS queries/responses
6. **HTTP Reconstruction**: Rebuild HTTP requests/responses
7. **Real-time Dashboard**: Web UI with live stats
8. **Alert System**: Detect suspicious traffic
9. **GeoIP**: Map connections on world map
10. **Performance**: High-speed capture (1+ Gbps)

### Common Gotchas

**Problem**: Permission denied
**Fix**: Run with `sudo` (Linux/macOS) or as Administrator (Windows)

**Problem**: No devices found
**Fix**: Install libpcap/WinPcap/Npcap

**Problem**: Packets being dropped
**Fix**: Increase buffer size, use BPF filters to reduce load

**Problem**: Can't see other devices' traffic
**Fix**: Need promiscuous mode and hub/mirror port (switches isolate traffic)

---

## Project 9: System Call Tracer (strace-like)

### Prerequisites & Requirements

**Before Starting:**
- **Completed**: Advanced Go knowledge, OS concepts
- **Platform**: Linux (uses ptrace), macOS (uses dtrace/dtruss)

**Knowledge Prerequisites:**
- **Must Know**:
  - System calls concept
  - Process management
  - Signal handling
- **Will Learn**:
  - ptrace API
  - System call interception
  - Debugging APIs
  - Low-level process inspection

**What to Install:**
```bash
mkdir strace-go
cd strace-go
go mod init github.com/yourusername/strace-go

# Linux: use golang.org/x/sys/unix
go get golang.org/x/sys/unix

# Note: macOS requires dtrace, different approach
```

**Estimated Time:** 30-50 hours (complex!)

### Overview
Build a system call tracer like `strace` (Linux) or `dtruss` (macOS) that shows all system calls made by a program. Advanced userspace debugging.

### What You'll Learn
- **ptrace**: Process tracing API
- **System Calls**: What programs actually do
- **Debugging**: How debuggers work
- **Signal Handling**: Intercept and handle signals
- **Cross-platform**: Different OS debugging APIs

### Core Features
1. Attach to running process or launch new one
2. Intercept all system calls
3. Display syscall name, arguments, return value
4. Filter by syscall type
5. Count syscall frequencies
6. Measure time spent in syscalls
7. Follow child processes

### Challenge Yourself
1. Decode arguments (pointers, structures)
2. Follow forks and threads
3. Statistical summary mode
4. Filter expressions
5. Compare with real strace output

---

# Golang Learning Projects - Advanced Level

Advanced projects that tackle complex system design, distributed systems, performance optimization, and production-grade implementations.

---

## Project 1: Container Runtime (Simplified Docker)

### Prerequisites & Requirements

**Before Starting:**
- **Completed**:
  - ALL intermediate projects
  - Strong understanding of operating systems
  - Experience with Linux system administration
- **Equivalent Experience**:
  - Built complex networked applications in Go
  - Deep Linux/UNIX systems knowledge
  - Worked with Docker or Kubernetes
  - Comfortable with low-level programming

**⚠️ WARNING: Advanced Linux Project**
- **Linux ONLY** - Will NOT work on macOS or Windows (different kernels)
- **Root access required** - Many operations need sudo
- **Can break your system** - Use VM or container for development
- **Kernel knowledge required** - Not for beginners

**Knowledge Prerequisites:**
- **Must Know**:
  - Linux system administration
  - Process management (fork, exec, wait)
  - File systems and mount points
  - Network configuration (IP, routing, NAT)
  - UNIX permissions and users
  - Shell scripting
  - Go systems programming
  - Error handling patterns
- **Should Know**:
  - Linux kernel concepts
  - System calls
  - Container technology basics (Docker concepts)
  - Network namespaces and bridges
  - iptables basics
  - Layered filesystems
- **Will Learn**:
  - Linux namespaces (PID, network, mount, UTS, IPC, user)
  - cgroups v1 and v2
  - OverlayFS and union filesystems
  - pivot_root vs chroot
  - veth pairs and network bridges
  - OCI image specification
  - seccomp and capabilities
  - Container security

**New Go Concepts:**
1. **syscall Package**: Direct system calls
2. **unix Package**: Low-level UNIX APIs
3. **os/exec with Namespaces**: Process isolation
4. **SysProcAttr**: Process attributes (namespaces, credentials)
5. **unsafe Package**: Pointer manipulation (use carefully)
6. **cgo**: Call C code if needed
7. **//go:build linux**: Build constraints
8. **netlink**: Kernel networking interface

**External Dependencies:**
- **Required**:
  - `golang.org/x/sys/unix` - UNIX system calls
  - `github.com/vishvananda/netlink` - Network configuration
  - `github.com/opencontainers/runtime-spec` - OCI runtime spec
- **Optional**:
  - `github.com/docker/docker` - Study Docker's implementation
  - `github.com/opencontainers/image-spec` - OCI image spec
  - `github.com/seccomp/libseccomp-golang` - Seccomp filtering

**System Requirements:**
- **OS**: Linux (kernel 3.10+, 4.x+ recommended)
  - Ubuntu 20.04+ or Debian 11+ (recommended for beginners)
  - Fedora 35+
  - Arch Linux
  - **NOT macOS or Windows** (different kernels, no namespaces)
- **Architecture**: x86_64 (amd64)
- **RAM**: 4GB minimum (8GB+ recommended)
- **Disk**: 10GB+ free space
- **Root Access**: Required for most operations
- **VM Recommended**: Use VirtualBox, VMware, or Multipass to avoid breaking host

**Linux Features Required:**
```bash
# Check kernel version (3.10+ minimum, 4.x+ recommended)
uname -r

# Check if namespaces are supported
ls /proc/self/ns/
# Should see: cgroup, ipc, mnt, net, pid, user, uts

# Check if cgroups are available
ls /sys/fs/cgroup/

# Check cgroup version
grep cgroup /proc/filesystems
# Should see: cgroup and cgroup2

# Check if overlay filesystem is supported
grep overlay /proc/filesystems

# Check user namespaces (important!)
cat /proc/sys/kernel/unprivileged_userns_clone
# Should be 1 (enabled)

# If disabled, enable it:
sudo sysctl -w kernel.unprivileged_userns_clone=1
# Make permanent:
echo "kernel.unprivileged_userns_clone=1" | sudo tee -a /etc/sysctl.conf
```

**Development Environment Setup:**

**Option 1: Multipass VM (Recommended - Easy):**
```bash
# Install Multipass (macOS)
brew install multipass

# Install Multipass (Linux)
sudo snap install multipass

# Create Ubuntu VM
multipass launch --name container-dev --cpus 2 --memory 4G --disk 20G 22.04

# Enter VM
multipass shell container-dev

# Inside VM, install Go
sudo snap install go --classic

# Install tools
sudo apt update
sudo apt install -y build-essential git

# Setup project
mkdir -p ~/container-runtime
cd ~/container-runtime
go mod init github.com/yourusername/container-runtime
```

**Option 2: Docker Container (Paradox - Run in container to build containers):**
```bash
# Run privileged container with Go
docker run -it --privileged --name gocontainer \
  -v $(pwd):/workspace \
  -w /workspace \
  golang:1.21 bash

# Inside container
apt update && apt install -y iptables
go mod init github.com/yourusername/container-runtime
```

**Option 3: Native Linux:**
```bash
# If you're already on Linux
mkdir -p ~/container-runtime
cd ~/container-runtime
go mod init github.com/yourusername/container-runtime

# Install required tools
sudo apt install -y iptables bridge-utils
```

**What to Install:**
```bash
# 1. Go dependencies
go get golang.org/x/sys/unix
go get github.com/vishvananda/netlink
go get github.com/opencontainers/runtime-spec/specs-go

# Optional
go get github.com/seccomp/libseccomp-golang  # Needs libseccomp-dev

# 2. System tools
sudo apt update
sudo apt install -y \
    iptables \
    bridge-utils \
    iproute2 \
    uidmap \
    libseccomp-dev  # For seccomp

# 3. Verify installations
which iptables
which brctl
ip link show

go mod tidy
```

**Testing Prerequisites:**
```bash
# Test namespace creation (requires root)
sudo cat > test_namespace.go << 'EOF'
package main
import (
    "fmt"
    "os"
    "os/exec"
    "syscall"
)
func main() {
    cmd := exec.Command("/bin/bash")
    cmd.Stdin = os.Stdin
    cmd.Stdout = os.Stdout
    cmd.Stderr = os.Stderr
    cmd.SysProcAttr = &syscall.SysProcAttr{
        Cloneflags: syscall.CLONE_NEWUTS | syscall.CLONE_NEWPID | syscall.CLONE_NEWNS,
    }
    if err := cmd.Run(); err != nil {
        fmt.Println("Error:", err)
        os.Exit(1)
    }
}
EOF

sudo go run test_namespace.go
# Inside the new namespace, try:
hostname test-container  # Won't affect host
echo $$  # Should be PID 1
exit

rm test_namespace.go
```

**Test cgroups:**
```bash
# Test cgroup v1 (if available)
if [ -d /sys/fs/cgroup/memory ]; then
    sudo mkdir -p /sys/fs/cgroup/memory/test
    echo 100M | sudo tee /sys/fs/cgroup/memory/test/memory.limit_in_bytes
    echo $$ | sudo tee /sys/fs/cgroup/memory/test/cgroup.procs
    cat /sys/fs/cgroup/memory/test/memory.limit_in_bytes
    sudo rmdir /sys/fs/cgroup/memory/test
fi

# Test cgroup v2 (unified hierarchy)
if [ -f /sys/fs/cgroup/cgroup.controllers ]; then
    echo "cgroup v2 available"
    cat /sys/fs/cgroup/cgroup.controllers
fi
```

**Test overlayfs:**
```bash
# Create test overlay mount
mkdir -p /tmp/overlay-test/{lower,upper,work,merged}
echo "lower layer" > /tmp/overlay-test/lower/file.txt

sudo mount -t overlay overlay \
  -o lowerdir=/tmp/overlay-test/lower,upperdir=/tmp/overlay-test/upper,workdir=/tmp/overlay-test/work \
  /tmp/overlay-test/merged

cat /tmp/overlay-test/merged/file.txt
echo "upper layer" > /tmp/overlay-test/merged/file.txt
cat /tmp/overlay-test/merged/file.txt
cat /tmp/overlay-test/lower/file.txt  # Still shows "lower layer"
cat /tmp/overlay-test/upper/file.txt  # Shows "upper layer"

sudo umount /tmp/overlay-test/merged
rm -rf /tmp/overlay-test
```

**Estimated Time:**
- Learning Linux concepts: 10-20 hours (if new to namespaces/cgroups)
- Setup and prerequisites: 4-6 hours
- Basic container (run command): 8-12 hours
- Process isolation (namespaces): 10-15 hours
- Resource limits (cgroups): 8-12 hours
- Filesystem (overlayfs): 10-15 hours
- Networking (veth, bridge): 12-18 hours
- Image management: 8-12 hours
- Security (capabilities, seccomp): 8-12 hours
- CLI interface: 4-6 hours
- Testing and debugging: 15-25 hours
- **Total**: 100-150 hours (This is a MAJOR project!)

**Files You'll Create:**
- `main.go` - 200-300 lines
- `container/container.go` - 400-600 lines
- `container/namespace.go` - 200-300 lines
- `container/cgroup.go` - 300-500 lines
- `container/network.go` - 300-500 lines
- `container/mount.go` - 200-300 lines
- `image/image.go` - 300-400 lines
- `image/overlay.go` - 200-300 lines
- `runtime/runtime.go` - 300-500 lines
- `cli/commands.go` - 200-300 lines
- `security/capabilities.go` - 150-250 lines
- `security/seccomp.go` - 200-300 lines
- `utils/syscall_helpers.go` - 150-250 lines

**New Challenges:**
- **Low-Level Linux**: Direct system calls, kernel interfaces
- **Root Permissions**: Many operations require root
- **Complex Interactions**: Namespaces + cgroups + networking + filesystem
- **Error Handling**: Cryptic kernel errors
- **Debugging**: gdb, strace, and kernel logs
- **Security**: Preventing container escape
- **Resource Cleanup**: Properly unmounting, deleting cgroups
- **Cross-Platform Issues**: Linux-only code

**Safety Considerations:**

⚠️ **IMPORTANT - READ THIS**:

1. **Use a VM or Test Machine**:
   - Don't develop on your main workstation
   - Easy to break networking, mounts, or worse
   - Use Multipass, VirtualBox, or cloud VM

2. **Snapshot Before Testing**:
   - VM snapshots before major changes
   - Easy rollback if something breaks

3. **Clean Up Resources**:
   - Always unmount filesystems
   - Delete cgroups after use
   - Kill orphaned processes
   - Remove network interfaces

4. **Don't Run Untrusted Code**:
   - Your container runtime won't be secure initially
   - Don't run malicious code in containers
   - Missing many Docker security features

5. **Check Before Sudo**:
   - Review commands before running with sudo
   - Typo in mount/umount can be catastrophic
   - Test with non-critical directories first

**Common Setup Issues:**

1. **"operation not permitted" errors**:
   - Need root: `sudo go run main.go`
   - Or build and run separately:
     ```bash
     go build -o myruntime
     sudo ./myruntime
     ```

2. **"no such file or directory" for /proc/self/ns/**:
   - Kernel too old (need 3.10+)
   - Namespace support not compiled in kernel
   - Update kernel or use different distro

3. **"cgroup mounting failed"**:
   - Check if cgroups are mounted: `mount | grep cgroup`
   - Try manual mount:
     ```bash
     sudo mount -t cgroup2 none /sys/fs/cgroup
     ```

4. **"overlay not supported"**:
   - Check: `grep overlay /proc/filesystems`
   - Load module: `sudo modprobe overlay`
   - Add to autoload: `echo overlay | sudo tee /etc/modules-load.d/overlay.conf`

5. **"network unreachable" in container**:
   - Need network namespace setup
   - Create veth pair
   - Configure bridge
   - Set up NAT with iptables

6. **Cross-compilation errors**:
   - This is Linux-only code
   - Add build constraint: `//go:build linux`
   - Compile on Linux or in Linux VM

7. **CGO errors**:
   - If using seccomp: need `libseccomp-dev`
   - Install: `sudo apt install libseccomp-dev`
   - Or skip seccomp initially

**Debugging Tools:**

```bash
# Monitor system calls
sudo strace -f ./myruntime run /bin/sh

# Check namespaces of process
ls -la /proc/PID/ns/

# Check cgroups of process
cat /proc/PID/cgroup

# Monitor network
sudo tcpdump -i any
ip addr show
ip link show
bridge link show

# Check mounts
cat /proc/mounts | grep overlay
mount | grep overlay

# Kernel logs
sudo dmesg | tail -n 50
sudo journalctl -f

# List all network namespaces
sudo ip netns list

# Execute command in namespace
sudo ip netns exec NAMESPACE ip addr
```

**Learning Resources:**
- **Essential Reading**:
  - Linux Namespaces: https://man7.org/linux/man-pages/man7/namespaces.7.html
  - cgroups: https://www.kernel.org/doc/Documentation/cgroup-v1/cgroups.txt
  - OCI Runtime Spec: https://github.com/opencontainers/runtime-spec
  - Container Networking: https://www.tkng.io/cni/

- **Books**:
  - "Understanding the Linux Kernel" - Bovet & Cesati
  - "Linux System Programming" - Robert Love

- **Tutorials**:
  - Build Your Own Container: https://www.infoq.com/articles/build-a-container-golang/
  - Linux Containers from Scratch: https://ericchiang.github.io/post/containers-from-scratch/
  - Docker Internals: https://docker-saigon.github.io/post/Docker-Internals/

- **Reference Implementations**:
  - runc: https://github.com/opencontainers/runc (Docker's runtime)
  - crun: https://github.com/containers/crun (C implementation)
  - youki: https://github.com/containers/youki (Rust implementation)

**Alternative: Use Docker Desktop with WSL2 (Windows)**
- Windows users: Use WSL2 (Windows Subsystem for Linux)
- Install Ubuntu in WSL2
- Access Linux kernel features
- Still need root/sudo in WSL2

**Alternative: Cloud VM**
```bash
# AWS EC2 (free tier)
aws ec2 run-instances --image-id ami-ubuntu --instance-type t2.micro

# DigitalOcean
# Create $5/month droplet with Ubuntu

# Google Cloud
gcloud compute instances create container-dev --machine-type=e2-medium

# Then SSH and develop there
```

### Overview
Build a simplified container runtime that can create isolated environments using Linux namespaces, cgroups, and overlayfs. This is a deep dive into operating system concepts and how tools like Docker work under the hood.

### What You'll Learn
- **Linux Namespaces**: Isolate processes (PID, network, mount, UTS, IPC, user)
- **Cgroups**: Resource limiting (CPU, memory, I/O)
- **OverlayFS**: Layered filesystem for container images
- **chroot/pivot_root**: Change root filesystem
- **System Calls**: Direct syscall usage via `syscall` package
- **Process Management**: Fork, exec, signal handling
- **Networking**: Virtual network interfaces, bridges, iptables
- **Image Format**: OCI (Open Container Initiative) image spec
- **Security**: Capabilities, seccomp, AppArmor

### Core Features
1. Create isolated containers with separate namespaces
2. Limit container resources with cgroups
3. Use layered filesystem (overlay)
4. Network isolation with virtual interfaces
5. Pull and run container images (simplified OCI format)
6. Execute commands inside containers
7. Container lifecycle management (start, stop, kill, remove)
8. Basic logging and monitoring

### Project Structure
```
container-runtime/
├── main.go
├── runtime/
│   ├── container.go       # Container lifecycle
│   ├── namespace.go       # Namespace creation
│   ├── cgroup.go          # Resource limits
│   └── rootfs.go          # Filesystem setup
├── image/
│   ├── pull.go            # Image downloading
│   ├── layer.go           # Layer management
│   └── overlay.go         # OverlayFS setup
├── network/
│   ├── bridge.go          # Network bridge creation
│   ├── veth.go            # Virtual ethernet pairs
│   └── nat.go             # NAT/iptables rules
├── exec/
│   └── exec.go            # Execute commands in container
└── go.mod
```

### Implementation Guide

#### Step 1: Understanding Linux Namespaces

**Key Concepts:**
- **PID Namespace**: Process isolation (container sees PID 1)
- **Mount Namespace**: Filesystem isolation
- **Network Namespace**: Separate network stack
- **UTS Namespace**: Hostname isolation
- **IPC Namespace**: Inter-process communication isolation
- **User Namespace**: User/group ID remapping

**What you need to create:**

**`runtime/namespace.go`:**
- `CreateNamespaces()` function that sets up clone flags:
  - `CLONE_NEWPID` - PID namespace
  - `CLONE_NEWNET` - Network namespace
  - `CLONE_NEWNS` - Mount namespace
  - `CLONE_NEWUTS` - UTS namespace
  - `CLONE_NEWIPC` - IPC namespace
  - `CLONE_NEWUSER` - User namespace (optional, requires more setup)
- `EnterNamespace(nsType, nsPid)` - Enter existing namespace
- Helper to fork process with namespace flags

**Learning Notes:**
- Namespaces created during clone/unshare system calls
- Each namespace can be referenced via `/proc/<pid>/ns/<type>`
- Must have CAP_SYS_ADMIN capability (run as root)
- Child process inherits namespaces from parent

**Hints:**
- Use `syscall.SysProcAttr` with `Cloneflags` when starting process
- Example: `cmd.SysProcAttr = &syscall.SysProcAttr{Cloneflags: syscall.CLONE_NEWPID | syscall.CLONE_NEWNET}`
- Inside PID namespace, first process becomes PID 1
- Must call `syscall.Mount()` to setup new mount namespace properly

#### Step 2: Cgroups for Resource Limiting

**Key Concepts:**
- **Cgroups v2**: Unified hierarchy for resource control
- **Controllers**: cpu, memory, io, pids
- **Limits**: Set maximums for resources
- **Hierarchy**: Cgroups organized in tree structure

**What you need to create:**

**`runtime/cgroup.go`:**
- `CgroupConfig` struct with limits:
  - MemoryLimit (bytes)
  - CPUShares (relative weight)
  - CPUQuota (microseconds per period)
  - PIDsMax (max number of processes)
- `CreateCgroup(name, config)` - Create cgroup and set limits
- `AddProcessToCgroup(pid, cgroupPath)` - Add process to cgroup
- `RemoveCgroup(name)` - Clean up cgroup
- Helper functions to read/write cgroup files

**Learning Notes:**
- Cgroups v2 located at `/sys/fs/cgroup/`
- Each limit set by writing to specific file (e.g., `memory.max`)
- Add process by writing PID to `cgroup.procs`
- Nested cgroups inherit parent limits

**Hints:**
- Create cgroup: `os.Mkdir("/sys/fs/cgroup/mycontainer", 0755)`
- Set memory limit: `os.WriteFile("/sys/fs/cgroup/mycontainer/memory.max", []byte("536870912"), 0644)` (512MB)
- Set CPU limit: Write to `cpu.max` format: `"quota period"` (e.g., "50000 100000" = 50% CPU)
- Add PID: `os.WriteFile("/sys/fs/cgroup/mycontainer/cgroup.procs", []byte(fmt.Sprint(pid)), 0644)`
- Check if cgroup v2: `mount | grep cgroup2`

#### Step 3: Filesystem Isolation with OverlayFS

**Key Concepts:**
- **Layers**: Lower layers (read-only) + upper layer (read-write)
- **OverlayFS**: Union mount combining layers
- **Copy-on-Write**: Modifications don't affect lower layers
- **Image Layers**: Container images as stacked layers

**What you need to create:**

**`runtime/rootfs.go`:**
- `PrepareRootfs(imageLayers, containerID)` - Setup overlay mount
- `MountOverlay(lower, upper, merged, work)` - Mount overlayfs
- `SetupDevices(rootPath)` - Create /dev nodes (null, zero, random, etc.)
- `SetupProc(rootPath)` - Mount /proc
- `PivotRoot(newRoot, putOld)` - Change root filesystem
- `UnmountRootfs(containerID)` - Clean up mounts

**Learning Notes:**
- OverlayFS syntax: `mount -t overlay overlay -o lowerdir=L1:L2,upperdir=U,workdir=W merged`
- lowerdir: Read-only layers (colon-separated)
- upperdir: Writable layer (changes stored here)
- workdir: Working directory for overlay (must be empty)
- merged: Mount point where unified view appears

**Hints:**
- Use `syscall.Mount()` with type "overlay"
- Options: `fmt.Sprintf("lowerdir=%s,upperdir=%s,workdir=%s", lower, upper, work)`
- pivot_root syscall changes root mount point (more secure than chroot)
- Create essential devices: `mknod /dev/null c 1 3`
- Mount proc: `syscall.Mount("proc", "/proc", "proc", 0, "")`

#### Step 4: Container Lifecycle

**What you need to create:**

**`runtime/container.go`:**
- `Container` struct:
  - ID (unique identifier)
  - Config (command, env vars, resource limits)
  - State (running, stopped, paused)
  - Namespaces (file descriptors or paths)
  - Cgroup (path to cgroup)
  - RootFS (path to merged filesystem)
  - PID (process ID)
- Methods:
  - `Create(config)` - Setup namespaces, cgroups, rootfs (don't start yet)
  - `Start()` - Execute container command
  - `Stop(timeout)` - Send SIGTERM, wait, then SIGKILL
  - `Kill()` - Immediate SIGKILL
  - `Remove()` - Clean up resources after stop
  - `Pause()`/`Unpause()` - Use cgroup freezer
  - `Logs()` - Read container stdout/stderr

**Hints:**
- Generate UUID for container ID
- Store container metadata in JSON file
- Use `exec.Cmd` with namespace flags in `SysProcAttr`
- Redirect stdout/stderr to log files
- For pause: Write "1" to cgroup.freeze, "0" to unpause
- Track state transitions (created → running → stopped)

#### Step 5: Networking

**Key Concepts:**
- **veth pairs**: Virtual ethernet cable connecting namespaces
- **Bridge**: Virtual switch connecting containers
- **NAT**: Network address translation for internet access
- **iptables**: Firewall rules for routing

**What you need to create:**

**`network/bridge.go`:**
- `CreateBridge(name, subnet)` - Create bridge interface
- `SetupBridgeNAT(bridgeName)` - Configure NAT with iptables

**`network/veth.go`:**
- `CreateVethPair(name1, name2)` - Create virtual ethernet pair
- `AttachVethToBridge(vethName, bridgeName)` - Connect veth to bridge
- `MoveVethToNamespace(vethName, nsPid)` - Move veth to container namespace
- `ConfigureVethIP(vethName, ip, gateway)` - Assign IP address

**Learning Notes:**
- Bridge acts as virtual switch (like docker0)
- One veth end stays in host, other moves to container
- Container gets private IP (e.g., 172.17.0.0/16)
- NAT allows containers to access internet via host IP

**Hints:**
- Use `netlink` package: `go get github.com/vishvananda/netlink`
- Create bridge: `netlink.LinkAdd(&netlink.Bridge{...})`
- Create veth pair: `netlink.LinkAdd(&netlink.Veth{LinkAttrs: ..., PeerName: ...})`
- Move to namespace: `netlink.LinkSetNsPid(link, pid)`
- iptables NAT: `iptables -t nat -A POSTROUTING -s 172.17.0.0/16 ! -o docker0 -j MASQUERADE`
- Must run as root for network operations

#### Step 6: Image Management

**Key Concepts:**
- **OCI Image Format**: Standard container image format
- **Layers**: Tar archives containing filesystem changes
- **Manifest**: JSON describing image (config, layers)
- **Registry**: HTTP API for pulling images (Docker Hub, etc.)

**What you need to create:**

**`image/pull.go`:**
- `PullImage(ref)` - Download image from registry
  - Parse image reference (name:tag)
  - Fetch manifest from registry
  - Download each layer (tar.gz files)
  - Extract layers to storage
- Handle authentication (Bearer tokens)
- Show progress during download

**`image/layer.go`:**
- `ExtractLayer(tarPath, destPath)` - Extract tar archive
- `GetImageLayers(imageName)` - List layer paths for image
- `GetImageConfig(imageName)` - Read image configuration (entrypoint, env, etc.)

**Hints:**
- Docker Registry API v2: `https://registry.hub.docker.com/v2/`
- Get token: `GET /v2/` returns WWW-Authenticate header with token URL
- Get manifest: `GET /v2/<name>/manifests/<tag>`
- Download layer: `GET /v2/<name>/blobs/<digest>`
- Extract tar: Use `archive/tar` package
- Store layers: `/var/lib/myruntime/layers/<digest>/`

#### Step 7: Execute Commands in Container

**What you need to create:**

**`exec/exec.go`:**
- `Exec(containerID, command, args)` - Execute command in running container
  - Find container's namespaces
  - Enter namespaces using setns syscall
  - Execute command with proper environment
  - Stream stdout/stderr back to caller

**Hints:**
- Open namespace file: `os.Open(fmt.Sprintf("/proc/%d/ns/pid", containerPid))`
- Enter namespace: `syscall.Setns(fd, syscall.CLONE_NEWPID)`
- Must enter all namespaces (pid, net, mnt, uts, ipc)
- Use `os.Setenv()` to set environment variables
- Execute with `syscall.Exec()`

#### Step 8: CLI Interface

**What you need to create:**
- Commands:
  - `myruntime run <image> <command>` - Create and start container
  - `myruntime create <image>` - Create container without starting
  - `myruntime start <container-id>` - Start created container
  - `myruntime stop <container-id>` - Stop running container
  - `myruntime rm <container-id>` - Remove stopped container
  - `myruntime ps` - List containers
  - `myruntime logs <container-id>` - View logs
  - `myruntime exec <container-id> <command>` - Execute in container
  - `myruntime pull <image>` - Download image

**Hints:**
- Use cobra library for CLI: `go get github.com/spf13/cobra`
- Require root privileges (check `os.Geteuid() == 0`)
- Store container state in `/var/lib/myruntime/containers/`
- Use locks to prevent concurrent operations on same container

### Build and Run

**Prerequisites:**
- Linux system (namespaces/cgroups are Linux-specific)
- Root access
- Kernel with namespace/cgroup support

```bash
# Build
go build -o myruntime

# Run as root
sudo ./myruntime run alpine:latest /bin/sh

# In another terminal, list containers
sudo ./myruntime ps

# Execute command in container
sudo ./myruntime exec <container-id> ls /

# Stop and remove
sudo ./myruntime stop <container-id>
sudo ./myruntime rm <container-id>
```

### Challenge Yourself

1. **Security**: Implement seccomp profiles to restrict syscalls
2. **Capabilities**: Drop unnecessary Linux capabilities
3. **User Namespaces**: Run containers without root
4. **Volume Mounts**: Mount host directories into containers
5. **Port Mapping**: Expose container ports to host
6. **Multi-container Networks**: Containers communicate with each other
7. **Image Building**: Implement Dockerfile-like image creation
8. **Health Checks**: Monitor container health and restart
9. **Resource Monitoring**: Real-time CPU/memory stats
10. **Checkpoint/Restore**: CRIU integration for container migration

### Common Gotchas

**Problem**: "Operation not permitted" errors
**Fix**: Must run as root; check capabilities with `capsh --print`

**Problem**: Can't mount overlayfs
**Fix**: Ensure kernel has overlay module: `modprobe overlay`

**Problem**: Containers can't access network
**Fix**: Enable IP forwarding: `echo 1 > /proc/sys/net/ipv4/ip_forward`

**Problem**: Namespace cleanup fails
**Fix**: Kill all processes in namespace first, then unmount

**Problem**: Cgroup operations fail
**Fix**: Check if cgroup v2 is mounted: `mount | grep cgroup2`

---

## Project 2: Distributed Cache (Redis-like)

### Prerequisites & Requirements

**Before Starting:**
- **Completed**:
  - REST API project (networking, concurrency)
  - File Sync Tool project (network protocols)
  - OR deep experience with distributed systems
- **Equivalent Experience**:
  - Built networked services in Go
  - Worked with Redis or Memcached
  - Understanding of distributed systems concepts
  - Performance optimization experience

**Knowledge Prerequisites:**
- **Must Know**:
  - TCP networking and protocols
  - Concurrent programming (goroutines, channels, mutexes)
  - Data structures (maps, lists, sets)
  - Serialization (binary protocols)
  - Persistence (file I/O, journaling)
  - Hashing and consistent hashing
  - Error handling and recovery
- **Should Know**:
  - Redis commands and data types
  - Replication concepts
  - Network performance optimization
  - Memory management
  - Cache eviction policies (LRU, LFU)
  - Pub/sub patterns
- **Will Learn**:
  - RESP protocol (Redis Serialization Protocol)
  - Leader-follower replication
  - AOF (Append-Only File) persistence
  - RDB snapshots
  - TTL (Time-To-Live) implementation
  - Atomic operations
  - Pipeline processing
  - Cluster consistent hashing
  - High-performance TCP servers

**New Go Concepts:**
1. **sync.Map**: Concurrent map for high-performance
2. **atomic Package**: Lock-free operations
3. **bufio.Scanner/Writer**: Efficient I/O buffering
4. **time.AfterFunc**: TTL implementation
5. **context.Context**: Request cancellation
6. **sync.Pool**: Object reuse for performance
7. **binary.Write/Read**: Binary protocol encoding
8. **net.Conn Management**: Connection pooling
9. **Profiling**: pprof for performance analysis

**External Dependencies:**
- **Required**:
  - Standard library only for basic version!
  - `golang.org/x/sync/singleflight` - Prevent duplicate work (optional)
- **Optional (for advanced features)**:
  - `github.com/gomodule/redigo` - Redis client (for testing compatibility)
  - `github.com/tidwall/resp` - RESP protocol parser
  - `github.com/hashicorp/raft` - Raft consensus (for cluster mode)
  - `github.com/prometheus/client_golang` - Metrics export

**System Requirements:**
- **OS**: Linux, macOS, Windows (cross-platform)
- **RAM**: 8GB minimum (16GB for testing with large datasets)
- **CPU**: Multi-core recommended (for concurrency testing)
- **Network**: Low-latency network for cluster testing
- **Disk**: 1GB+ for persistence testing

**Performance Targets:**
- **Throughput**: 10,000+ ops/second (single instance)
- **Latency**: <1ms for GET/SET operations
- **Concurrent Connections**: 1,000+ simultaneous clients
- **Memory**: Efficient memory usage, configurable limits

**What to Install:**
```bash
# 1. Create project
mkdir distributed-cache
cd distributed-cache
go mod init github.com/yourusername/distributed-cache

# 2. Optional dependencies (start with stdlib only)
go get golang.org/x/sync/singleflight  # Prevent thundering herd

# 3. Testing and benchmarking tools
go install github.com/rakyll/hey@latest  # HTTP load testing
go install github.com/rogpeppe/gometalinter@latest  # Code linting

# 4. Install Redis client for testing compatibility
go get github.com/gomodule/redigo/redis

go mod tidy
```

**Install Redis (for comparison and testing):**
```bash
# macOS
brew install redis
brew services start redis

# Linux (Ubuntu/Debian)
sudo apt update
sudo apt install redis-server
sudo systemctl start redis-server

# Check Redis is running
redis-cli ping
# Should return: PONG

# Test basic commands
redis-cli
127.0.0.1:6379> SET mykey "Hello"
127.0.0.1:6379> GET mykey
127.0.0.1:6379> EXIT
```

**Benchmarking Tools:**
```bash
# redis-benchmark (comes with Redis)
redis-benchmark -h localhost -p 6379 -t get,set -n 100000 -q

# You'll use this to compare your implementation

# Custom benchmark tool
cat > bench.sh << 'EOF'
#!/bin/bash
echo "Benchmarking your cache..."
redis-benchmark -h localhost -p 6380 -t get,set -n 100000 -q

echo "\nComparing with Redis..."
redis-benchmark -h localhost -p 6379 -t get,set -n 100000 -q
EOF

chmod +x bench.sh
```

**Environment Configuration:**
```bash
cat > .env << 'EOF'
# Server settings
HOST=0.0.0.0
PORT=6380  # Different from Redis default 6379
MAX_CONNECTIONS=10000

# Memory settings
MAX_MEMORY_MB=1024  # 1GB limit
EVICTION_POLICY=lru  # lru, lfu, random, no-eviction

# Persistence
ENABLE_AOF=true
AOF_FILE=./appendonly.aof
AOF_SYNC=everysec  # always, everysec, no

ENABLE_RDB=true
RDB_FILE=./dump.rdb
RDB_SAVE_INTERVAL_SECONDS=300  # Save every 5 minutes

# Replication
REPLICATION_MODE=leader  # leader, follower
LEADER_HOST=localhost
LEADER_PORT=6380

# Performance
WORKER_POOL_SIZE=100
READ_BUFFER_SIZE=4096
WRITE_BUFFER_SIZE=4096

# Features
ENABLE_PUBSUB=true
ENABLE_TTL=true
TTL_CHECK_INTERVAL_MS=100

# Monitoring
ENABLE_STATS=true
STATS_PORT=8080
EOF

echo ".env" >> .gitignore
echo "*.aof" >> .gitignore
echo "*.rdb" >> .gitignore
```

**Testing Setup:**
```bash
# Test RESP protocol parsing
cat > test_resp.go << 'EOF'
package main
import (
    "bufio"
    "fmt"
    "strconv"
    "strings"
)

// Simple RESP parser for testing
func parseRESP(data string) (interface{}, error) {
    reader := bufio.NewReader(strings.NewReader(data))
    b, _ := reader.ReadByte()
    switch b {
    case '+':
        line, _ := reader.ReadString('\n')
        return strings.TrimSpace(line), nil
    case '-':
        line, _ := reader.ReadString('\n')
        return fmt.Errorf(strings.TrimSpace(line)), nil
    case ':':
        line, _ := reader.ReadString('\n')
        i, _ := strconv.Atoi(strings.TrimSpace(line))
        return i, nil
    case '$':
        line, _ := reader.ReadString('\n')
        length, _ := strconv.Atoi(strings.TrimSpace(line))
        if length == -1 {
            return nil, nil
        }
        buf := make([]byte, length)
        reader.Read(buf)
        return string(buf), nil
    default:
        return nil, fmt.Errorf("unknown type")
    }
}

func main() {
    tests := []string{
        "+OK\r\n",
        "-Error message\r\n",
        ":1000\r\n",
        "$5\r\nHello\r\n",
        "$-1\r\n",
    }
    for _, test := range tests {
        result, _ := parseRESP(test)
        fmt.Printf("%q => %v\n", test, result)
    }
}
EOF

go run test_resp.go
rm test_resp.go
```

**Test TCP Server:**
```bash
cat > test_tcp.go << 'EOF'
package main
import (
    "bufio"
    "fmt"
    "net"
)
func handleConnection(conn net.Conn) {
    defer conn.Close()
    reader := bufio.NewReader(conn)
    for {
        message, err := reader.ReadString('\n')
        if err != nil {
            return
        }
        fmt.Printf("Received: %s", message)
        conn.Write([]byte("+OK\r\n"))
    }
}
func main() {
    ln, _ := net.Listen("tcp", ":6380")
    fmt.Println("Server listening on :6380")
    for {
        conn, _ := ln.Accept()
        go handleConnection(conn)
    }
}
EOF

go run test_tcp.go &
TCP_PID=$!
sleep 1

# Test with telnet or nc
echo -e "PING\r\n" | nc localhost 6380

kill $TCP_PID
rm test_tcp.go
```

**Estimated Time:**
- Learning RESP protocol: 4-6 hours
- Basic TCP server: 6-8 hours
- Core data structures (GET/SET): 8-12 hours
- Command parser: 6-8 hours
- Advanced data types (lists, sets, hashes): 12-18 hours
- TTL implementation: 6-8 hours
- Persistence (AOF): 8-12 hours
- Persistence (RDB snapshots): 8-12 hours
- Replication: 15-25 hours
- Pub/Sub: 8-12 hours
- Performance optimization: 10-15 hours
- Cluster mode (consistent hashing): 15-25 hours
- Testing and benchmarking: 12-18 hours
- **Total**: 120-180 hours (This is a MAJOR project!)

**Files You'll Create:**
- `main.go` - 150-200 lines
- `server/server.go` - 300-500 lines
- `protocol/resp.go` - 200-300 lines
- `store/store.go` - 400-600 lines
- `store/data_types.go` - 300-500 lines
- `store/ttl.go` - 150-250 lines
- `store/eviction.go` - 200-300 lines
- `commands/commands.go` - 500-800 lines
- `persistence/aof.go` - 250-400 lines
- `persistence/rdb.go` - 300-500 lines
- `replication/replication.go` - 400-600 lines
- `pubsub/pubsub.go` - 250-400 lines
- `cluster/consistent_hash.go` - 200-300 lines
- `cluster/node.go` - 300-500 lines
- `metrics/stats.go` - 150-250 lines
- `client/client.go` - 200-300 lines (for testing)

**New Challenges:**
- **Protocol Design**: Efficient binary protocol parsing
- **Concurrency**: High-performance concurrent access
- **Memory Management**: Efficient data structures, eviction
- **Persistence**: Durable writes without sacrificing performance
- **Replication**: Consistency vs availability tradeoffs
- **Network Performance**: Minimize latency, maximize throughput
- **Cluster Management**: Node discovery, data sharding
- **Atomic Operations**: Race-free multi-step operations

**Testing Your Setup:**
```bash
# Create test client
cat > test_client.go << 'EOF'
package main
import (
    "fmt"
    "net"
    "time"
)
func main() {
    conn, err := net.Dial("tcp", "localhost:6380")
    if err != nil {
        fmt.Println("Cannot connect:", err)
        return
    }
    defer conn.Close()

    // Send PING
    conn.Write([]byte("*1\r\n$4\r\nPING\r\n"))

    // Read response
    buf := make([]byte, 1024)
    conn.SetReadDeadline(time.Now().Add(2 * time.Second))
    n, err := conn.Read(buf)
    if err != nil {
        fmt.Println("Read error:", err)
        return
    }
    fmt.Printf("Response: %q\n", buf[:n])
}
EOF

# Run when your server is ready
# go run test_client.go
```

**Common Setup Issues:**

1. **Port already in use**:
   - Check: `lsof -i :6380` (macOS/Linux) or `netstat -ano | findstr :6380` (Windows)
   - Use different port or kill process
   - Redis default is 6379, use 6380 for your cache

2. **Connection refused**:
   - Check server is running: `netstat -an | grep 6380`
   - Check firewall settings
   - Ensure binding to correct interface (0.0.0.0 vs 127.0.0.1)

3. **Performance not meeting targets**:
   - Profile with pprof: `import _ "net/http/pprof"`
   - Check for lock contention: use `sync.RWMutex` instead of `sync.Mutex`
   - Use buffered channels
   - Connection pooling

4. **Memory leaks**:
   - Not cleaning up expired keys
   - Growing maps without bounds
   - Implement eviction policy
   - Use `sync.Pool` for temporary objects

5. **Data loss on restart**:
   - Ensure AOF is syncing: `fsync()` calls
   - Check file permissions
   - Verify AOF file format
   - Test restore on startup

6. **Replication lag**:
   - Network latency between nodes
   - Follower can't keep up with write rate
   - Implement backpressure
   - Buffer replication commands

**Performance Optimization Tips:**

**Concurrency:**
```go
// Use sync.Map for high-read scenarios
var cache sync.Map
cache.Store("key", "value")
val, _ := cache.Load("key")

// Or shard regular maps to reduce lock contention
type ShardedMap struct {
    shards []*MapShard
}
func (m *ShardedMap) getShard(key string) *MapShard {
    hash := fnv.New32a()
    hash.Write([]byte(key))
    return m.shards[hash.Sum32()%uint32(len(m.shards))]
}
```

**Memory:**
```go
// Use sync.Pool for temporary objects
var bufferPool = sync.Pool{
    New: func() interface{} {
        return make([]byte, 4096)
    },
}
buf := bufferPool.Get().([]byte)
defer bufferPool.Put(buf)
```

**I/O:**
```go
// Buffered I/O
writer := bufio.NewWriterSize(conn, 32*1024)  // 32KB buffer

// Batch writes
for _, cmd := range commands {
    writer.Write(cmd)
}
writer.Flush()  // Single syscall
```

**Protocol:**
```go
// Pre-allocate common responses
var (
    respOK = []byte("+OK\r\n")
    respPong = []byte("+PONG\r\n")
    respNil = []byte("$-1\r\n")
)

// Avoid allocations in hot path
func encodeInt(n int, buf []byte) []byte {
    buf = append(buf, ':')
    buf = strconv.AppendInt(buf, int64(n), 10)
    buf = append(buf, '\r', '\n')
    return buf
}
```

**Benchmarking:**
```bash
# Profile CPU
go test -cpuprofile=cpu.prof -bench=.
go tool pprof cpu.prof
(pprof) top10
(pprof) list functionName

# Profile Memory
go test -memprofile=mem.prof -bench=.
go tool pprof mem.prof

# Trace
go test -trace=trace.out -bench=.
go tool trace trace.out
```

**Security Considerations:**
- No authentication initially (add later)
- Limit command size (prevent OOM)
- Limit number of connections
- Validate input (prevent crashes)
- Rate limiting per client
- Disable dangerous commands in production

**Learning Resources:**

**Essential Reading:**
- Redis Protocol Spec: https://redis.io/docs/reference/protocol-spec/
- Redis Commands: https://redis.io/commands/
- Build Your Own Redis: https://build-your-own.org/redis/
- Redis Internals: https://redis.com/ebook/part-2-core-concepts/

**Books:**
- "Redis in Action" - Josiah Carlson
- "Designing Data-Intensive Applications" - Martin Kleppmann

**Reference Implementations:**
- Redis source: https://github.com/redis/redis (C)
- godis: https://github.com/HDT3213/godis (Go implementation)
- miniredis: https://github.com/alicebob/miniredis (Go, in-memory)

**Videos:**
- "How Redis Works" - Redis University
- "Building a Key-Value Store" - MIT 6.824

### Overview
Build a distributed in-memory cache similar to Redis with replication, persistence, and a custom protocol. This teaches distributed systems concepts, network protocols, and high-performance data structures.

### What You'll Learn
- **TCP Protocol**: Custom binary protocol design
- **RESP Protocol**: Redis serialization protocol (optional)
- **Data Structures**: Hash tables, sorted sets, lists, strings
- **Replication**: Master-slave replication with eventual consistency
- **Persistence**: AOF (append-only file) and RDB (snapshots)
- **Pub/Sub**: Message broadcasting to subscribers
- **Expiration**: TTL (time-to-live) with efficient cleanup
- **Concurrency**: High-performance concurrent access
- **Sharding**: Consistent hashing for distributed data
- **Cluster Mode**: Multi-node coordination

### Core Features
1. Key-value operations (GET, SET, DEL, EXISTS)
2. Data types: strings, lists, sets, hashes, sorted sets
3. Expiration with TTL
4. Pub/Sub messaging
5. Persistence (AOF and RDB)
6. Master-slave replication
7. Transactions (MULTI/EXEC)
8. Custom binary protocol or RESP
9. Client libraries for Go
10. Cluster mode with sharding

### Project Structure
```
distributed-cache/
├── server/
│   ├── main.go            # Server entry point
│   ├── server.go          # TCP server
│   ├── handler.go         # Command handling
│   └── config.go          # Configuration
├── storage/
│   ├── store.go           # Main storage interface
│   ├── string.go          # String operations
│   ├── list.go            # List operations
│   ├── hash.go            # Hash operations
│   ├── set.go             # Set operations
│   └── zset.go            # Sorted set operations
├── persistence/
│   ├── aof.go             # Append-only file
│   ├── rdb.go             # Snapshot persistence
│   └── recovery.go        # Data recovery on startup
├── replication/
│   ├── master.go          # Master node logic
│   ├── slave.go           # Slave node logic
│   └── sync.go            # Replication sync protocol
├── protocol/
│   ├── parser.go          # Protocol parser
│   ├── serializer.go      # Response serialization
│   └── commands.go        # Command definitions
├── pubsub/
│   └── pubsub.go          # Pub/Sub implementation
├── cluster/
│   ├── node.go            # Cluster node
│   ├── shard.go           # Consistent hashing
│   └── gossip.go          # Node discovery and health
├── client/
│   └── client.go          # Go client library
└── go.mod
```

### Implementation Guide

#### Step 1: Core Storage Engine

**Key Concepts:**
- **Lock-free Structures**: Use sync.Map or sharded locks for concurrency
- **Generic Storage**: Store any value type with type assertions
- **TTL Management**: Background goroutine for expiration cleanup

**What you need to create:**

**`storage/store.go`:**
- `Store` struct with:
  - Main data map: `map[string]*Value`
  - Expiration map: `map[string]time.Time`
  - RWMutex for thread safety (or multiple mutexes for sharding)
  - Stats (hits, misses, evictions)
- `Value` struct to hold any type: string, list, hash, etc.
- Core methods:
  - `Get(key)` - Retrieve value
  - `Set(key, value, ttl)` - Store value with optional expiration
  - `Del(keys...)` - Delete one or more keys
  - `Exists(key)` - Check if key exists
  - `Expire(key, ttl)` - Set TTL on existing key
  - `TTL(key)` - Get remaining TTL
- Background goroutine to clean expired keys

**Learning Notes:**
- **Sharding**: Split keyspace into N shards, each with own mutex (reduces lock contention)
- **Expiration Strategies**: Passive (check on access) + active (background sweep)
- **Memory Management**: Consider max memory limits and eviction policies (LRU)

**Hints:**
- Use `sync.RWMutex` for read-heavy workloads
- Shard by key hash: `shard := hash(key) % numShards`
- Expiration goroutine: `time.NewTicker(1 * time.Second)`, scan subset of keys each iteration
- Store value type info to prevent type confusion
- Consider using `sync.Map` for high concurrency scenarios

#### Step 2: Data Type Implementations

**What you need to create:**

**`storage/string.go`:**
- `Append(key, value)` - Append to string
- `GetRange(key, start, end)` - Get substring
- `Incr(key)`, `IncrBy(key, delta)` - Atomic increment
- `Decr(key)`, `DecrBy(key, delta)` - Atomic decrement

**`storage/list.go`:**
- `LPush(key, values...)` - Prepend to list
- `RPush(key, values...)` - Append to list
- `LPop(key)`, `RPop(key)` - Remove and return elements
- `LRange(key, start, stop)` - Get range of elements
- `LLen(key)` - List length

**`storage/hash.go`:**
- `HSet(key, field, value)` - Set hash field
- `HGet(key, field)` - Get hash field
- `HGetAll(key)` - Get all fields and values
- `HDel(key, fields...)` - Delete fields
- `HExists(key, field)` - Check field exists

**`storage/set.go`:**
- `SAdd(key, members...)` - Add members to set
- `SRem(key, members...)` - Remove members
- `SMembers(key)` - Get all members
- `SIsMember(key, member)` - Check membership
- `SInter(keys...)`, `SUnion(keys...)` - Set operations

**`storage/zset.go`:**
- `ZAdd(key, score, member)` - Add member with score
- `ZRem(key, members...)` - Remove members
- `ZRange(key, start, stop)` - Get range by rank
- `ZRangeByScore(key, min, max)` - Get range by score
- `ZScore(key, member)` - Get member's score

**Hints:**
- Use Go slices for lists (consider doubly-linked list for large lists)
- Use map[string]struct{} for sets (empty struct uses no memory)
- For sorted sets, use skip list or tree structure (e.g., `github.com/emirpasic/gods`)
- All operations must be thread-safe
- Return errors for type mismatches (e.g., LPUSH on a string value)

#### Step 3: Protocol Implementation

**Key Concepts:**
- **RESP (REdis Serialization Protocol)**: Simple text protocol
- **Binary Protocol**: More efficient, custom design
- **Command Parsing**: Parse incoming bytes into commands
- **Response Encoding**: Encode results back to client

**What you need to create:**

**RESP Format (if using Redis protocol):**
```
Simple Strings: +OK\r\n
Errors: -Error message\r\n
Integers: :1000\r\n
Bulk Strings: $6\r\nfoobar\r\n
Arrays: *2\r\n$3\r\nfoo\r\n$3\r\nbar\r\n
```

**`protocol/parser.go`:**
- `ParseCommand(conn)` - Read from connection, parse into Command struct
- `Command` struct: name, args []string
- Handle multi-line inputs
- Support pipelining (multiple commands in one request)

**`protocol/serializer.go`:**
- `SerializeString(s)` - Encode string response
- `SerializeInt(i)` - Encode integer
- `SerializeArray(arr)` - Encode array
- `SerializeError(err)` - Encode error

**Hints:**
- Read until `\r\n` delimiter
- Use buffered reader: `bufio.NewReader(conn)`
- Parse array size first, then read each element
- Validate command format before processing
- Handle incomplete reads gracefully

#### Step 4: Command Handling

**What you need to create:**

**`server/handler.go`:**
- `CommandHandler` interface with `Execute(cmd) response`
- Registry of command name → handler
- Built-in commands:
  - **String**: GET, SET, DEL, INCR, DECR, APPEND, EXISTS
  - **List**: LPUSH, RPUSH, LPOP, RPOP, LRANGE, LLEN
  - **Hash**: HSET, HGET, HGETALL, HDEL, HEXISTS
  - **Set**: SADD, SREM, SMEMBERS, SISMEMBER
  - **Sorted Set**: ZADD, ZREM, ZRANGE, ZRANGEBYSCORE
  - **Key**: EXPIRE, TTL, KEYS (pattern matching)
  - **Server**: PING, INFO, SAVE, BGSAVE
  - **Pub/Sub**: PUBLISH, SUBSCRIBE, UNSUBSCRIBE
  - **Transaction**: MULTI, EXEC, DISCARD
- Argument validation
- Error handling

**Hints:**
- Use map to register commands: `map[string]CommandHandler`
- Validate argument count for each command
- Return consistent error messages
- Support case-insensitive commands
- Log slow commands for debugging

#### Step 5: Persistence

**Key Concepts:**
- **AOF**: Log every write operation, replay on restart
- **RDB**: Periodic snapshots of entire dataset
- **Hybrid**: RDB for bulk, AOF for recent changes

**What you need to create:**

**`persistence/aof.go`:**
- `AOF` struct with file handle and buffer
- `LogCommand(cmd)` - Append command to AOF file
- `Flush()` - Sync buffer to disk
- `Rewrite()` - Compact AOF by replaying and generating fresh state
- Configure fsync policy: always, every second, or never

**`persistence/rdb.go`:**
- `CreateSnapshot(store, filepath)` - Serialize entire store to binary file
- `LoadSnapshot(filepath)` - Deserialize and restore store
- Use `encoding/gob` or custom binary format
- Background save to avoid blocking

**`persistence/recovery.go`:**
- `Recover(store)` - Load RDB + replay AOF on startup
- Handle corrupted files gracefully
- Checksum verification

**Hints:**
- AOF: Simply write commands as RESP format
- Flush policy: Use `os.File.Sync()` to force write
- RDB format: Header + [key, value, expiry]* + checksum
- Background save: Fork-like with goroutine + copy-on-write map
- Rewrite AOF: Iterate current keys and generate fresh SET commands

#### Step 6: Pub/Sub

**Key Concepts:**
- **Channels**: Named topics for messages
- **Subscribers**: Clients subscribed to channels
- **Pattern Matching**: Subscribe to patterns (e.g., `news.*`)

**What you need to create:**

**`pubsub/pubsub.go`:**
- `PubSub` struct with:
  - Channels map: `map[string][]Subscriber`
  - Pattern subscriptions
  - Mutex for thread safety
- `Subscriber` struct: connection, channels subscribed
- Methods:
  - `Subscribe(conn, channels...)` - Add subscription
  - `Unsubscribe(conn, channels...)` - Remove subscription
  - `Publish(channel, message)` - Send message to all subscribers
  - `PSubscribe(conn, patterns...)` - Pattern-based subscription

**Hints:**
- When client subscribes, switch connection to pub/sub mode (no normal commands)
- Store subscriber connections and write messages directly to them
- Use goroutines to send to multiple subscribers concurrently
- Handle slow subscribers with buffer or timeout
- Pattern matching: Use `filepath.Match()` or regex

#### Step 7: Replication

**Key Concepts:**
- **Master**: Primary node handling writes
- **Slave/Replica**: Read-only copy of master
- **Sync Protocol**: Master sends data to slaves
- **Replication Lag**: Slaves may be behind master

**What you need to create:**

**`replication/master.go`:**
- Track connected slaves
- Send RDB snapshot to new slaves
- Stream AOF commands to all slaves
- `AddSlave(conn)` - Register new slave
- `BroadcastCommand(cmd)` - Send write command to all slaves

**`replication/slave.go`:**
- Connect to master on startup
- Request full sync (receive RDB)
- Receive and apply incremental updates (AOF stream)
- Read-only mode (reject writes)
- Handle reconnection if master fails

**`replication/sync.go`:**
- `FullSync(slave)` - Send RDB snapshot + offset
- `PartialSync(slave, offset)` - Resume from offset
- Replication offset tracking

**Hints:**
- Master keeps replication backlog (circular buffer of recent commands)
- Slave requests: "SYNC" for full, "PSYNC offset" for partial
- Heartbeat: Slave sends PING periodically, master responds
- On disconnect, slave tries partial sync with offset
- Handle slave failures: Remove from slave list, don't block master

#### Step 8: Cluster Mode

**Key Concepts:**
- **Consistent Hashing**: Distribute keys across nodes
- **Hash Slots**: 16384 slots, each key mapped to slot
- **Gossip Protocol**: Nodes exchange cluster state
- **Resharding**: Move slots between nodes

**What you need to create:**

**`cluster/shard.go`:**
- `HashSlot(key)` - Calculate slot for key (CRC16 % 16384)
- `SlotToNode(slot)` - Find node owning slot
- `NodeConfig`: Track which slots each node owns

**`cluster/node.go`:**
- `ClusterNode` struct: ID, address, slots owned
- `RedirectClient(key)` - Return MOVED error if key on different node
- Handle cluster commands: CLUSTER NODES, CLUSTER SLOTS

**`cluster/gossip.go`:**
- Periodic gossip messages between nodes
- Share cluster state: node list, slot assignments, health
- Detect failed nodes and trigger failover
- Use UDP for gossip efficiency

**Hints:**
- CRC16: Use `hash/crc32` or implement CRC16
- Client redirection: `-MOVED <slot> <ip>:<port>`
- Gossip: Send to random subset of nodes every second
- Slot migration: Mark slot as migrating, forward requests during transition
- Multi-key commands: Only work if all keys in same slot

#### Step 9: Client Library

**What you need to create:**

**`client/client.go`:**
- `Client` struct with connection pool
- Methods matching server commands: Get, Set, LPush, HSet, etc.
- Connection pooling for reuse
- Pipelining support (batch commands)
- Automatic reconnection
- Cluster-aware routing

**Hints:**
- Use connection pool: maintain pool of TCP connections
- Pipeline: Buffer commands, send all at once, read all responses
- Parse responses and return Go types
- Handle MOVED redirects in cluster mode
- Implement timeouts for all operations

### Build and Run

```bash
# Start master server
./cache-server --port 6379 --aof-enabled --rdb-enabled

# Start slave
./cache-server --port 6380 --replicaof localhost:6379

# Use client
./cache-cli set mykey "hello"
./cache-cli get mykey

# Start cluster (3 nodes)
./cache-server --port 7000 --cluster-enabled
./cache-server --port 7001 --cluster-enabled
./cache-server --port 7002 --cluster-enabled
```

### Challenge Yourself

1. **Sentinel**: Automatic failover for master-slave setup
2. **Streams**: Redis streams for event sourcing
3. **Geospatial**: GEO commands for location data
4. **Lua Scripting**: Execute Lua scripts server-side
5. **Bloom Filters**: Probabilistic set membership
6. **HyperLogLog**: Cardinality estimation
7. **TLS/SSL**: Encrypted connections
8. **ACL**: Access control lists for users
9. **Memory Analysis**: MEMORY commands for debugging
10. **Modules**: Plugin system for extending functionality

### Common Gotchas

**Problem**: Race conditions in concurrent access
**Fix**: Use mutexes or lock-free structures; test with `-race` flag

**Problem**: Memory leaks from expired keys
**Fix**: Implement active expiration in background goroutine

**Problem**: Replication falls behind
**Fix**: Use buffered channels, monitor lag, implement backpressure

**Problem**: AOF file grows too large
**Fix**: Implement AOF rewriting to compact

**Problem**: Cluster split-brain after network partition
**Fix**: Implement quorum-based voting for cluster decisions

---

## Project 3: Load Balancer & API Gateway

### Prerequisites & Requirements

**Before Starting:**
- **Completed**:
  - REST API project (HTTP servers)
  - Web Scraper project (HTTP clients)
  - OR significant experience with production web services
- **Equivalent Experience**:
  - Built reverse proxies or API gateways
  - Worked with nginx, HAProxy, or Envoy
  - Understanding of load balancing concepts
  - Production systems experience

**Knowledge Prerequisites:**
- **Must Know**:
  - HTTP/HTTPS protocol deep knowledge
  - Headers, methods, status codes
  - Request/response lifecycle
  - TLS/SSL basics
  - Networking (TCP, DNS, routing)
  - Goroutines and channels
  - Context for cancellation
  - Error handling patterns
- **Should Know**:
  - Load balancing algorithms
  - Health check strategies
  - Rate limiting techniques
  - Circuit breaker pattern
  - Middleware patterns
  - WebSocket protocol
  - Service discovery concepts
- **Will Learn**:
  - Reverse proxy implementation
  - HTTP/2 and WebSocket proxying
  - TLS termination
  - Advanced rate limiting algorithms
  - Circuit breaker implementation
  - Observability (metrics, tracing)
  - Dynamic backend management
  - Production-grade error handling
  - Performance optimization

**New Go Concepts:**
1. **httputil.ReverseProxy**: Built-in reverse proxy
2. **Transport Configuration**: Connection pooling, timeouts
3. **http.ResponseWriter Hijacking**: For WebSockets
4. **TLS Config**: Certificate management
5. **Context Propagation**: Request tracing
6. **sync.RWMutex**: Read-heavy workloads
7. **atomic Operations**: Lock-free counters
8. **time.Ticker**: Periodic health checks
9. **Middleware Chaining**: Request pipeline

**External Dependencies:**
- **Required**:
  - `golang.org/x/time/rate` - Rate limiting
  - `github.com/prometheus/client_golang` - Metrics
- **Recommended**:
  - `github.com/gorilla/mux` - Advanced routing
  - `github.com/gorilla/websocket` - WebSocket support
  - `github.com/hashicorp/consul/api` - Service discovery (optional)
  - `go.opentelemetry.io/otel` - Distributed tracing (optional)
  - `github.com/sony/gobreaker` - Circuit breaker implementation

**System Requirements:**
- **OS**: Linux, macOS, Windows (cross-platform)
- **RAM**: 4GB minimum (8GB recommended)
- **Network**: Good network connection for testing
- **TLS**: OpenSSL or similar for certificates
- **Load Testing Tools**: Apache Bench (ab), wrk, or k6

**Performance Targets:**
- **Throughput**: 10,000+ requests/second
- **Latency**: <10ms added latency
- **Concurrent Connections**: 10,000+ simultaneous
- **Uptime**: Graceful shutdowns, no dropped requests

**What to Install:**
```bash
# 1. Create project
mkdir load-balancer
cd load-balancer
go mod init github.com/yourusername/load-balancer

# 2. Install dependencies
go get golang.org/x/time/rate  # Rate limiting
go get github.com/prometheus/client_golang/prometheus  # Metrics
go get github.com/prometheus/client_golang/prometheus/promhttp
go get github.com/gorilla/mux  # Routing
go get github.com/gorilla/websocket  # WebSocket
go get github.com/sony/gobreaker  # Circuit breaker

# Optional: Service discovery
go get github.com/hashicorp/consul/api

# Optional: Distributed tracing
go get go.opentelemetry.io/otel
go get go.opentelemetry.io/otel/exporters/jaeger

go mod tidy
```

**Install Backend Test Servers:**
```bash
# Create simple backend servers for testing
cat > backend_server.go << 'EOF'
package main
import (
    "fmt"
    "log"
    "net/http"
    "os"
    "time"
)
func handler(w http.ResponseWriter, r *http.Request) {
    port := os.Getenv("PORT")
    time.Sleep(100 * time.Millisecond)  // Simulate work
    fmt.Fprintf(w, "Response from backend on port %s\n", port)
}
func healthHandler(w http.ResponseWriter, r *http.Request) {
    w.WriteHeader(http.StatusOK)
    fmt.Fprint(w, "OK")
}
func main() {
    port := os.Getenv("PORT")
    if port == "" {
        port = "8081"
    }
    http.HandleFunc("/", handler)
    http.HandleFunc("/health", healthHandler)
    log.Printf("Backend server listening on :%s", port)
    log.Fatal(http.ListenAndServe(":"+port, nil))
}
EOF

# Run multiple backends
PORT=8081 go run backend_server.go &
PORT=8082 go run backend_server.go &
PORT=8083 go run backend_server.go &

# Test backends
curl http://localhost:8081/
curl http://localhost:8082/health

# Stop backends
killall backend_server
```

**Install Load Testing Tools:**
```bash
# Apache Bench (usually pre-installed)
ab -V

# If not installed:
# macOS
brew install apr-util  # ab comes with httpd

# Linux
sudo apt install apache2-utils  # Ubuntu/Debian
sudo yum install httpd-tools     # CentOS/RHEL

# wrk (better than ab)
# macOS
brew install wrk

# Linux - build from source
git clone https://github.com/wg/wrk.git
cd wrk
make
sudo cp wrk /usr/local/bin/
cd ..

# k6 (modern, scriptable)
# macOS
brew install k6

# Linux
sudo gpg -k
sudo gpg --no-default-keyring --keyring /usr/share/keyrings/k6-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C5AD17C747E3415A3642D57D77C6C491D6AC1D69
echo "deb [signed-by=/usr/share/keyrings/k6-archive-keyring.gpg] https://dl.k6.io/deb stable main" | sudo tee /etc/apt/sources.list.d/k6.list
sudo apt-get update
sudo apt-get install k6
```

**TLS Certificates (for HTTPS testing):**
```bash
# Generate self-signed certificates for testing
mkdir -p certs
cd certs

# Generate CA
openssl genrsa -out ca-key.pem 2048
openssl req -x509 -new -nodes -key ca-key.pem \
  -days 365 -out ca-cert.pem \
  -subj "/CN=Test CA"

# Generate server certificate
openssl genrsa -out server-key.pem 2048
openssl req -new -key server-key.pem \
  -out server-csr.pem \
  -subj "/CN=localhost"

openssl x509 -req -in server-csr.pem \
  -CA ca-cert.pem -CAkey ca-key.pem \
  -CAcreateserial -out server-cert.pem \
  -days 365

cd ..

echo "certs/" >> .gitignore
```

**Environment Configuration:**
```bash
cat > .env << 'EOF'
# Load Balancer settings
HOST=0.0.0.0
PORT=8080
HTTPS_PORT=8443
ENABLE_TLS=false

# TLS certificates
CERT_FILE=./certs/server-cert.pem
KEY_FILE=./certs/server-key.pem

# Backend servers
BACKENDS=http://localhost:8081,http://localhost:8082,http://localhost:8083

# Load balancing
LB_ALGORITHM=round-robin  # round-robin, least-conn, weighted, ip-hash

# Health checks
HEALTH_CHECK_ENABLED=true
HEALTH_CHECK_INTERVAL_SECONDS=10
HEALTH_CHECK_TIMEOUT_SECONDS=5
HEALTH_CHECK_PATH=/health
HEALTH_CHECK_UNHEALTHY_THRESHOLD=3
HEALTH_CHECK_HEALTHY_THRESHOLD=2

# Circuit breaker
CIRCUIT_BREAKER_ENABLED=true
CIRCUIT_BREAKER_MAX_REQUESTS=100
CIRCUIT_BREAKER_INTERVAL_SECONDS=60
CIRCUIT_BREAKER_TIMEOUT_SECONDS=30
CIRCUIT_BREAKER_FAILURE_THRESHOLD=0.5  # 50% failure rate

# Rate limiting
RATE_LIMIT_ENABLED=true
RATE_LIMIT_REQUESTS_PER_SECOND=100
RATE_LIMIT_BURST=200

# Timeouts
REQUEST_TIMEOUT_SECONDS=30
IDLE_TIMEOUT_SECONDS=120
KEEP_ALIVE_TIMEOUT_SECONDS=60

# Connection pooling
MAX_IDLE_CONNS=100
MAX_IDLE_CONNS_PER_HOST=10

# Retries
MAX_RETRIES=3
RETRY_BACKOFF_MS=100

# Metrics
METRICS_ENABLED=true
METRICS_PORT=9090
METRICS_PATH=/metrics

# Logging
LOG_LEVEL=info  # debug, info, warn, error
LOG_FORMAT=json  # json, text
ACCESS_LOG_ENABLED=true

# Features
ENABLE_WEBSOCKET=true
ENABLE_GZIP=true
ENABLE_CORS=true
EOF

echo ".env" >> .gitignore
```

**Testing Setup:**
```bash
# Basic load test with ab
ab -n 10000 -c 100 http://localhost:8080/

# Advanced load test with wrk
wrk -t4 -c100 -d30s http://localhost:8080/
# -t4: 4 threads
# -c100: 100 connections
# -d30s: 30 seconds duration

# Custom wrk script for POST requests
cat > post.lua << 'EOF'
wrk.method = "POST"
wrk.body   = '{"test": "data"}'
wrk.headers["Content-Type"] = "application/json"
EOF

wrk -t4 -c100 -d10s -s post.lua http://localhost:8080/api/test

# k6 load test
cat > loadtest.js << 'EOF'
import http from 'k6/http';
import { check, sleep } from 'k6';

export let options = {
  vus: 100,
  duration: '30s',
};

export default function() {
  let res = http.get('http://localhost:8080/');
  check(res, {
    'status is 200': (r) => r.status === 200,
    'response time < 500ms': (r) => r.timings.duration < 500,
  });
  sleep(0.1);
}
EOF

k6 run loadtest.js
```

**Estimated Time:**
- Basic reverse proxy: 4-6 hours
- Load balancing algorithms: 6-8 hours
- Health checking: 6-8 hours
- Circuit breaker: 4-6 hours
- Rate limiting: 4-6 hours
- Middleware system: 4-6 hours
- TLS termination: 4-6 hours
- WebSocket proxying: 6-8 hours
- Metrics and monitoring: 6-8 hours
- Service discovery: 8-12 hours
- Configuration management: 4-6 hours
- Testing and optimization: 10-15 hours
- **Total**: 70-100 hours

**Files You'll Create:**
- `main.go` - 150-200 lines
- `config/config.go` - 100-150 lines
- `proxy/reverse_proxy.go` - 200-300 lines
- `balancer/balancer.go` - 150-250 lines
- `balancer/round_robin.go` - 80-120 lines
- `balancer/least_conn.go` - 100-150 lines
- `balancer/weighted.go` - 100-150 lines
- `balancer/consistent_hash.go` - 150-250 lines
- `health/health_checker.go` - 200-300 lines
- `circuitbreaker/breaker.go` - 150-250 lines
- `ratelimit/limiter.go` - 150-250 lines
- `middleware/middleware.go` - 100-150 lines
- `middleware/auth.go` - 80-120 lines
- `middleware/cors.go` - 60-100 lines
- `middleware/gzip.go` - 80-120 lines
- `middleware/logger.go` - 100-150 lines
- `backend/backend.go` - 150-250 lines
- `metrics/metrics.go` - 150-250 lines
- `discovery/consul.go` - 200-300 lines (if using Consul)
- `websocket/websocket.go` - 150-250 lines

**New Challenges:**
- **Connection Management**: Pooling, keep-alive, timeouts
- **State Management**: Tracking backend health, connections
- **Graceful Shutdown**: No dropped requests during restart
- **Performance**: Minimize latency, maximize throughput
- **Observability**: Metrics, logs, tracing
- **Dynamic Configuration**: Hot reload, service discovery
- **Error Handling**: Retries, timeouts, circuit breaking
- **Security**: Authentication, rate limiting, TLS

**Testing Your Setup:**
```bash
# Test reverse proxy
cat > test_proxy.go << 'EOF'
package main
import (
    "fmt"
    "log"
    "net/http"
    "net/http/httputil"
    "net/url"
)
func main() {
    target, _ := url.Parse("http://localhost:8081")
    proxy := httputil.NewSingleHostReverseProxy(target)

    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        proxy.ServeHTTP(w, r)
    })

    fmt.Println("Proxy listening on :8080")
    log.Fatal(http.ListenAndServe(":8080", nil))
}
EOF

# Run backend and proxy
PORT=8081 go run backend_server.go &
BACKEND_PID=$!
sleep 1

go run test_proxy.go &
PROXY_PID=$!
sleep 1

# Test
curl http://localhost:8080/

kill $BACKEND_PID $PROXY_PID
rm test_proxy.go
```

**Common Setup Issues:**

1. **Backend connection refused**:
   - Ensure backends are running
   - Check backend URLs in config
   - Verify network connectivity

2. **Health checks failing**:
   - Check health check endpoint exists
   - Verify timeout settings
   - Look at backend logs

3. **High latency**:
   - Enable connection pooling
   - Increase MaxIdleConns
   - Reduce health check frequency
   - Profile with pprof

4. **WebSocket proxy not working**:
   - Need to upgrade connection
   - Copy Upgrade headers
   - Use httputil.ReverseProxy.ModifyResponse

5. **TLS errors**:
   - Check certificate paths
   - Verify certificate is valid
   - For testing, use InsecureSkipVerify (not for production!)

6. **Circuit breaker stuck open**:
   - Check failure threshold
   - Verify timeout settings
   - Look at backend health

**Performance Optimization:**

**Connection Pooling:**
```go
transport := &http.Transport{
    MaxIdleConns:        100,
    MaxIdleConnsPerHost: 10,
    IdleConnTimeout:     90 * time.Second,
    DisableKeepAlives:   false,
}

client := &http.Client{
    Transport: transport,
    Timeout:   30 * time.Second,
}
```

**Reduce Allocations:**
```go
// Reuse buffers
var bufferPool = sync.Pool{
    New: func() interface{} {
        return new(bytes.Buffer)
    },
}

buf := bufferPool.Get().(*bytes.Buffer)
defer func() {
    buf.Reset()
    bufferPool.Put(buf)
}()
```

**Concurrent Health Checks:**
```go
var wg sync.WaitGroup
for _, backend := range backends {
    wg.Add(1)
    go func(b *Backend) {
        defer wg.Done()
        b.HealthCheck()
    }(backend)
}
wg.Wait()
```

**Profiling:**
```go
import _ "net/http/pprof"

go func() {
    log.Println(http.ListenAndServe("localhost:6060", nil))
}()

// Then visit:
// http://localhost:6060/debug/pprof/
// go tool pprof http://localhost:6060/debug/pprof/profile?seconds=30
```

**Benchmarking:**
```bash
# Benchmark different algorithms
for algo in round-robin least-conn weighted ip-hash; do
    echo "Testing $algo..."
    # Update config
    sed -i '' "s/LB_ALGORITHM=.*/LB_ALGORITHM=$algo/" .env
    # Restart load balancer
    pkill load-balancer
    ./load-balancer &
    sleep 2
    # Run benchmark
    wrk -t4 -c100 -d10s http://localhost:8080/ | grep Requests/sec
done
```

**Monitoring:**
```bash
# Start Prometheus (if installed)
prometheu --config.file=prometheus.yml

# prometheus.yml:
cat > prometheus.yml << 'EOF'
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'load-balancer'
    static_configs:
      - targets: ['localhost:9090']
EOF

# Grafana dashboard for metrics
# Import dashboard ID 11074 (generic load balancer)
```

**Security Considerations:**
- Validate backend URLs
- Implement authentication middleware
- Rate limit per IP/user
- Prevent header injection
- Sanitize request/response
- Use TLS in production
- Set security headers (HSTS, CSP, etc.)
- Regular security audits

**Production Checklist:**
- [ ] Health checks working
- [ ] Circuit breakers configured
- [ ] Rate limiting enabled
- [ ] TLS certificates valid
- [ ] Metrics exposed
- [ ] Logging configured
- [ ] Graceful shutdown
- [ ] Connection limits set
- [ ] Timeouts configured
- [ ] Error handling tested
- [ ] Load tested at expected scale
- [ ] Monitoring alerts set up

**Learning Resources:**

**Essential Reading:**
- nginx architecture: https://www.aosabook.org/en/nginx.html
- HAProxy configuration: https://www.haproxy.org/
- Envoy proxy: https://www.envoyproxy.io/docs/
- Load Balancing Algorithms: https://kemptechnologies.com/load-balancer/load-balancing-algorithms-techniques/

**Books:**
- "Site Reliability Engineering" - Google
- "Designing Distributed Systems" - Brendan Burns

**Go Resources:**
- net/http/httputil: https://pkg.go.dev/net/http/httputil
- Go HTTP Server Internals: https://blog.cloudflare.com/the-complete-guide-to-golang-net-http-timeouts/

### Overview
Build a production-grade load balancer with health checking, multiple balancing algorithms, circuit breaking, and API gateway features like rate limiting, authentication, and request transformation.

### What You'll Learn
- **Reverse Proxy**: Forward requests to backend servers
- **Load Balancing Algorithms**: Round-robin, least connections, weighted, consistent hashing
- **Health Checks**: Active and passive health monitoring
- **Circuit Breaker**: Prevent cascading failures
- **Rate Limiting**: Token bucket, leaky bucket, sliding window
- **Middleware Chain**: Composable request/response processing
- **TLS Termination**: Handle HTTPS at load balancer
- **WebSocket Proxying**: Upgrade and proxy WebSocket connections
- **Metrics & Monitoring**: Prometheus metrics, OpenTelemetry
- **Service Discovery**: Dynamic backend registration (Consul, etcd)

### Core Features
1. HTTP/HTTPS reverse proxy
2. Multiple load balancing algorithms
3. Health checking (HTTP, TCP, custom)
4. Circuit breaker pattern
5. Rate limiting per client/route
6. Authentication (JWT, API keys)
7. Request/response transformation
8. WebSocket support
9. Metrics and logging
10. Dynamic configuration reload
11. Service discovery integration
12. A/B testing and canary deployments

### Project Structure
```
load-balancer/
├── main.go
├── proxy/
│   ├── proxy.go           # Core reverse proxy
│   ├── director.go        # Request routing
│   └── websocket.go       # WebSocket handling
├── balancer/
│   ├── interface.go       # Balancer interface
│   ├── roundrobin.go      # Round-robin algorithm
│   ├── leastconn.go       # Least connections
│   ├── weighted.go        # Weighted round-robin
│   └── consistent.go      # Consistent hashing
├── health/
│   ├── checker.go         # Health check orchestrator
│   ├── http.go            # HTTP health checks
│   └── tcp.go             # TCP health checks
├── middleware/
│   ├── ratelimit.go       # Rate limiting
│   ├── auth.go            # Authentication
│   ├── circuitbreaker.go  # Circuit breaker
│   ├── retry.go           # Retry logic
│   ├── timeout.go         # Request timeouts
│   ├── cors.go            # CORS headers
│   └── transform.go       # Request/response modification
├── backend/
│   ├── pool.go            # Backend server pool
│   ├── server.go          # Backend server representation
│   └── discovery.go       # Service discovery
├── config/
│   ├── config.go          # Configuration structs
│   └── loader.go          # Hot reload configuration
├── metrics/
│   └── prometheus.go      # Prometheus metrics
└── go.mod
```

### Implementation Guide

#### Step 1: Core Reverse Proxy

**Key Concepts:**
- **httputil.ReverseProxy**: Go's built-in reverse proxy
- **Director Function**: Modify request before forwarding
- **Transport**: Customize HTTP client behavior
- **Error Handling**: Handle backend failures gracefully

**What you need to create:**

**`proxy/proxy.go`:**
- `Proxy` struct with:
  - Balancer (selects backend)
  - Middleware chain
  - Error handler
  - Transport configuration
- `ServeHTTP(w, r)` - Main request handling:
  - Select backend via balancer
  - Apply middleware
  - Forward request
  - Handle response
- `NewProxy(config)` - Create configured proxy
- Custom `Director` function to rewrite requests

**Learning Notes:**
- `httputil.NewSingleHostReverseProxy()` for single backend
- Director rewrites request URL, headers
- Transport handles connection pooling, timeouts
- Error handling via `ModifyResponse` or `ErrorHandler`

**Hints:**
- Create custom transport with timeouts:
```go
&http.Transport{
    MaxIdleConns: 100,
    IdleConnTimeout: 90 * time.Second,
    DialContext: (&net.Dialer{Timeout: 30 * time.Second}).DialContext,
}
```
- Preserve X-Forwarded-For, X-Real-IP headers
- Remove hop-by-hop headers (Connection, Upgrade, etc.)
- Handle errors: retry different backend, return 502/503

#### Step 2: Load Balancing Algorithms

**What you need to create:**

**`balancer/interface.go`:**
- `Balancer` interface:
  - `Next()` - Select next backend
  - `AddBackend(server)` - Add server to pool
  - `RemoveBackend(server)` - Remove server
  - `MarkUnhealthy(server)` - Mark server as down
  - `MarkHealthy(server)` - Mark server as up

**`balancer/roundrobin.go`:**
- Simple round-robin using atomic counter
- Cycle through available backends
- Skip unhealthy backends

**`balancer/leastconn.go`:**
- Track active connections per backend
- Select backend with fewest connections
- Increment on request start, decrement on finish

**`balancer/weighted.go`:**
- Weighted round-robin
- Servers with higher weight selected more often
- Use smooth weighted algorithm (avoid bursts)

**`balancer/consistent.go`:**
- Consistent hashing (for sticky sessions)
- Hash request attribute (IP, session cookie)
- Use hash ring with virtual nodes
- Minimizes redistribution on backend changes

**Hints:**
- Use `sync/atomic` for lock-free counters
- For least connections, use atomic.Int64 per backend
- Consistent hashing: Create 100-150 virtual nodes per backend
- Test rebalancing when backends added/removed
- Consider health status in selection

#### Step 3: Health Checking

**Key Concepts:**
- **Active Checks**: Periodically probe backends
- **Passive Checks**: Detect failures from proxy traffic
- **Check Types**: HTTP, TCP, custom script
- **Grace Period**: Don't immediately mark as down (flap detection)

**What you need to create:**

**`health/checker.go`:**
- `HealthChecker` struct:
  - Check interval (e.g., every 10 seconds)
  - Timeout per check
  - Healthy/unhealthy thresholds
  - Map of backend → health status
- `Start()` - Begin health checking
- `Stop()` - Stop health checks
- Notify balancer of health changes

**`health/http.go`:**
- `HTTPHealthCheck` - Send GET request to health endpoint
- Check status code (200-299 = healthy)
- Verify response body matches expected value (optional)
- Timeout handling

**`health/tcp.go`:**
- `TCPHealthCheck` - Attempt TCP connection
- Connection success = healthy
- Faster than HTTP, no application logic

**Hints:**
- Run health checks in goroutines per backend
- Require N consecutive successes to mark healthy (avoid flapping)
- Require M consecutive failures to mark unhealthy
- Log health status changes
- Exponential backoff for failed backends
- Passive checks: Count 5xx responses, mark unhealthy after threshold

#### Step 4: Circuit Breaker

**Key Concepts:**
- **States**: Closed (normal), Open (failing), Half-Open (testing)
- **Failure Threshold**: Open circuit after N failures
- **Timeout**: Try again after timeout period
- **Success Threshold**: Close circuit after M successes in half-open

**What you need to create:**

**`middleware/circuitbreaker.go`:**
- `CircuitBreaker` struct per backend:
  - State (closed/open/half-open)
  - Failure count
  - Success count
  - Last failure time
  - Threshold config
- `Execute(fn)` - Wrap request execution:
  - If open, return immediately (fail fast)
  - If half-open, allow limited requests
  - If closed, execute normally
  - Update state based on result
- Metrics for circuit breaker trips

**State Transitions:**
- Closed → Open: After N failures
- Open → Half-Open: After timeout
- Half-Open → Closed: After M successes
- Half-Open → Open: On any failure

**Hints:**
- Use `sync.RWMutex` for state access
- Consider time window (failures in last 10 seconds)
- Return specific error when circuit open
- Emit metrics when circuit trips
- Different thresholds per backend or route

#### Step 5: Rate Limiting

**Key Concepts:**
- **Token Bucket**: Tokens added at rate, consumed per request
- **Leaky Bucket**: Fixed rate output, requests queue
- **Sliding Window**: Count requests in rolling time window
- **Per-Client**: Track by IP or API key

**What you need to create:**

**`middleware/ratelimit.go`:**
- `RateLimiter` struct with:
  - Algorithm (token bucket, sliding window, etc.)
  - Rate (requests per second/minute)
  - Burst (max tokens)
  - Storage (in-memory map or Redis)
- `Allow(clientID)` - Check if request allowed
- `Middleware(next)` - HTTP middleware:
  - Extract client ID (IP, header, cookie)
  - Check rate limit
  - Return 429 Too Many Requests if exceeded
  - Add headers: X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset

**Token Bucket Algorithm:**
- Bucket has capacity B (burst)
- Tokens added at rate R per second
- Request consumes 1 token
- If tokens available, allow request; else deny

**Hints:**
- Use `golang.org/x/time/rate` for token bucket
- Store per-client state: `map[string]*rate.Limiter`
- Clean up expired entries periodically
- For distributed: Use Redis with atomic operations
- Different limits per route or user tier

#### Step 6: Middleware Chain

**Key Concepts:**
- **Middleware Pattern**: Wrap handlers with reusable logic
- **Composition**: Chain multiple middleware
- **Order Matters**: Middleware executed in order

**What you need to create:**

**Middleware Implementations:**
- `Logger` - Log requests and responses
- `Metrics` - Record Prometheus metrics
- `Recovery` - Recover from panics
- `CORS` - Handle CORS preflight and headers
- `Auth` - Validate JWT or API keys
- `Transform` - Modify request/response headers/body
- `Retry` - Retry failed requests
- `Timeout` - Enforce request timeouts
- `Compression` - Gzip response compression

**`middleware/chain.go`:**
- `Chain(middlewares...)` - Compose middleware
- `Middleware` type: `func(http.Handler) http.Handler`

**Hints:**
- Middleware signature: `func(next http.Handler) http.Handler`
- Chain execution: outermost middleware wraps all others
- Use context to pass data between middleware
- Order example: Recovery → Logger → CORS → Auth → RateLimit → Proxy
- Allow per-route middleware configuration

#### Step 7: WebSocket Proxying

**Key Concepts:**
- **Upgrade**: HTTP connection upgraded to WebSocket
- **Bidirectional**: Proxy both directions simultaneously
- **Framing**: WebSocket frame format
- **Ping/Pong**: Keep-alive mechanism

**What you need to create:**

**`proxy/websocket.go`:**
- `IsWebSocketRequest(r)` - Check if upgrade request
- `ProxyWebSocket(w, r, backend)` - Proxy WebSocket:
  - Dial backend WebSocket
  - Upgrade client connection
  - Bidirectional copy: client ↔ backend
  - Handle ping/pong frames
  - Close both connections on error

**Hints:**
- Check headers: `Upgrade: websocket`, `Connection: Upgrade`
- Use `gorilla/websocket` or `nhooyr.io/websocket`
- Bidirectional copy: Two goroutines, one per direction
- Preserve WebSocket subprotocols
- Health check WebSocket backends differently
- Consider sticky sessions for WebSocket (consistent hashing)

#### Step 8: Metrics & Monitoring

**Key Concepts:**
- **Prometheus**: Time-series metrics database
- **Metric Types**: Counter, Gauge, Histogram, Summary
- **Labels**: Categorize metrics (backend, status code)

**What you need to create:**

**`metrics/prometheus.go`:**
- Metrics to expose:
  - Request count (counter, by backend, status, method)
  - Request duration (histogram, by backend)
  - Active connections (gauge, by backend)
  - Backend health (gauge)
  - Circuit breaker state (gauge)
  - Rate limit rejections (counter)
- `/metrics` endpoint for Prometheus scraping
- Middleware to record metrics per request

**Hints:**
- Use `github.com/prometheus/client_golang`
- Define metrics:
```go
requestsTotal = promauto.NewCounterVec(
    prometheus.CounterOpts{Name: "http_requests_total"},
    []string{"backend", "status", "method"},
)
```
- Record in middleware:
```go
requestsTotal.WithLabelValues(backend, status, method).Inc()
```
- Histogram buckets: `.001, .005, .01, .05, .1, .5, 1, 5` (seconds)
- Expose with `promhttp.Handler()` on separate port (e.g., 9090)

#### Step 9: Service Discovery

**Key Concepts:**
- **Dynamic Registration**: Backends register themselves
- **Health Integration**: Remove unhealthy backends
- **Watch**: React to backend changes in real-time
- **Service Registry**: Consul, etcd, Kubernetes

**What you need to create:**

**`backend/discovery.go`:**
- `ServiceDiscovery` interface:
  - `Watch()` - Start watching for changes
  - `GetBackends()` - List current backends
  - `Subscribe(callback)` - Notify on changes
- Implementations:
  - `ConsulDiscovery` - Use Consul API
  - `KubernetesDiscovery` - Watch Kubernetes services
  - `StaticDiscovery` - Load from config file

**Consul Example:**
- Backends register: `curl -X PUT consul:8500/v1/agent/service/register`
- Load balancer watches: `consul:8500/v1/health/service/myapp`
- Receive list of healthy backends
- Update backend pool on changes

**Hints:**
- Poll or use long-polling/streaming from service registry
- Parse backend metadata: weight, tags, version
- Implement retry with backoff if registry unavailable
- Cache last known backends in case registry down
- Support canary deployments: route % to new version

#### Step 10: Configuration & Hot Reload

**What you need to create:**

**`config/config.go`:**
- Configuration structure:
```yaml
backends:
  - url: http://backend1:8080
    weight: 10
    health_check: /health
  - url: http://backend2:8080
    weight: 5

load_balancer:
  algorithm: weighted_round_robin
  health_check_interval: 10s

rate_limiting:
  enabled: true
  requests_per_minute: 100

circuit_breaker:
  failure_threshold: 5
  timeout: 30s
```

**`config/loader.go`:**
- `LoadConfig(path)` - Read and parse YAML/JSON
- `WatchConfig(path, callback)` - Watch file for changes
- `ReloadConfig()` - Apply new configuration without restart:
  - Update backend pool
  - Adjust rate limits
  - Change balancing algorithm
  - Graceful: Don't drop in-flight requests

**Hints:**
- Use `fsnotify` to watch config file
- Validate configuration before applying
- Use atomic pointer swap for zero-downtime reload
- Log configuration changes
- Support multiple config formats: YAML, JSON, TOML

### Build and Run

```bash
# Build
go build -o lb

# Configuration file (config.yaml)
# ... (see above)

# Run
./lb --config config.yaml --port 8080 --metrics-port 9090

# Test
curl http://localhost:8080/api/users

# View metrics
curl http://localhost:9090/metrics

# Reload configuration
kill -HUP $(pgrep lb)
```

### Challenge Yourself

1. **gRPC Support**: Load balance gRPC services
2. **Mutual TLS**: Client certificate authentication
3. **WAF**: Web Application Firewall rules
4. **DDoS Protection**: Advanced rate limiting, IP blocking
5. **Caching**: Cache responses at load balancer
6. **Request Tracing**: OpenTelemetry distributed tracing
7. **Blue-Green Deployment**: Instant traffic switching
8. **Geographic Routing**: Route to nearest region
9. **Session Affinity**: Sticky sessions based on cookie
10. **Admin UI**: Web dashboard for configuration and monitoring

### Common Gotchas

**Problem**: Connection pool exhaustion
**Fix**: Configure `MaxIdleConns` and `IdleConnTimeout` appropriately

**Problem**: WebSocket connections break after timeout
**Fix**: Don't apply HTTP timeouts to WebSocket connections

**Problem**: Health checks overwhelm backends
**Fix**: Adjust check interval, stagger checks across backends

**Problem**: Memory leak from goroutines
**Fix**: Ensure all goroutines have exit conditions, use context cancellation

**Problem**: Uneven load distribution
**Fix**: Implement weighted algorithms, consider backend capacity

---

## Final Thoughts - Advanced Projects

After completing these advanced projects, you'll understand:

✅ Operating system internals (namespaces, cgroups, syscalls)
✅ Distributed systems patterns (replication, sharding, consensus)
✅ High-performance data structures and algorithms
✅ Network programming and custom protocols
✅ Production-grade error handling and resilience
✅ Observability and monitoring
✅ Systems design and architecture

---

## Project 4: Custom Filesystem (FUSE)

### Prerequisites & Requirements

**Before Starting:**
- **Completed**: File Sync Tool, Container Runtime
- **Platform**: Linux, macOS (FUSE support), Windows (using WinFsp)

**Knowledge Prerequisites:**
- **Must Know**:
  - Filesystem concepts (inodes, directories, files)
  - File operations (read, write, seek)
  - POSIX file API
- **Will Learn**:
  - FUSE (Filesystem in Userspace)
  - Filesystem implementation
  - Virtual filesystems
  - Inode management

**External Dependencies:**
- **Required**:
  - `github.com/hanwen/go-fuse/v2` - FUSE bindings for Go
  - System: FUSE/macFUSE/WinFsp

**What to Install:**
```bash
# Linux
sudo apt install fuse libfuse-dev

# macOS
brew install --cask macfuse

# Go dependencies
mkdir myfs
cd myfs
go mod init github.com/yourusername/myfs

go get github.com/hanwen/go-fuse/v2/fs
go get github.com/hanwen/go-fuse/v2/fuse

go mod tidy
```

**Estimated Time:** 40-60 hours

### Overview
Build a custom filesystem using FUSE (Filesystem in Userspace). Implement a memory-based filesystem, encrypted filesystem, or remote filesystem. Learn how filesystems work at a low level.

### What You'll Learn
- **FUSE**: Filesystem in userspace
- **Filesystem Operations**: open, read, write, mkdir, rmdir, etc.
- **Inode Management**: File metadata
- **Directory Structures**: Hierarchical storage
- **Caching**: Improve performance
- **Extended Attributes**: xattr support

### Core Features
1. In-memory filesystem (like tmpfs)
2. File CRUD operations
3. Directory operations
4. File metadata (size, timestamps, permissions)
5. Symbolic links
6. Mount/unmount
7. Persistence (optional - save to disk)

### Project Ideas
1. **MemFS**: Pure in-memory filesystem
2. **EncryptFS**: Transparent encryption filesystem
3. **DeduplicatedFS**: Content-addressable storage
4. **S3FS**: Mount S3 bucket as filesystem
5. **GitFS**: Expose Git repository as filesystem
6. **HTTPFS**: Mount HTTP directory listings
7. **UnionFS**: Overlay multiple filesystems

### Implementation Guide

#### Step 1: Basic FUSE Setup

**What to create:**
```go
type MemFS struct {
    fs.Inode
    files map[string]*MemFile
}

type MemFile struct {
    data    []byte
    mode    uint32
    modTime time.Time
}

func main() {
    root := &MemFS{
        files: make(map[string]*MemFile),
    }

    server, _ := fs.Mount("/tmp/myfs", root, &fs.Options{
        MountOptions: fuse.MountOptions{
            Name:  "myfs",
            Debug: true,
        },
    })

    server.Wait()
}
```

#### Step 2: Implement Operations

**Required Methods:**
- `Getattr`: Get file attributes
- `Open`: Open file
- `Read`: Read file data
- `Write`: Write file data
- `Readdir`: List directory contents
- `Mkdir`: Create directory
- `Unlink`: Delete file
- `Rmdir`: Remove directory
- `Rename`: Rename file/directory

### Challenge Yourself
1. **Encryption**: Transparent file encryption
2. **Compression**: Compress files on-the-fly
3. **Versioning**: Keep file history
4. **Quota**: Limit filesystem size
5. **Permissions**: Full POSIX permissions
6. **Extended Attributes**: xattr support
7. **Hard Links**: Multiple names for same inode
8. **Caching**: Kernel cache support
9. **Network FS**: Remote filesystem over network
10. **Performance**: Benchmark against real filesystems

---

## Project 5: Kernel Module (eBPF Program)

### Prerequisites & Requirements

**Before Starting:**
- **Completed**: System call tracer, advanced Linux knowledge
- **Platform**: Linux only (kernel 4.x+)
- **Skills**: C basics (eBPF programs written in restricted C)

**Knowledge Prerequisites:**
- **Must Know**:
  - Linux kernel concepts
  - System calls
  - Networking basics
  - C programming basics
- **Will Learn**:
  - eBPF (Extended Berkeley Packet Filter)
  - Kernel-level programming
  - Performance tracing
  - Security monitoring

**External Dependencies:**
- **Required**:
  - `github.com/cilium/ebpf` - eBPF library for Go
  - `clang`, `llvm` - Compile eBPF programs
  - Linux headers

**What to Install:**
```bash
# Linux
sudo apt install clang llvm libbpf-dev linux-headers-$(uname -r)

mkdir ebpf-tracer
cd ebpf-tracer
go mod init github.com/yourusername/ebpf-tracer

go get github.com/cilium/ebpf
go get github.com/cilium/ebpf/link
go get github.com/cilium/ebpf/perf

go mod tidy
```

**Estimated Time:** 50-80 hours (very complex!)

### Overview
Build eBPF-based tools for tracing, monitoring, and security. eBPF allows running sandboxed programs in the Linux kernel without kernel modules or system reboot. This is cutting-edge technology used by Cilium, Falco, and bpftrace.

### What You'll Learn
- **eBPF**: Extended BPF for kernel programming
- **Kernel Tracing**: Trace kernel functions
- **Performance Analysis**: Low-overhead profiling
- **Security**: Runtime security monitoring
- **Networking**: Packet filtering in kernel

### Project Ideas

#### 1. **System Call Tracer (eBPF version)**
- Trace all system calls
- Lower overhead than ptrace
- Per-process filtering

#### 2. **Network Monitor**
- Capture packets in kernel
- Count bytes per process
- Protocol statistics

#### 3. **File Access Monitor**
- Track file opens/reads/writes
- Security auditing
- Performance analysis

#### 4. **CPU Profiler**
- Sample stack traces
- Generate flame graphs
- Find hotspots

#### 5. **Security Monitor**
- Detect suspicious behavior
- Block unauthorized actions
- Container security

### Implementation Guide

#### Step 1: Write eBPF Program (C)

**File: `tracer.c`**
```c
//go:build ignore

#include <linux/bpf.h>
#include <bpf/bpf_helpers.h>

struct event {
    __u32 pid;
    __u64 ts;
    char comm[16];
};

struct {
    __uint(type, BPF_MAP_TYPE_PERF_EVENT_ARRAY);
} events SEC(".maps");

SEC("tracepoint/syscalls/sys_enter_openat")
int trace_openat(void *ctx) {
    struct event e = {};
    e.pid = bpf_get_current_pid_tgid() >> 32;
    e.ts = bpf_ktime_get_ns();
    bpf_get_current_comm(&e.comm, sizeof(e.comm));

    bpf_perf_event_output(ctx, &events, BPF_F_CURRENT_CPU, &e, sizeof(e));
    return 0;
}

char LICENSE[] SEC("license") = "GPL";
```

#### Step 2: Load and Run (Go)

**File: `main.go`**
```go
//go:generate go run github.com/cilium/ebpf/cmd/bpf2go -cc clang tracer tracer.c

package main

import (
    "github.com/cilium/ebpf/link"
    "github.com/cilium/ebpf/perf"
)

func main() {
    // Load pre-compiled eBPF objects
    objs := tracerObjects{}
    if err := loadTracerObjects(&objs, nil); err != nil {
        panic(err)
    }
    defer objs.Close()

    // Attach to tracepoint
    tp, err := link.Tracepoint("syscalls", "sys_enter_openat", objs.TraceOpenat, nil)
    if err != nil {
        panic(err)
    }
    defer tp.Close()

    // Read events
    rd, err := perf.NewReader(objs.Events, 4096)
    if err != nil {
        panic(err)
    }
    defer rd.Close()

    for {
        record, err := rd.Read()
        if err != nil {
            continue
        }

        // Parse event struct
        // Process event...
    }
}
```

#### Step 3: Compile and Run

```bash
# Generate Go bindings
go generate

# Build
go build

# Run (needs root)
sudo ./ebpf-tracer
```

### Challenge Yourself

1. **XDP**: High-performance packet filtering
2. **LSM**: Linux Security Modules hooks
3. **kprobes**: Trace any kernel function
4. **uprobes**: Trace userspace functions
5. **Maps**: Share data between kernel and userspace
6. **Statistics**: Histograms, counters
7. **Filtering**: Complex event filtering
8. **Multiple Programs**: Coordinate multiple eBPF programs
9. **CO-RE**: Compile Once, Run Everywhere
10. **Visualization**: Real-time dashboards

### Use Cases

**Performance:**
- CPU profiling
- Memory allocation tracing
- I/O latency analysis
- Network performance

**Security:**
- Runtime security monitoring
- Container escape detection
- Privilege escalation detection
- Network security

**Observability:**
- Distributed tracing
- Service mesh monitoring
- Application performance monitoring

### Common Gotchas

**Problem**: Permission denied
**Fix**: Need root and `CAP_BPF` capability

**Problem**: eBPF verifier rejection
**Fix**: eBPF has restrictions (no unbounded loops, limited instructions)

**Problem**: Can't compile eBPF
**Fix**: Need clang/llvm, Linux headers

**Problem**: Map full
**Fix**: Increase map size or use LRU maps

### Learning Resources

**Essential:**
- eBPF.io: https://ebpf.io/
- Cilium eBPF Go library: https://github.com/cilium/ebpf
- Linux kernel eBPF docs: https://www.kernel.org/doc/html/latest/bpf/

**Books:**
- "Linux Observability with BPF" - David Calavera, Lorenzo Fontana
- "BPF Performance Tools" - Brendan Gregg

**Tools to Study:**
- bpftrace: High-level eBPF tracing language
- bcc: BPF Compiler Collection
- Cilium: Container networking with eBPF
- Falco: Container security with eBPF

---

## Project 6: Virtual Machine Monitor (Hypervisor)

### Prerequisites & Requirements

**Before Starting:**
- **Completed**: Container Runtime project
- **Platform**: Linux (KVM), macOS (Hypervisor.framework), Windows (Hyper-V)
- **Hardware**: CPU with virtualization support (Intel VT-x or AMD-V)

**Knowledge Prerequisites:**
- **Must Know**:
  - Operating system architecture
  - CPU architecture (x86/x64)
  - Memory management (page tables, MMU)
  - I/O and interrupts
- **Will Learn**:
  - Virtualization technology
  - Hypervisor architecture
  - KVM (Kernel-based Virtual Machine)
  - Hardware-assisted virtualization
  - Virtual devices

**External Dependencies:**
- **Linux (KVM)**:
  - System: `/dev/kvm` device
  - No Go library needed, use `syscall` directly or:
  - `github.com/intel/govmm` - Go VMM library (reference)

**What to Install:**
```bash
# Check if virtualization is enabled
# Linux
egrep -c '(vmx|svm)' /proc/cpuinfo
# Should be > 0

# Check if KVM module loaded
lsmod | grep kvm

# Load KVM module
sudo modprobe kvm
sudo modprobe kvm_intel  # or kvm_amd

# Check /dev/kvm exists
ls -l /dev/kvm

mkdir simple-vmm
cd simple-vmm
go mod init github.com/yourusername/simple-vmm

go get golang.org/x/sys/unix
```

**Estimated Time:** 80-120 hours (extremely complex!)

### Overview
Build a simple virtual machine monitor (hypervisor) using KVM on Linux. This is the most advanced project - you'll learn how virtualization works at the lowest level. Used by QEMU, Firecracker, Cloud Hypervisor.

### What You'll Learn
- **Virtualization**: Hardware-assisted virtualization
- **KVM API**: Linux kernel virtualization interface
- **vCPU Management**: Virtual CPU creation and execution
- **Memory Management**: Guest physical memory
- **Device Emulation**: Virtual devices
- **Interrupt Handling**: Virtual interrupts
- **Boot Process**: Loading and booting guest OS

### Core Features
1. Create VM
2. Allocate guest memory
3. Create virtual CPUs (vCPUs)
4. Load guest kernel/firmware
5. Run vCPUs in threads
6. Handle VM exits (I/O, MMIO)
7. Basic device emulation (serial port)
8. Boot Linux kernel

### Architecture

```
┌─────────────────────────────────┐
│      Your Go Program            │
│  ┌──────────────────────────┐   │
│  │  VM Management           │   │
│  └──────────────────────────┘   │
│  ┌──────────────────────────┐   │
│  │  vCPU Threads            │   │
│  └──────────────────────────┘   │
│  ┌──────────────────────────┐   │
│  │  Device Emulation        │   │
│  └──────────────────────────┘   │
└─────────────────────────────────┘
            ↕ ioctl()
┌─────────────────────────────────┐
│  Linux Kernel (/dev/kvm)        │
│  ┌──────────────────────────┐   │
│  │     KVM Module           │   │
│  └──────────────────────────┘   │
└─────────────────────────────────┘
            ↕
┌─────────────────────────────────┐
│  Hardware (CPU, Memory)         │
│  Intel VT-x / AMD-V             │
└─────────────────────────────────┘
```

### Implementation Guide

#### Step 1: Open KVM Device

```go
func openKVM() (int, error) {
    fd, err := unix.Open("/dev/kvm", unix.O_RDWR, 0)
    if err != nil {
        return 0, err
    }

    // Check KVM API version
    version, _, _ := unix.Syscall(unix.SYS_IOCTL, uintptr(fd), KVM_GET_API_VERSION, 0)
    if version != 12 {
        return 0, fmt.Errorf("unsupported KVM API version: %d", version)
    }

    return fd, nil
}
```

#### Step 2: Create VM

```go
const KVM_CREATE_VM = 0xAE01

func createVM(kvmFD int) (int, error) {
    vmFD, _, errno := unix.Syscall(unix.SYS_IOCTL, uintptr(kvmFD), KVM_CREATE_VM, 0)
    if errno != 0 {
        return 0, errno
    }
    return int(vmFD), nil
}
```

#### Step 3: Allocate Guest Memory

```go
const KVM_SET_USER_MEMORY_REGION = 0x4020AE46

type kvmUserspaceMemoryRegion struct {
    slot          uint32
    flags         uint32
    guestPhysAddr uint64
    memorySize    uint64
    userspaceAddr uint64
}

func setMemory(vmFD int, size uint64) ([]byte, error) {
    // Allocate memory with mmap
    mem, err := unix.Mmap(-1, 0, int(size), unix.PROT_READ|unix.PROT_WRITE, unix.MAP_PRIVATE|unix.MAP_ANONYMOUS)
    if err != nil {
        return nil, err
    }

    // Tell KVM about this memory region
    region := kvmUserspaceMemoryRegion{
        slot:          0,
        flags:         0,
        guestPhysAddr: 0,  // Guest physical address 0
        memorySize:    size,
        userspaceAddr: uint64(uintptr(unsafe.Pointer(&mem[0]))),
    }

    _, _, errno := unix.Syscall(unix.SYS_IOCTL, uintptr(vmFD), KVM_SET_USER_MEMORY_REGION, uintptr(unsafe.Pointer(&region)))
    if errno != 0 {
        return nil, errno
    }

    return mem, nil
}
```

#### Step 4: Create vCPU

```go
const KVM_CREATE_VCPU = 0xAE41

func createVCPU(vmFD int, id int) (int, error) {
    vcpuFD, _, errno := unix.Syscall(unix.SYS_IOCTL, uintptr(vmFD), KVM_CREATE_VCPU, uintptr(id))
    if errno != 0 {
        return 0, errno
    }
    return int(vcpuFD), nil
}
```

#### Step 5: Run vCPU

```go
const KVM_RUN = 0xAE80

func runVCPU(vcpuFD int) error {
    for {
        _, _, errno := unix.Syscall(unix.SYS_IOCTL, uintptr(vcpuFD), KVM_RUN, 0)
        if errno != 0 {
            return errno
        }

        // Handle VM exit
        // Check exit reason from kvm_run structure
        // Handle I/O, MMIO, HLT, etc.
    }
}
```

### Project Milestones

1. **Hello World**: Boot and run a simple 16-bit bootloader
2. **Real Mode**: Run code in real mode (16-bit)
3. **Protected Mode**: Switch to protected mode (32-bit)
4. **Long Mode**: 64-bit mode
5. **Serial Port**: Emulate serial console
6. **Boot Linux**: Boot a minimal Linux kernel
7. **Network**: Virtual network device
8. **Disk**: Virtual block device

### Challenge Yourself

1. **Device Emulation**: Keyboard, mouse, disk, network
2. **Multicore**: Multiple vCPUs
3. **Snapshot/Restore**: Save and restore VM state
4. **Live Migration**: Move VM to another host
5. **Nested Virtualization**: Run VMs inside VMs
6. **Performance**: Optimize for speed
7. **PCI Devices**: Emulate PCI bus and devices
8. **UEFI**: Boot with UEFI firmware
9. **Debugging**: GDB stub for debugging guest
10. **Cloud Integration**: AWS Nitro Enclaves-like isolation

### Real-World Examples

**Firecracker** (AWS Lambda):
- Minimal VMM for serverless
- Fast boot (<125ms)
- Written in Rust
- Open source: https://github.com/firecracker-microvm/firecracker

**Cloud Hypervisor**:
- Modern VMM
- Written in Rust
- KVM-based
- Open source: https://github.com/cloud-hypervisor/cloud-hypervisor

**QEMU**:
- Full system emulator
- Can use KVM acceleration
- Very feature-rich
- Open source: https://www.qemu.org/

### Learning Resources

**Essential:**
- KVM API: https://www.kernel.org/doc/html/latest/virt/kvm/api.html
- Intel SDM: Intel Software Developer's Manual (x86 architecture)
- OSDev Wiki: https://wiki.osdev.org/

**Books:**
- "Virtual Machines" - James Smith, Ravi Nair
- "Programming Beyond the Visible" - Tiago Carvalho
- Intel/AMD processor manuals

**Articles:**
- "Using the KVM API" - LWN.net
- Firecracker design docs

### Common Gotchas

**Problem**: /dev/kvm not found
**Fix**: Load KVM kernel module, check virtualization enabled in BIOS

**Problem**: VM crashes immediately
**Fix**: Ensure guest memory is set up correctly, CPU state initialized

**Problem**: Guest hangs
**Fix**: Check interrupt handling, device emulation

**Problem**: Slow performance
**Fix**: Ensure using hardware virtualization (not emulation)

---

**You've reached the advanced level!** You can now:
- Build production systems from scratch
- Contribute to major open-source projects
- Design distributed architectures
- Optimize for performance and scalability
- Debug complex system issues

Keep building, keep learning! 🚀

---

# Observability & Monitoring Guide

## Integrating into Every Project

For **production-ready applications**, add comprehensive observability to all projects above. This section provides guidance on implementing logging, metrics, and tracing across your projects.

### Why Observability Matters

**Reality:**
- You can't fix what you can't see. 90% of production issues are diagnosed through logs, metrics, and traces.
- Observability isn't optional for production systems—it's how you debug, optimize, and prove reliability.
- These skills are expected in senior roles: knowing Prometheus, Grafana, and OpenTelemetry is standard.

**The Three Pillars:**
1. **Logs**: What happened (events, errors, debug info)
2. **Metrics**: How much/how many (counters, gauges, histograms)
3. **Traces**: Where time is spent (distributed request flows)

---

## Logging Implementation

### Prerequisites

**Tools to install:**
```bash
# Structured logging libraries
go get go.uber.org/zap
go get github.com/rs/zerolog

# Alternative: stdlib + structured output
go get golang.org/x/exp/slog  # Go 1.21+ has built-in slog
```

**Log aggregation (choose one):**
- **Loki** (Grafana's log aggregation) - lightweight, easy to start
- **OpenSearch** (if you built Project 3B)
- **Fluentd/Fluent Bit** - log forwarding to any backend

### What to Implement in Each Project

**Logger Setup:**
- Create logger instance with structured fields
- Configure log levels (debug, info, warn, error)
- Add context: request ID, user ID, service name
- Output as JSON for parsing

**What to Log:**
- **Requests**: HTTP endpoints, gRPC calls (method, path, status, duration)
- **Errors**: All errors with stack traces and context
- **State changes**: User created, file uploaded, job started/completed
- **Performance**: Slow queries (>100ms), timeouts
- **Security**: Auth attempts, rate limit hits

**Log Levels:**
- `DEBUG`: Detailed flow (disabled in production)
- `INFO`: Normal operations (server started, request completed)
- `WARN`: Recoverable issues (retry, fallback used)
- `ERROR`: Failures that need attention
- `FATAL`: Unrecoverable errors (shutdown)

**12-Factor Logging ([XI. Logs](https://12factor.net/logs)):**
- Treat logs as event streams
- Write to stdout/stderr (not files)
- Never manage log files in the app
- Let execution environment handle log routing (Docker, Kubernetes, systemd)
- Use structured logging (JSON) for parsing by log aggregators

**Best Practices:**
- Always include correlation/request ID for tracing requests
- Add structured fields (user_id, request_id) not just strings
- Log before and after external calls (DB, API)
- Never log sensitive data (passwords, tokens, PII)
- Sample debug logs (1% of requests) in production to reduce volume
- Follow [12-Factor XI. Logs](https://12factor.net/logs): Write to stdout/stderr, let environment handle routing

**Example Structure (Conceptual):**
- Initialize logger with service name, environment, version
- Create middleware that adds request ID to context
- Extract logger from context: `logger := ctx.Value("logger")`
- Log with fields: `logger.Info("user created", "user_id", id, "email", email)`

**Integration with Loki:**
- Install Promtail (log shipper) to forward logs to Loki
- Configure Promtail to read your application's JSON logs
- Query logs in Grafana using LogQL
- Create alerts on error rate spikes

---

## Metrics Implementation

### Prerequisites

**Tools to install:**
```bash
# Prometheus client
go get github.com/prometheus/client_golang/prometheus
go get github.com/prometheus/client_golang/prometheus/promauto
go get github.com/prometheus/client_golang/prometheus/promhttp
```

**Metrics backend:**
- **Prometheus** - pull-based metrics collection
- **Grafana** - visualization and dashboards
- **VictoriaMetrics** - high-performance alternative to Prometheus

### What to Implement in Each Project

**Metric Types to Use:**

1. **Counters** (always increasing):
   - HTTP requests total (labeled by method, path, status)
   - Errors total (by type, severity)
   - Jobs processed, messages sent, cache hits/misses

2. **Gauges** (can go up/down):
   - Active connections, goroutines
   - Queue length, memory usage
   - Current number of users online

3. **Histograms** (distribution of values):
   - Request duration (p50, p95, p99)
   - Response size
   - Query execution time
   - File upload size

4. **Summaries** (similar to histograms):
   - Use histograms instead (more flexible for aggregation)

**Key Metrics for Each Project Type:**

**Web Services (REST APIs, WebSocket servers):**
- `http_requests_total` - counter by method, path, status
- `http_request_duration_seconds` - histogram with buckets
- `http_requests_in_flight` - gauge of current requests
- `websocket_connections_active` - gauge

**CLI Tools:**
- `command_execution_duration_seconds` - histogram
- `command_executions_total` - counter by command, status
- `files_processed_total` - counter

**Background Jobs/Workers:**
- `jobs_processed_total` - counter by job type, status
- `jobs_in_queue` - gauge
- `job_duration_seconds` - histogram
- `job_failures_total` - counter

**Database Operations:**
- `db_queries_total` - counter by operation (select, insert, update, delete)
- `db_query_duration_seconds` - histogram
- `db_connections_active` - gauge
- `db_errors_total` - counter by type

**Cache Operations:**
- `cache_hits_total`, `cache_misses_total` - counters
- `cache_operations_duration_seconds` - histogram
- `cache_size_bytes` - gauge

**System Resources:**
- `process_cpu_seconds_total` - counter
- `process_resident_memory_bytes` - gauge
- `go_goroutines` - gauge (built-in)
- `go_gc_duration_seconds` - histogram (built-in)

**Implementation Pattern:**
- Register metrics at package initialization
- Create metrics registry
- Expose `/metrics` endpoint using `promhttp.Handler()`
- Instrument code: wrap handlers, increment counters, observe durations
- Use labels sparingly (high cardinality kills Prometheus)

**Middleware Pattern:**
- Create HTTP middleware that records metrics for all requests
- Measure duration, increment counters, track in-flight requests
- Add to all HTTP routes automatically

**Prometheus Setup:**
- Configure Prometheus to scrape your `/metrics` endpoint
- Set scrape interval (15s typical)
- Define recording rules for aggregations
- Create alerting rules for SLOs

**Grafana Dashboards:**
- Request rate (QPS), error rate, duration (RED metrics)
- Latency percentiles (p50, p95, p99)
- Saturation metrics (CPU, memory, connections)
- Business metrics (users, transactions)

---

## Distributed Tracing Implementation

### Prerequisites

**Tools to install:**
```bash
# OpenTelemetry
go get go.opentelemetry.io/otel
go get go.opentelemetry.io/otel/trace
go get go.opentelemetry.io/otel/exporters/jaeger
go get go.opentelemetry.io/otel/exporters/otlp/otlptrace
go get go.opentelemetry.io/otel/sdk/trace
go get go.opentelemetry.io/otel/sdk/resource
go get go.opentelemetry.io/contrib/instrumentation/net/http/otelhttp
```

**Tracing backends (choose one):**
- **Jaeger** - easy to start, good UI, open source
- **Tempo** (Grafana) - integrates with Loki and Prometheus
- **Zipkin** - another open source option

### What to Implement in Each Project

**Tracing Concepts:**
- **Trace**: Complete journey of a request through your system
- **Span**: Single operation within a trace (function call, DB query, HTTP request)
- **Context**: Carries trace info between functions/services

**What to Trace:**
- HTTP/gRPC requests (automatic with middleware)
- Database queries and commands
- External API calls
- File I/O operations
- Message queue operations
- Cache operations
- Function calls in critical paths

**Span Attributes to Add:**
- `http.method`, `http.url`, `http.status_code`
- `db.system`, `db.statement`, `db.operation`
- `user.id`, `request.id`
- Error details when span fails
- Custom business context

**Implementation Pattern:**
- Initialize OpenTelemetry tracer provider on startup
- Configure exporter (Jaeger, Tempo, OTLP)
- Create tracer for your service: `tracer := otel.Tracer("service-name")`
- Use HTTP middleware for automatic request tracing
- Manually create spans for important operations:
  - Start span: `ctx, span := tracer.Start(ctx, "operation-name")`
  - Always defer span.End()
  - Pass context through call chain
  - Add attributes: `span.SetAttributes(attribute.String("key", "value"))`
  - Record errors: `span.RecordError(err)` and `span.SetStatus(codes.Error, msg)`

**Context Propagation:**
- Always pass `context.Context` as first parameter
- Extract trace context from incoming requests (HTTP headers, message metadata)
- Inject trace context into outgoing requests
- OpenTelemetry middleware does this automatically for HTTP

**Sampling:**
- Trace 100% in development
- Use probabilistic sampling in production (e.g., 10% of requests)
- Always sample errors (head-based or tail-based sampling)
- Sample slow requests (>1s) at higher rate

**Correlation:**
- Add trace ID to logs: extract from span context
- Link logs, metrics, and traces using trace_id
- Grafana can jump from logs to traces to metrics

---

## Project-Specific Implementation Guide

### Basic Projects (1-6)

**Add to All:**
- Structured logging with request IDs
- Basic metrics: operations_total, duration_seconds, errors_total
- Expose `/metrics` endpoint (for CLI, log metrics to file or push to gateway)

**Project 1 (CLI Todo):**
- Log: command executed, file operations, errors
- Metrics: commands_total, operations_duration_seconds, todos_total
- No tracing needed (single process)

**Project 2 (Weather CLI):**
- Log: API calls, cache hits/misses, parsing errors
- Metrics: api_requests_total, cache_hit_ratio, response_time_seconds
- Trace: API request flow (fetch → parse → display)

**Project 3 (File Organizer):**
- Log: files scanned, moved, errors (permission denied, etc.)
- Metrics: files_processed_total, bytes_moved_total, scan_duration_seconds
- Trace: scan → categorize → move operations

**Project 4 (URL Shortener):**
- Log: URLs created, redirects, invalid requests
- Metrics: urls_created_total, redirects_total (by short_url), http_request_duration_seconds
- Trace: HTTP request → DB query → response

**Project 5 (RSS Aggregator):**
- Log: feeds fetched, parsing errors, new items
- Metrics: feeds_fetched_total, items_processed_total, fetch_duration_seconds, feed_errors_total
- Trace: fetch → parse → store flow

**Project 6 (Markdown Blog):**
- Log: pages rendered, file reads, template errors
- Metrics: pages_served_total, render_duration_seconds, http_requests_total
- Trace: HTTP request → read file → render template → response

### Intermediate Projects (7-18)

**Add to All:**
- Full structured logging with correlation IDs
- Complete RED metrics (Rate, Errors, Duration)
- Distributed tracing with span propagation
- Resource metrics (goroutines, memory, connections)
- Prometheus alerts for error rate and latency

**Project 7 (REST API):**
- Critical: Full HTTP instrumentation with all metrics types
- Trace database queries, auth middleware, business logic
- Log all CRUD operations with user context
- Dashboard: Request rate, latency percentiles, error rate by endpoint

**Project 8 (WebSocket Chat):**
- Metrics: connections_active, messages_sent_total, broadcast_duration_seconds
- Trace: message receive → broadcast → send flow
- Log: connections, disconnections, message routing
- Alert on connection spikes or message queue buildup

**Project 9 (File Sync Tool):**
- Metrics: files_synced_total, bytes_transferred, sync_duration_seconds, sync_conflicts_total
- Trace: change detection → conflict resolution → transfer
- Log: sync operations, conflicts, network errors
- Dashboard: Sync success rate, transfer speed, conflict frequency

**Project 10 (Web Scraper):**
- Metrics: pages_scraped_total, scrape_duration_seconds, parser_errors_total, rate_limit_hits_total
- Trace: fetch → parse → store pipeline
- Log: URLs scraped, rate limiting, parsing errors
- Alert on scraper failures or rate limit hits

**Project 11 (Process Monitor):**
- Metrics: processes_monitored, cpu_usage_percent, memory_usage_bytes, alerts_triggered_total
- This project generates metrics about OTHER processes
- Log: process starts/stops, threshold breaches
- Self-monitoring: Monitor the monitor itself

**Project 12 (Log Analyzer):**
- Metrics: logs_processed_total, patterns_matched_total, processing_rate_per_second
- Trace: read → parse → analyze → output
- Log: files processed, pattern matches, parse errors
- Dashboard: Processing throughput, pattern frequency

**Project 13 (System Monitor Dashboard):**
- This project visualizes metrics from other services
- Collect system metrics: CPU, memory, disk, network
- Expose as Prometheus metrics
- Create Grafana dashboard showing system health

**Project 14 (Custom Shell):**
- Metrics: commands_executed_total, command_duration_seconds, errors_total
- Log: command history, process lifecycle, errors
- Trace: command parsing → execution → output

**Project 15 (Packet Sniffer):**
- Metrics: packets_captured_total, bytes_captured, packet_rate_per_second, protocols_histogram
- Log: capture sessions, interesting packets (anomalies), errors
- Dashboard: Network traffic patterns, protocol distribution

**Project 16 (System Call Tracer):**
- Metrics: syscalls_traced_total, trace_duration_seconds, syscalls_by_type
- Log: traced programs, significant syscalls, trace errors
- Dashboard: Syscall frequency heatmap

**Project 17 (MongoDB/Redis):**
- CRITICAL: Database and cache metrics
- Metrics: db_queries_total, query_duration_seconds, cache_hit_ratio, connections_active
- Trace: Request → cache check → DB query → cache update → response
- Log: Slow queries (>100ms), cache evictions, connection pool exhaustion
- Dashboard: Query performance, cache effectiveness, connection pool usage

**Project 18 (OpenSearch):**
- Metrics: search_queries_total, query_duration_seconds, index_operations_total, search_errors_total
- Trace: Search request → query building → execution → result parsing
- Log: Search queries (for analytics), indexing operations, errors
- Dashboard: Search performance, index growth, query patterns

### Advanced Projects (19-21)

**Add to All:**
- Production-grade observability
- SLO tracking (99.9% availability, p99 < 100ms)
- Advanced alerting (anomaly detection, multi-window alerts)
- Performance profiling integration (pprof endpoints)

**Project 19 (FUSE Filesystem):**
- Metrics: operations_total (by type: read, write, open), operation_duration_seconds, errors_total, open_files_gauge
- Trace: FUSE operation → backend storage → response
- Log: Mount/unmount, file operations, errors
- Alert on slow operations or high error rates

**Project 20 (eBPF Monitor):**
- This project monitors kernel-level events
- Metrics: events_captured_total (by type), processing_latency_microseconds
- Log: eBPF program lifecycle, interesting events
- Dashboard: Kernel event patterns, system call distribution

**Project 21 (Hypervisor):**
- Metrics: vms_running, vcpu_usage_percent, vm_memory_bytes, io_operations_total, vm_lifecycle_events_total
- Trace: VM operations (start, stop, device access)
- Log: VM lifecycle, device emulation, errors
- Dashboard: VM resource usage, performance metrics

---

## Setting Up Observability Stack

### Quick Start (Docker Compose)

**What you need:**
- Prometheus (metrics)
- Loki (logs)
- Tempo (traces)
- Grafana (visualization)
- Promtail (log shipping)

**Setup Steps:**
1. Create `docker-compose.yml` with all services
2. Configure Prometheus to scrape your app's `/metrics` endpoint
3. Configure Promtail to ship logs from file or stdout
4. Configure OpenTelemetry to export traces to Tempo
5. Add data sources in Grafana
6. Import community dashboards or create custom ones

**Prometheus Configuration:**
- Add scrape config with your service endpoint
- Set scrape interval (15s)
- Define job name and labels

**Grafana Dashboards to Create:**
- **Service Overview**: Request rate, error rate, latency (RED)
- **System Resources**: CPU, memory, goroutines, GC
- **Business Metrics**: Users, transactions, conversions
- **Error Analysis**: Error types, frequency, affected endpoints
- **Performance**: Latency percentiles, slow endpoints, database query time

**Alerting Rules:**
- Error rate > 1% for 5 minutes
- p99 latency > 1s for 5 minutes
- Service down (no metrics scraped)
- Memory usage > 80%
- Goroutine leak (growing over time)

---

## Testing Observability

**How to Verify:**
- Generate load (use `hey`, `wrk`, or `ab`)
- Check metrics endpoint: `curl localhost:8080/metrics`
- Verify Prometheus scrapes: Check targets page
- Create test alerts and verify firing
- Trace a request end-to-end in Jaeger/Tempo
- Query logs in Grafana using LogQL
- Verify correlation: Find trace ID in logs, jump to trace

**Load Testing Commands:**
```bash
# Generate HTTP load
hey -n 10000 -c 100 http://localhost:8080/api/users

# Generate errors intentionally
for i in {1..100}; do curl http://localhost:8080/api/invalid; done

# Monitor metrics while testing
watch -n 1 'curl -s localhost:8080/metrics | grep http_requests'
```

---

## Best Practices Summary

**Logging:**
- Use structured logging (JSON) with consistent field names
- Include correlation IDs in all logs
- Log at appropriate levels
- Sample debug logs in production
- Never log sensitive data

**Metrics:**
- Follow naming conventions: `<namespace>_<subsystem>_<name>_<unit>`
- Use labels wisely (avoid high cardinality)
- Expose Go runtime metrics (goroutines, GC, memory)
- Create dashboards showing business impact, not just technical metrics
- Set up alerts based on SLOs

**Tracing:**
- Trace critical paths and external calls
- Keep span names concise and consistent
- Add meaningful attributes
- Sample intelligently (errors and slow requests at 100%, others less)
- Propagate context through entire call chain

**General:**
- Treat observability as a first-class feature, not an afterthought
- Test your observability: Can you debug production issues with your logs/metrics/traces?
- Document what you're measuring and why
- Review dashboards and alerts regularly
- Use observability to drive improvements (find slow queries, optimize hot paths)

---

## 12-Factor App Methodology Integration

### Applying 12-Factor Principles to Your Projects

The [12-Factor App](https://12factor.net/) is a methodology for building modern, scalable, maintainable software-as-a-service apps. Apply these principles to your intermediate and advanced projects:

**I. Codebase ([12factor.net/codebase](https://12factor.net/codebase))**
- One codebase tracked in Git, many deploys
- Use Git for all projects
- Same code deployed to dev, staging, production
- Use branches/tags for releases

**II. Dependencies ([12factor.net/dependencies](https://12factor.net/dependencies))**
- Explicitly declare and isolate dependencies
- Use `go.mod` and `go.sum` (you're already doing this!)
- Never rely on system-wide packages
- Vendor dependencies for reproducible builds: `go mod vendor`

**III. Config ([12factor.net/config](https://12factor.net/config))**
- Store config in environment variables, NOT in code
- No hardcoded URLs, credentials, or feature flags
- Use `.env` files for local dev (never commit!)
- Examples:
  - `DATABASE_URL=postgres://user:pass@host/db`
  - `REDIS_URL=redis://localhost:6379`
  - `API_KEY=your-api-key`
  - `LOG_LEVEL=info`
- Load with `os.Getenv()` or `github.com/joho/godotenv`

**IV. Backing Services ([12factor.net/backing-services](https://12factor.net/backing-services))**
- Treat databases, caches, queues as attached resources
- Connect via URLs from config
- Should be able to swap local DB for production DB without code changes
- Example: PostgreSQL (local) → RDS (production), same connection code

**V. Build, Release, Run ([12factor.net/build-release-run](https://12factor.net/build-release-run))**
- Strictly separate build and run stages
- **Build**: Compile code (`go build`)
- **Release**: Combine build with config (Docker image + env vars)
- **Run**: Execute release in environment
- Use CI/CD pipelines (GitHub Actions, GitLab CI)

**VI. Processes ([12factor.net/processes](https://12factor.net/processes))**
- Execute app as stateless processes
- Store state in backing services (database, Redis)
- No sticky sessions
- Any process can die and be replaced
- Example: Session data in Redis, not in-memory

**VII. Port Binding ([12factor.net/port-binding](https://12factor.net/port-binding))**
- Export services via port binding
- Self-contained: App includes web server (Go's `net/http`)
- No separate web server needed (not like PHP+Apache)
- Bind to port from `PORT` env var
- Example: `http.ListenAndServe(":" + os.Getenv("PORT"), handler)`

**VIII. Concurrency ([12factor.net/concurrency](https://12factor.net/concurrency))**
- Scale out via process model
- Run multiple instances of your app
- Let OS/container orchestrator handle processes
- Use goroutines for concurrency within process
- Example: Run 3 instances behind load balancer

**IX. Disposability ([12factor.net/disposability](https://12factor.net/disposability))**
- Fast startup and graceful shutdown
- Handle SIGTERM for shutdown
- Finish processing current requests
- Close database connections cleanly
- Example:
  ```go
  // Graceful shutdown pattern
  sigChan := make(chan os.Signal, 1)
  signal.Notify(sigChan, os.Interrupt, syscall.SIGTERM)
  <-sigChan
  ctx, cancel := context.WithTimeout(context.Background(), 30*time.Second)
  defer cancel()
  server.Shutdown(ctx)
  ```

**X. Dev/Prod Parity ([12factor.net/dev-prod-parity](https://12factor.net/dev-prod-parity))**
- Keep development and production similar
- Use same database type (PostgreSQL local and production)
- Same Go version
- Use Docker to ensure consistency
- Minimize time, personnel, and tools gap

**XI. Logs ([12factor.net/logs](https://12factor.net/logs))**
- Treat logs as event streams
- Write to stdout/stderr ONLY
- Don't manage log files in app
- Let environment route logs (Docker → CloudWatch, Kubernetes → Elasticsearch)
- Use structured logging (JSON)

**XII. Admin Processes ([12factor.net/admin-processes](https://12factor.net/admin-processes))**
- Run admin/maintenance tasks as one-off processes
- Use same codebase and config
- Examples: Database migrations, data backups, one-time scripts
- Run in same environment: `go run scripts/migrate.go`

### Checklist for Each Project

For intermediate and advanced projects, ensure:

- [ ] Configuration via environment variables (no hardcoded values)
- [ ] `go.mod` with all dependencies declared
- [ ] Logs to stdout/stderr (structured JSON format)
- [ ] Graceful shutdown handling
- [ ] Port from `PORT` env var (default to 8080)
- [ ] Database URL from environment
- [ ] Stateless design (state in DB/cache, not memory)
- [ ] Docker image for consistent deployment
- [ ] README with environment variables documented
- [ ] Health check endpoint (`/health` or `/readiness`)

### Example: 12-Factor Compliant Service

**Environment Variables (`.env`):**
```
DATABASE_URL=postgres://user:pass@localhost/db
REDIS_URL=redis://localhost:6379
PORT=8080
LOG_LEVEL=info
JWT_SECRET=your-secret-key
```

**Config Loading (`config/config.go`):**
```
// Load from environment, with defaults
type Config struct {
    DatabaseURL string
    RedisURL    string
    Port        string
    LogLevel    string
    JWTSecret   string
}

func Load() *Config {
    return &Config{
        DatabaseURL: getEnv("DATABASE_URL", "postgres://localhost/db"),
        RedisURL:    getEnv("REDIS_URL", "redis://localhost:6379"),
        Port:        getEnv("PORT", "8080"),
        LogLevel:    getEnv("LOG_LEVEL", "info"),
        JWTSecret:   getEnv("JWT_SECRET", ""),
    }
}
```

**Graceful Shutdown (`main.go`):**
```
func main() {
    cfg := config.Load()
    server := &http.Server{Addr: ":" + cfg.Port, Handler: handler}

    go func() {
        if err := server.ListenAndServe(); err != nil && err != http.ErrServerClosed {
            log.Fatal(err)
        }
    }()

    // Wait for interrupt
    sigChan := make(chan os.Signal, 1)
    signal.Notify(sigChan, os.Interrupt, syscall.SIGTERM)
    <-sigChan

    // Graceful shutdown
    ctx, cancel := context.WithTimeout(context.Background(), 30*time.Second)
    defer cancel()
    if err := server.Shutdown(ctx); err != nil {
        log.Printf("Shutdown error: %v", err)
    }
}
```

**Dockerfile (for consistent deployment):**
```dockerfile
# Build stage
FROM golang:1.21-alpine AS build
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN go build -o server .

# Run stage
FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=build /app/server .
EXPOSE 8080
CMD ["./server"]
```

**Health Check Endpoint:**
```go
func healthHandler(w http.ResponseWriter, r *http.Request) {
    // Check database connection
    if err := db.Ping(); err != nil {
        w.WriteHeader(http.StatusServiceUnavailable)
        json.NewEncoder(w).Encode(map[string]string{"status": "unhealthy"})
        return
    }
    json.NewEncoder(w).Encode(map[string]string{"status": "healthy"})
}
```

### Why 12-Factor Matters

**For Your Career:**
- Industry standard for cloud-native applications
- Expected knowledge for backend/DevOps roles
- Makes your projects professional-grade
- Demonstrates understanding of production systems

**For Your Code:**
- Easy to deploy to cloud platforms (Heroku, AWS, GCP, Azure)
- Works with Docker, Kubernetes, Cloud Run
- Easy to test (inject test database URLs)
- Easy to scale (just add more instances)
- Easy to maintain (clear separation of concerns)

**Real-World Impact:**
- Netflix, Heroku, Spotify use these principles
- Kubernetes assumes 12-factor apps
- Serverless platforms (AWS Lambda) expect this design
- Makes migration between clouds simple

---

# Software Design Patterns Project

## Project 22: Design Patterns Library & Demo System

### Prerequisites & Requirements

**Before Starting:**
- Completed at least 10 previous projects
- Strong understanding of interfaces and composition
- Comfortable with complex codebases
- Understanding of SOLID principles

**Knowledge Prerequisites:**
- **Must Know**:
  - Interfaces and interface composition
  - Struct embedding
  - Method receivers
  - Generics (Go 1.18+)
  - Concurrency patterns (goroutines, channels)
- **Should Know**:
  - Common code smells
  - When to abstract vs. when to keep simple
  - Testing and mocking
- **Nice to Have**:
  - Experience with design patterns in other languages
  - Read "Design Patterns" (Gang of Four) or similar

**System Requirements:**
- **Go**: 1.21+ (for generics and improved features)
- **Disk Space**: ~100MB
- **RAM**: 4GB recommended

**Go Concepts You'll Use:**
- Interfaces and type assertions
- Struct embedding (for inheritance-like patterns)
- Functional options pattern
- Context pattern
- Generics for reusable patterns

### Overview

Build a comprehensive library demonstrating all major design patterns, with real-world examples and tests. This project is your design patterns handbook in code.

**Goal**: Implement 23 classic design patterns + Go-specific patterns with practical examples.

**What You'll Learn:**
- When and why to use each pattern
- Go-idiomatic implementations (not Java translations)
- Trade-offs and alternatives
- Testing patterns
- Pattern combinations
- Anti-patterns to avoid

**Duration**: 4-6 weeks (implement 3-4 patterns per week)

### Features to Build

**Core Pattern Categories:**
1. **Creational Patterns** (6) - Object creation mechanisms
2. **Structural Patterns** (7) - Object composition
3. **Behavioral Patterns** (11) - Object communication
4. **Concurrency Patterns** (5) - Go-specific concurrent designs
5. **Architectural Patterns** (4) - High-level structures

**For Each Pattern:**
- Clean implementation
- Real-world example (not toys)
- Unit tests
- Documentation explaining when to use
- Comparison with alternative approaches

### Project Structure

```
design-patterns/
├── cmd/
│   └── demo/           # Interactive demo CLI
├── patterns/
│   ├── creational/
│   │   ├── singleton/
│   │   ├── factory/
│   │   ├── abstract_factory/
│   │   ├── builder/
│   │   ├── prototype/
│   │   └── object_pool/
│   ├── structural/
│   │   ├── adapter/
│   │   ├── bridge/
│   │   ├── composite/
│   │   ├── decorator/
│   │   ├── facade/
│   │   ├── flyweight/
│   │   └── proxy/
│   ├── behavioral/
│   │   ├── chain_of_responsibility/
│   │   ├── command/
│   │   ├── iterator/
│   │   ├── mediator/
│   │   ├── memento/
│   │   ├── observer/
│   │   ├── state/
│   │   ├── strategy/
│   │   ├── template_method/
│   │   ├── visitor/
│   │   └── interpreter/
│   ├── concurrency/
│   │   ├── worker_pool/
│   │   ├── pipeline/
│   │   ├── fan_in_out/
│   │   ├── circuit_breaker/
│   │   └── semaphore/
│   └── architectural/
│       ├── mvc/
│       ├── repository/
│       ├── dependency_injection/
│       └── event_sourcing/
├── examples/          # Real-world usage examples
└── docs/             # Pattern documentation
```

### Implementation Guide

#### Creational Patterns

**1. Singleton Pattern**

**What you need to create:**
- Thread-safe singleton using `sync.Once`
- Demonstrate why global variables aren't enough
- Show lazy initialization
- Example: Database connection pool, logger, configuration

**Key Concepts:**
- `sync.Once` for thread-safe initialization
- Package-level vs instance-level singleton
- Interface-based design for testing
- When NOT to use (dependency injection is often better)

**Anti-patterns to avoid:**
- Using global variables without synchronization
- Mutable singleton state
- Singleton as a god object

**2. Factory Pattern**

**What you need to create:**
- Simple factory: Function returns interface
- Factory method: Interface with creation method
- Example: Create different database drivers, notification senders, payment processors

**Key Concepts:**
- Return interfaces, not concrete types
- Register factories for extensibility
- Factory with configuration

**When to use:**
- Need to create different types based on input
- Want to decouple creation from usage
- Plugin systems

**3. Abstract Factory Pattern**

**What you need to create:**
- Factory that creates families of related objects
- Example: UI toolkit (Button, Window, ScrollBar) with different themes (Windows, Mac, Linux)
- Example: Cloud provider factory (AWS, GCP, Azure) creating related services (Storage, Compute, Database)

**Key Concepts:**
- Factory interface with multiple creation methods
- Ensures created objects are compatible
- Concrete factory for each family

**4. Builder Pattern**

**What you need to create:**
- Builder with method chaining
- Functional options pattern (Go-idiomatic)
- Director (optional) for complex builds
- Example: HTTP request builder, SQL query builder, configuration builder

**Key Concepts:**
- Separate object construction from representation
- Fluent interface (method chaining)
- Functional options: `func(builder)` pattern
- Validation in Build() method

**Functional Options Pattern (Go-specific):**
- More idiomatic than traditional builder
- Options are functions that modify struct
- Allows optional parameters
- Example: `NewServer(WithPort(8080), WithTimeout(30*time.Second))`

**5. Prototype Pattern**

**What you need to create:**
- Clone interface with deep copy
- Registry of prototypes
- Example: Cloning complex configuration objects, game entities, document templates

**Key Concepts:**
- Implement `Clone() T` method
- Deep copy vs shallow copy
- Use when creating from scratch is expensive

**6. Object Pool Pattern**

**What you need to create:**
- Reusable object pool with Get/Put
- Maximum size and blocking behavior
- Example: Database connection pool, worker pool, buffer pool

**Key Concepts:**
- `sync.Pool` for automatic pooling (GC-aware)
- Custom pool for controlled lifecycle
- Initialize/Reset objects on Get/Put
- Handle pool exhaustion (block, error, create new)

**When to use:**
- Object creation is expensive
- Objects are frequently created and destroyed
- Limited resources (connections, memory)

#### Structural Patterns

**1. Adapter Pattern**

**What you need to create:**
- Wrapper that converts one interface to another
- Example: Adapt third-party library to your interface, legacy system integration, different storage backends

**Key Concepts:**
- Implements target interface
- Wraps adaptee
- Translates calls

**When to use:**
- Integrate incompatible interfaces
- Wrap legacy code
- Support multiple implementations

**2. Bridge Pattern**

**What you need to create:**
- Separate abstraction from implementation
- Both can vary independently
- Example: Shape (abstraction) with different Renderers (implementation), database abstraction with different drivers

**Key Concepts:**
- Abstraction holds reference to implementation
- Implementation is an interface
- Both hierarchies can grow independently

**Difference from Adapter:**
- Adapter: Make existing interfaces work together
- Bridge: Design time separation of concerns

**3. Composite Pattern**

**What you need to create:**
- Tree structure of objects
- Treat individual objects and compositions uniformly
- Example: File system (files and directories), GUI components (widgets and containers), organizational hierarchy

**Key Concepts:**
- Component interface for both leaf and composite
- Composite holds slice of components
- Recursive operations

**When to use:**
- Part-whole hierarchies
- Want to treat individuals and groups the same

**4. Decorator Pattern**

**What you need to create:**
- Add behavior to objects dynamically
- Stack multiple decorators
- Example: HTTP middleware, stream readers/writers, logging decorator, caching decorator

**Key Concepts:**
- Decorator implements same interface as component
- Wraps component and adds behavior
- Can stack decorators
- io.Reader/Writer chain is classic example

**Difference from Inheritance:**
- More flexible (composition over inheritance)
- Can add/remove at runtime
- Combine behaviors in different ways

**5. Facade Pattern**

**What you need to create:**
- Simple interface to complex subsystem
- Hide complexity behind clean API
- Example: Unified API for multiple microservices, simplified database operations, complex library wrapper

**Key Concepts:**
- Provides simplified methods
- Delegates to subsystem components
- Doesn't add functionality, just simplifies

**When to use:**
- Complex subsystem with many classes
- Want to provide simple default behavior
- Decouple clients from subsystem

**6. Flyweight Pattern**

**What you need to create:**
- Share common state between many objects
- Separate intrinsic (shared) from extrinsic (unique) state
- Example: Character glyphs in text editor, game tiles, particle systems

**Key Concepts:**
- Flyweight factory caches and reuses objects
- Immutable shared state
- Pass unique state as parameters
- Reduce memory usage

**When to use:**
- Many similar objects
- High memory cost
- Most state can be shared

**7. Proxy Pattern**

**What you need to create:**
- Surrogate controlling access to object
- Types: Protection proxy, virtual proxy, remote proxy, caching proxy
- Example: Lazy loading, access control, caching layer, RPC client

**Key Concepts:**
- Implements same interface as real subject
- Controls access or adds behavior
- Transparent to client

**Types:**
- **Virtual Proxy**: Lazy initialization (create expensive object only when needed)
- **Protection Proxy**: Access control (check permissions)
- **Remote Proxy**: Represent object in different address space (RPC client)
- **Caching Proxy**: Cache results

#### Behavioral Patterns

**1. Chain of Responsibility**

**What you need to create:**
- Chain of handlers
- Each handler processes or passes to next
- Example: HTTP middleware chain, logging levels, approval workflows, event handling

**Key Concepts:**
- Handler interface with `Handle()` and `SetNext()`
- Each handler decides: process and stop, or pass to next
- Decouples sender from receiver

**When to use:**
- Multiple objects can handle request
- Don't know which handler in advance
- Want to avoid coupling sender to receiver

**2. Command Pattern**

**What you need to create:**
- Encapsulate request as object
- Support undo/redo
- Example: Transaction system, task queue, macro recording, editor operations

**Key Concepts:**
- Command interface with `Execute()` and `Undo()`
- Receiver: Object that performs actual work
- Invoker: Triggers commands
- Can queue, log, undo commands

**When to use:**
- Parameterize objects with operations
- Queue operations
- Support undo
- Log requests

**3. Iterator Pattern**

**What you need to create:**
- Access elements sequentially without exposing structure
- Example: Custom collection iteration, database result set, tree traversal

**Key Concepts:**
- Iterator interface: `Next() (T, bool)`
- Collection provides iterator
- Can have multiple iterators on same collection

**Go-idiomatic:**
- Use channels and goroutines for iteration
- Callback-based iteration: `collection.ForEach(func(item T))`
- Generic iterator with `iter.Seq` (Go 1.23+)

**4. Mediator Pattern**

**What you need to create:**
- Centralized communication between objects
- Objects don't reference each other directly
- Example: Chat room, air traffic control, GUI dialog coordination, event bus

**Key Concepts:**
- Mediator interface
- Colleagues register with mediator
- All communication through mediator
- Reduces coupling between colleagues

**When to use:**
- Many objects communicate in complex ways
- Want to centralize control logic
- Hard to reuse objects due to tight coupling

**5. Memento Pattern**

**What you need to create:**
- Capture and restore object state
- Without exposing internals
- Example: Editor undo/redo, game save states, transaction rollback

**Key Concepts:**
- Originator: Object whose state is saved
- Memento: Immutable snapshot of state
- Caretaker: Stores mementos

**Implementation:**
- Memento as opaque struct
- Only originator can read memento
- Caretaker stores but doesn't modify

**6. Observer Pattern**

**What you need to create:**
- One-to-many dependency
- When object changes, notify dependents
- Example: Event system, pub/sub, model-view update, real-time notifications

**Key Concepts:**
- Subject (observable) maintains list of observers
- Observer interface with `Update()` method
- Subject calls `Update()` on all observers when state changes

**Go-idiomatic:**
- Use channels for notifications
- Channel of channels pattern
- `context.Context` for cancellation

**Push vs Pull:**
- Push: Subject sends data to observers
- Pull: Observers query subject for data

**7. State Pattern**

**What you need to create:**
- Object changes behavior when state changes
- Example: TCP connection states, order processing, vending machine, player states

**Key Concepts:**
- State interface with methods for each action
- Context holds current state
- Each state implementation handles transitions
- Alternative to large switch/if statements

**When to use:**
- Object behavior depends on state
- Large conditionals based on state
- State transitions have complex logic

**8. Strategy Pattern**

**What you need to create:**
- Family of interchangeable algorithms
- Select algorithm at runtime
- Example: Sorting algorithms, compression methods, payment methods, routing strategies

**Key Concepts:**
- Strategy interface
- Context uses strategy interface
- Inject strategy (dependency injection)
- Can swap strategies at runtime

**When to use:**
- Multiple algorithms for same task
- Want to avoid conditionals
- Client chooses algorithm

**Difference from State:**
- Strategy: Client aware of strategies, chooses one
- State: Object not aware of states, states manage transitions

**9. Template Method Pattern**

**What you need to create:**
- Define algorithm skeleton
- Subclasses override specific steps
- Example: Data processing pipeline, test fixtures, document generator

**Key Concepts:**
- Abstract base with template method
- Template method calls hooks (abstract methods)
- Subclasses implement hooks

**Go implementation:**
- Use struct embedding
- Base struct with template method
- Embedded struct implements hooks
- Alternative: Pass functions as parameters (more flexible)

**10. Visitor Pattern**

**What you need to create:**
- Separate algorithm from object structure
- Add operations without modifying objects
- Example: AST traversal, file system operations, report generation

**Key Concepts:**
- Visitor interface with `Visit(element)` for each type
- Elements implement `Accept(visitor)`
- Double dispatch

**When to use:**
- Many unrelated operations on object structure
- Object structure rarely changes
- Operations change frequently

**Trade-offs:**
- Powerful but complex
- Adding new element types is hard
- Go interfaces make this less necessary

**11. Interpreter Pattern**

**What you need to create:**
- Interpret language or expressions
- Example: Query language, configuration DSL, arithmetic expressions, regex engine

**Key Concepts:**
- Grammar as class hierarchy
- Terminal and non-terminal expressions
- Context carries state
- Recursive interpretation

**When to use:**
- Simple grammar to interpret
- Efficiency not critical
- Alternative: Parser generators for complex languages

#### Concurrency Patterns (Go-Specific)

**1. Worker Pool Pattern**

**What you need to create:**
- Fixed number of workers processing jobs
- Job queue (buffered channel)
- Result collection
- Graceful shutdown
- Example: HTTP request pool, batch processing, task execution

**Key Concepts:**
- Jobs channel and results channel
- Workers read from jobs channel in loop
- Use `sync.WaitGroup` to wait for completion
- Use context for cancellation

**Implementation:**
- Create worker pool with N workers
- Each worker: `for job := range jobs { process(job) }`
- Send jobs to channel
- Close jobs channel when done
- Wait for all workers

**2. Pipeline Pattern**

**What you need to create:**
- Chain of processing stages
- Each stage is a goroutine
- Data flows through channels
- Example: Data processing pipeline, image processing, stream processing

**Key Concepts:**
- Each stage: input channel → process → output channel
- Fan-out: Multiple goroutines reading from same channel
- Fan-in: Multiple channels merged into one
- Composable stages

**Pattern:**
```
generate() → stage1() → stage2() → stage3() → consume()
   ↓           ↓          ↓          ↓           ↓
channel1  channel2   channel3   channel4
```

**3. Fan-Out/Fan-In Pattern**

**What you need to create:**
- Fan-out: Distribute work to multiple workers
- Fan-in: Merge results from multiple sources
- Example: Parallel API calls, distributed computation, load distribution

**Key Concepts:**
- One input channel, multiple workers reading (fan-out)
- Multiple output channels merged to one (fan-in)
- Use `sync.WaitGroup` to wait for all workers

**Fan-in implementation:**
- Start goroutine for each input channel
- Each goroutine forwards to output channel
- Close output when all inputs done

**4. Circuit Breaker Pattern**

**What you need to create:**
- Protect from cascading failures
- States: Closed (working), Open (failing), Half-Open (testing)
- Example: External API calls, database operations, microservice calls

**Key Concepts:**
- Track failures
- After threshold, open circuit (fast fail)
- After timeout, try one request (half-open)
- If succeeds, close circuit; if fails, stay open

**Implementation:**
- State machine (Closed → Open → Half-Open → Closed)
- Failure counter and timeout
- Thread-safe state transitions
- Return error immediately when open

**5. Semaphore Pattern**

**What you need to create:**
- Limit concurrent access to resource
- Bounded parallelism
- Example: Rate limiting, connection pool, resource quotas

**Key Concepts:**
- Use buffered channel as semaphore
- Acquire: Send to channel (blocks if full)
- Release: Receive from channel
- Capacity = buffer size

**Implementation:**
- Create buffered channel: `sem := make(chan struct{}, N)`
- Acquire: `sem <- struct{}{}`
- Release: `<-sem`
- Or use `golang.org/x/sync/semaphore` package

#### Architectural Patterns

**1. MVC Pattern (Model-View-Controller)**

**What you need to create:**
- Separate data, presentation, and logic
- Example: Web application structure

**Key Concepts:**
- Model: Data and business logic
- View: Presentation (templates, JSON responses)
- Controller: Handles requests, coordinates model and view

**Go implementation:**
- Handlers are controllers
- Structs/database are models
- Templates or JSON encoding are views

**2. Repository Pattern**

**What you need to create:**
- Abstract data access
- Interface for CRUD operations
- Example: Database access layer, storage abstraction

**Key Concepts:**
- Repository interface with methods: `Create`, `Read`, `Update`, `Delete`, `List`
- Implementations for different backends (SQL, NoSQL, in-memory)
- Business logic doesn't know storage details

**Benefits:**
- Testable (mock repository)
- Swappable backends
- Single place for data access logic

**3. Dependency Injection Pattern**

**What you need to create:**
- Inject dependencies rather than create them
- Example: Service initialization, testable components

**Key Concepts:**
- Constructor injection: Pass dependencies to `New()`
- Prefer interfaces to concrete types
- Dependency inversion principle
- Aligns with [12-Factor: IV. Backing Services](https://12factor.net/backing-services) - treat dependencies as attached resources

**12-Factor Connection:**
- Database, cache, message queue as injected dependencies
- Configure via environment variables
- Swap implementations without code changes
- Makes services portable across environments

**Go patterns:**
- Constructor functions: `NewService(db Database, cache Cache)`
- Config structs with interfaces
- Wire dependencies at startup
- Use dependency injection frameworks (wire, dig) for complex apps

**12-Factor Connection:**
- Aligns with Factor IV (Backing Services)
- Inject database, cache, queue interfaces
- Configure via environment variables
- Swap implementations without code changes
- Makes services portable across environments

**4. Event Sourcing Pattern**

**What you need to create:**
- Store events instead of current state
- Rebuild state by replaying events
- Example: Audit trail, temporal queries, CQRS systems

**Key Concepts:**
- Event store (append-only log)
- Events are immutable facts: "UserCreated", "OrderPlaced"
- Aggregate root applies events
- Projections/read models built from events

**Implementation:**
- Event interface with `Apply(aggregate)`
- Append events to store
- Load aggregate: fetch events and apply in order
- Snapshots for performance

---

### Testing Each Pattern

**What you need to create for each pattern:**

**Unit Tests:**
- Test pattern behavior
- Test edge cases
- Benchmark if performance-critical

**Example Tests:**
- Real-world usage scenario
- Show pattern solving actual problem
- Demonstrate benefits over alternatives

**Documentation:**
- When to use (problem statement)
- Pros and cons
- Go-specific considerations
- Common mistakes
- Alternative approaches

---

### Demo Application

**What you need to create:**

**Interactive CLI:**
- List all patterns by category
- Choose pattern to see demo
- Run example code
- Show output and explanation

**Features:**
- `./demo list` - Show all patterns
- `./demo show singleton` - Explain pattern
- `./demo run factory` - Run example
- `./demo compare adapter bridge` - Compare patterns

**Documentation Generator:**
- Generate markdown docs from code
- Include usage examples
- Create pattern catalog website

---

### Learning Path

**Week 1-2: Creational + Setup**
- Set up project structure
- Implement all 6 creational patterns
- Write tests and examples
- Document each pattern

**Week 3-4: Structural**
- Implement 7 structural patterns
- Real-world examples for each
- Compare similar patterns (Adapter vs Bridge, Decorator vs Proxy)

**Week 5: Behavioral (Part 1)**
- Implement Chain, Command, Iterator, Mediator, Memento, Observer
- Focus on patterns you'll use often

**Week 6: Behavioral (Part 2) + Concurrency**
- Implement State, Strategy, Template, Visitor, Interpreter
- Implement 5 concurrency patterns
- These are most important for Go

**Week 7: Architectural + Demo**
- Implement 4 architectural patterns
- Build demo application
- Write comprehensive documentation

**Week 8: Polish + Real Projects**
- Review all patterns
- Apply patterns to previous projects (refactor)
- Identify where patterns would help
- Create pattern decision tree (flowchart)

---

### Key Learnings

**Principles Behind Patterns:**
- Favor composition over inheritance
- Program to interfaces, not implementations
- Encapsulate what varies
- Depend on abstractions, not concretions
- Open/closed principle: Open for extension, closed for modification

**When NOT to Use Patterns:**
- YAGNI (You Ain't Gonna Need It) - Don't over-engineer
- Patterns add complexity - only use when needed
- Simple problems need simple solutions
- Go encourages simplicity - don't force patterns

**Go-Specific Insights:**
- Interfaces are implicit (duck typing)
- Composition through embedding (not inheritance)
- Concurrency patterns are first-class
- Prefer simple, readable code over clever patterns
- Standard library uses patterns extensively (learn from it)

---

### Anti-Patterns to Avoid

**Common Mistakes:**
- **Pattern Obsession**: Using patterns everywhere
- **Wrong Pattern**: Using pattern that doesn't fit problem
- **Over-Engineering**: Adding complexity without benefit
- **Cargo Cult**: Using pattern because "best practice" without understanding
- **God Object**: Singleton that does everything
- **Premature Abstraction**: Abstracting before you understand problem

**Go-Specific Anti-Patterns:**
- Forcing OOP inheritance patterns into Go
- Ignoring built-in concurrency primitives
- Complex interface hierarchies
- Mutable singletons with global state

---

### Advanced Challenges

**After completing basic implementation:**

1. **Pattern Combinations**: Implement complex systems using multiple patterns together
2. **Performance Analysis**: Benchmark pattern overhead vs. simple implementations
3. **Refactoring Exercise**: Take existing projects and apply appropriate patterns
4. **Pattern Detection Tool**: Build tool to detect patterns in codebases
5. **Anti-Pattern Linter**: Create linter that flags anti-patterns

---

### Resources

**Books:**
- "Design Patterns: Elements of Reusable Object-Oriented Software" (Gang of Four)
- "Head First Design Patterns"
- "Refactoring: Improving the Design of Existing Code" - Martin Fowler

**Go-Specific:**
- "100 Go Mistakes and How to Avoid Them" - Teiva Harsanyi
- Standard library source code (best examples of Go patterns)
- Go blog: https://go.dev/blog/

**Online:**
- Refactoring.guru - Visual pattern explanations
- SourceMaking.com - Pattern catalog

---

**This project is your design patterns reference.** Return to it whenever you need a pattern. Use it to level up your previous projects. Share it to teach others.

---

# Additional Projects: Complete Go & System Design Coverage

## Roadmap Coverage Analysis

These additional projects cover remaining topics from [roadmap.sh/golang](https://roadmap.sh/golang) and [roadmap.sh/system-design](https://roadmap.sh/system-design) that aren't fully addressed in previous projects.

---

## Project 23: Testing Framework & Advanced Testing

### Covers Go Roadmap Topics
- Testing (`testing` package)
- Benchmarking
- Fuzzing (Go 1.18+)
- Test Coverage
- Table-Driven Tests
- Mocking and Dependency Injection
- Integration Tests
- Property-Based Testing

### Prerequisites & Requirements

**Before Starting:**
- Completed 5+ previous projects
- Written basic tests with `testing` package
- Understanding of interfaces

**Knowledge Prerequisites:**
- **Must Know**: Basic test functions, `go test` command
- **Should Know**: Test assertions, error handling
- **Will Learn**: Advanced testing patterns, benchmarking, fuzzing, coverage analysis

**System Requirements:**
- Go 1.21+ (for fuzzing)
- 4GB RAM

### Overview

Build a comprehensive testing framework and test suite demonstrating all Go testing capabilities. Create reusable testing utilities and learn professional testing practices.

### What You'll Learn
- Table-driven tests (Go idiomatic pattern)
- Subtests with `t.Run()`
- Test helpers and fixtures
- Mocking with interfaces
- Benchmarking with `b.N`
- Fuzzing for finding edge cases
- Test coverage analysis
- Integration testing patterns
- Golden file testing
- Parallel test execution

### Core Features

1. **Test Utilities Library:**
   - Assertion helpers (`assertEqual`, `assertNil`, etc.)
   - Mock implementations for common interfaces
   - Test data generators
   - HTTP test helpers
   - Database test fixtures

2. **Demonstration Suite:**
   - Unit tests (functions, methods)
   - Table-driven tests
   - Subtests for organized test cases
   - Integration tests (database, HTTP)
   - Benchmark tests
   - Fuzz tests
   - Example tests (in documentation)

3. **Coverage Tools:**
   - Generate coverage reports
   - Visualize coverage
   - Track coverage over time
   - Set coverage thresholds

### Implementation Guide

#### Table-Driven Tests Pattern

**What you need to create:**
- Test struct with input and expected output
- Loop over test cases
- Use `t.Run()` for each case
- Clear test failure messages

**Example structure:**
```
tests := []struct {
    name     string
    input    int
    expected int
}{
    {"positive", 5, 25},
    {"zero", 0, 0},
    {"negative", -3, 9},
}
for _, tt := range tests {
    t.Run(tt.name, func(t *testing.T) {
        result := Square(tt.input)
        if result != tt.expected {
            t.Errorf("got %d, want %d", result, tt.expected)
        }
    })
}
```

#### Benchmarking

**What you need to create:**
- Benchmark functions with `Benchmark` prefix
- Use `b.N` for iterations
- Reset timer with `b.ResetTimer()`
- Prevent compiler optimizations

**Key concepts:**
- Measure allocations with `-benchmem`
- Compare benchmarks over time
- Profile hot paths
- Optimize based on data

#### Fuzzing (Go 1.18+)

**What you need to create:**
- Fuzz test with `Fuzz` prefix
- Property-based checks
- Corpus seed values
- Handle random inputs

**Use cases:**
- Find panics
- Validate input handling
- Discover edge cases
- Security testing

#### Mocking

**What you need to create:**
- Interface-based design
- Mock implementations
- Inject dependencies
- Verify mock calls

**Patterns:**
- Manual mocks (preferred in Go)
- Record calls for verification
- Return predefined results
- Assert expectations

### Project Structure

```
testing-framework/
├── assert/
│   ├── assert.go          # Assertion helpers
│   └── assert_test.go
├── mock/
│   ├── http.go           # HTTP mocks
│   ├── db.go             # Database mocks
│   └── time.go           # Time mocks
├── testdata/
│   ├── golden/           # Golden files
│   └── fixtures/         # Test data
├── examples/
│   ├── unit_test.go
│   ├── table_test.go
│   ├── integration_test.go
│   ├── benchmark_test.go
│   └── fuzz_test.go
└── coverage/
    └── coverage.sh       # Coverage scripts
```

### Testing Best Practices

**Test Organization:**
- One `_test.go` file per source file
- Use subtests for grouping
- Clear test names describing behavior
- Test public API, not internals

**Assertions:**
- Use clear error messages
- Show both expected and actual values
- Context about what failed
- Use helper functions

**Test Data:**
- Use `testdata/` directory
- Golden files for complex output
- Generate test data programmatically
- Keep tests deterministic

**Integration Tests:**
- Use build tags: `//go:build integration`
- Run separately: `go test -tags=integration`
- Use Docker for dependencies
- Clean up resources (defer)

### Commands

```bash
# Run all tests
go test ./...

# Run with coverage
go test -cover ./...
go test -coverprofile=coverage.out ./...
go tool cover -html=coverage.out

# Run benchmarks
go test -bench=. -benchmem

# Run specific test
go test -run TestMyFunc

# Run subtests
go test -run TestMyFunc/subtest_name

# Fuzzing
go test -fuzz=FuzzMyFunc -fuzztime=30s

# Parallel execution
go test -parallel=4 ./...

# Verbose output
go test -v ./...

# Integration tests
go test -tags=integration ./...
```

---

## Project 24: Message Queue & Event-Driven System

### Covers System Design Topics
- Message Queues
- Event-Driven Architecture
- Pub/Sub Pattern
- Background Jobs
- Asynchronous Processing
- At-Least-Once Delivery
- Dead Letter Queues
- Consumer Groups

### Prerequisites & Requirements

**Before Starting:**
- Completed REST API and Redis projects
- Understanding of concurrency
- Basic distributed systems knowledge

**System Requirements:**
- RabbitMQ, Kafka, or NATS
- Docker recommended
- 8GB RAM

### Overview

Build a complete message queue system with producers, consumers, dead letter queues, and monitoring. Implements event-driven architecture for decoupled services.

### What You'll Learn
- Message queue patterns
- At-least-once vs exactly-once delivery
- Consumer group balancing
- Message persistence
- Backpressure handling
- Circuit breaker for consumers
- DLQ (Dead Letter Queue)
- Event sourcing patterns

### Core Features

1. **Producer Service:**
   - Publish messages to queue
   - Message serialization (JSON, Protobuf)
   - Batching for performance
   - Confirm delivery
   - Retry with exponential backoff

2. **Consumer Service:**
   - Subscribe to topics/queues
   - Process messages concurrently
   - Acknowledge messages
   - Handle failures (DLQ)
   - Graceful shutdown

3. **Queue Management:**
   - Create/delete queues
   - Configure retention
   - Monitor queue depth
   - Purge messages
   - View DLQ

4. **Use Case Examples:**
   - Order processing pipeline
   - Email notification system
   - Image processing queue
   - Log aggregation

### Implementation Guide

#### RabbitMQ Integration

**What you need to create:**
- Connection pool management
- Channel per goroutine pattern
- Declare exchanges and queues
- Bind queues to exchanges
- Publish with confirms
- Consume with acknowledgment

**Exchange types:**
- Direct: Routing key match
- Topic: Pattern matching
- Fanout: Broadcast to all
- Headers: Attribute matching

#### Kafka Integration

**What you need to create:**
- Producer with Sarama library
- Consumer group for load balancing
- Partition assignment
- Offset management
- Batching messages

**Key concepts:**
- Topics and partitions
- Consumer groups
- Offset commits
- Rebalancing

#### Consumer Patterns

**What you need to create:**
- Worker pool pattern
- Message handler interface
- Automatic retry logic
- DLQ for poison messages
- Circuit breaker integration
- Metrics and observability

**Error handling:**
- Transient errors: Retry
- Permanent errors: DLQ
- Max retries exceeded: DLQ
- Processing timeout: Requeue

### Project Structure

```
message-queue/
├── producer/
│   ├── producer.go       # Message publisher
│   └── batch.go          # Batch publishing
├── consumer/
│   ├── consumer.go       # Message consumer
│   ├── worker.go         # Worker pool
│   └── handler.go        # Message handlers
├── queue/
│   ├── rabbitmq.go       # RabbitMQ client
│   ├── kafka.go          # Kafka client
│   └── nats.go           # NATS client
├── models/
│   └── message.go        # Message types
├── examples/
│   ├── order/            # Order processing
│   ├── email/            # Email sender
│   └── image/            # Image processor
└── monitoring/
    └── metrics.go        # Queue metrics
```

---

## Project 25: Distributed Cache & Rate Limiter

### Covers System Design Topics
- Caching Strategies
- Cache-Aside Pattern
- Write-Through Cache
- Write-Behind Cache
- Cache Invalidation
- Distributed Caching
- Rate Limiting Algorithms
- Token Bucket
- Leaky Bucket
- Sliding Window

### Prerequisites & Requirements

**Before Starting:**
- Completed Redis project
- Understanding of caching concepts
- Concurrent programming skills

### Overview

Build a distributed caching system with multiple eviction policies and a production-ready rate limiter with multiple algorithms.

### What You'll Learn
- LRU, LFU, FIFO eviction policies
- Distributed cache consistency
- Cache stampede prevention
- Rate limiting algorithms
- Token bucket implementation
- Sliding window counters
- Distributed rate limiting

### Core Features

1. **Cache Implementation:**
   - In-memory cache with eviction
   - LRU (Least Recently Used)
   - LFU (Least Frequently Used)
   - TTL-based expiration
   - Size-based eviction
   - Thread-safe operations

2. **Distributed Cache:**
   - Consistent hashing
   - Sharding strategy
   - Replication
   - Cache coherence
   - Redis cluster integration

3. **Rate Limiter:**
   - Token bucket algorithm
   - Leaky bucket algorithm
   - Fixed window counter
   - Sliding window counter
   - Distributed rate limiting (Redis)

4. **Cache Patterns:**
   - Cache-aside
   - Read-through
   - Write-through
   - Write-behind
   - Refresh-ahead

### Implementation Guide

#### LRU Cache

**What you need to create:**
- Doubly linked list for LRU order
- Hash map for O(1) lookup
- Move to front on access
- Evict least recently used when full
- Thread-safe with mutex

#### Rate Limiter - Token Bucket

**What you need to create:**
- Bucket with tokens
- Refill rate per second
- Consume tokens on request
- Block/reject when empty
- Distributed with Redis

**Algorithm:**
- Initialize bucket with capacity
- Refill tokens at steady rate
- Each request consumes N tokens
- Allow burst up to capacity

#### Sliding Window Rate Limiter

**What you need to create:**
- Redis sorted set with timestamps
- Remove old entries outside window
- Count entries in current window
- Allow if under limit

### Project Structure

```
distributed-cache/
├── cache/
│   ├── lru.go            # LRU cache
│   ├── lfu.go            # LFU cache
│   ├── ttl.go            # TTL cache
│   └── distributed.go    # Distributed cache
├── ratelimit/
│   ├── token_bucket.go
│   ├── leaky_bucket.go
│   ├── fixed_window.go
│   ├── sliding_window.go
│   └── distributed.go    # Redis-based
├── consistent/
│   └── hash.go           # Consistent hashing
└── examples/
    └── api/              # API with rate limiting
```

---

## Project 26: Service Mesh & Load Balancer

### Covers System Design Topics
- Load Balancing
- Layer 4 vs Layer 7 Load Balancing
- Load Balancing Algorithms
- Health Checks
- Service Discovery
- Circuit Breaker
- Retry Logic
- Timeout Handling
- Horizontal Scaling

### Prerequisites & Requirements

**Before Starting:**
- Completed network programming projects
- Understanding of microservices
- TCP/HTTP protocol knowledge

### Overview

Build a production-grade load balancer with multiple algorithms, health checking, and service discovery. Implements service mesh patterns.

### What You'll Learn
- Round robin load balancing
- Least connections algorithm
- Weighted load balancing
- Consistent hashing for sticky sessions
- Active/passive health checks
- Service registry integration
- Retry and timeout policies
- Connection pooling

### Core Features

1. **Load Balancing Algorithms:**
   - Round robin
   - Least connections
   - Weighted round robin
   - IP hash (sticky sessions)
   - Random selection
   - Least response time

2. **Health Checking:**
   - HTTP health endpoints
   - TCP connection checks
   - Passive health monitoring
   - Configurable intervals
   - Automatic removal of unhealthy backends

3. **Service Discovery:**
   - Register/deregister services
   - DNS-based discovery
   - Consul integration
   - etcd integration
   - Watch for changes

4. **Advanced Features:**
   - Circuit breaker per backend
   - Request retry logic
   - Connection pooling
   - SSL/TLS termination
   - WebSocket support
   - Metrics and monitoring

### Implementation Guide

#### Load Balancing Algorithm

**What you need to create:**
- Backend pool management
- Selection strategy interface
- Round robin with atomic counter
- Least connections tracker
- Weight distribution
- Health status tracking

#### Health Checking

**What you need to create:**
- Health checker goroutine per backend
- HTTP GET to health endpoint
- Mark backend healthy/unhealthy
- Configurable thresholds
- Exponential backoff for checks

#### Reverse Proxy

**What you need to create:**
- HTTP request forwarding
- Response proxying
- Header manipulation
- Connection pooling
- Error handling and retries

### Project Structure

```
load-balancer/
├── balancer/
│   ├── balancer.go       # Main load balancer
│   ├── roundrobin.go
│   ├── leastconn.go
│   ├── weighted.go
│   └── consistent.go     # Consistent hashing
├── health/
│   ├── checker.go        # Health checking
│   └── passive.go        # Passive monitoring
├── discovery/
│   ├── registry.go       # Service registry
│   ├── consul.go
│   └── etcd.go
├── proxy/
│   └── reverse.go        # Reverse proxy
└── pool/
    └── connection.go     # Connection pool
```

---

## Project 27: Context & Cancellation Patterns

### Covers Go Roadmap Topics
- Context package
- Context propagation
- Timeout handling
- Cancellation signals
- Context values
- Graceful shutdown
- Request-scoped data

### Prerequisites & Requirements

**Before Starting:**
- Completed 10+ projects
- Understanding of goroutines and channels
- HTTP server experience

### Overview

Build a comprehensive demonstration of Go's context package patterns. Covers timeout handling, cancellation propagation, and graceful shutdown.

### What You'll Learn
- Context creation and propagation
- Timeout contexts
- Cancellation contexts
- Context values (when to use)
- Context in HTTP handlers
- Context in database queries
- Graceful goroutine shutdown
- Context best practices

### Core Features

1. **Context Patterns:**
   - Timeout propagation through call stack
   - Manual cancellation
   - Deadline enforcement
   - Cascading cancellation

2. **HTTP Integration:**
   - Request context usage
   - Context-aware middleware
   - Client timeout configuration
   - Server graceful shutdown

3. **Database Integration:**
   - Query cancellation
   - Transaction timeout
   - Connection context

4. **Worker Patterns:**
   - Context-aware workers
   - Graceful worker shutdown
   - Pipeline cancellation

### Implementation Guide

#### Context Patterns

**What you need to create:**

**Timeout Context:**
- Create with `context.WithTimeout()`
- Check `ctx.Done()` channel
- Handle `context.DeadlineExceeded`
- Clean up on timeout

**Cancellation Context:**
- Create with `context.WithCancel()`
- Call cancel function to stop
- Propagate to child goroutines
- Select on `ctx.Done()`

**Context Values:**
- Use for request-scoped data only
- Not for passing parameters
- Use type-safe accessors
- Avoid in library code

#### HTTP Handler Pattern

**What you need to create:**
- Extract context from request
- Pass to downstream calls
- Set timeouts per endpoint
- Cancel on client disconnect

#### Database Query Pattern

**What you need to create:**
- Pass context to all queries
- Handle cancellation gracefully
- Rollback transaction on context done
- Close connections properly

### Project Structure

```
context-patterns/
├── examples/
│   ├── timeout.go
│   ├── cancellation.go
│   ├── values.go
│   └── pipeline.go
├── http/
│   ├── handlers.go       # Context in HTTP
│   └── middleware.go
├── database/
│   └── queries.go        # Context in DB
└── worker/
    └── pool.go           # Context in workers
```

---

## Project 28: gRPC Microservices

### Covers Go & System Design Topics
- gRPC
- Protocol Buffers
- Microservices Architecture
- Service-to-Service Communication
- Streaming (Unary, Server, Client, Bidirectional)
- Service Discovery
- API Gateway
- Distributed Tracing

### Prerequisites & Requirements

**Before Starting:**
- Completed REST API project
- Understanding of microservices
- Protocol Buffers knowledge

**System Requirements:**
- protoc compiler
- gRPC plugins
- Docker

### Overview

Build a complete microservices system using gRPC for inter-service communication. Includes API gateway, service discovery, and observability.

### What You'll Learn
- Protocol Buffers (protobuf)
- gRPC service definition
- Unary RPC calls
- Server streaming
- Client streaming
- Bidirectional streaming
- gRPC interceptors (middleware)
- Error handling in gRPC
- Service mesh integration

### Core Features

1. **Multiple Microservices:**
   - User service (authentication)
   - Product service (catalog)
   - Order service (orders)
   - Notification service (async)

2. **Communication Patterns:**
   - Unary calls (request-response)
   - Server streaming (feed updates)
   - Client streaming (batch upload)
   - Bidirectional (chat, real-time sync)

3. **Infrastructure:**
   - API Gateway (gRPC-Gateway or custom)
   - Service discovery (Consul/etcd)
   - Load balancing (client-side)
   - Distributed tracing (OpenTelemetry)

4. **Production Features:**
   - Authentication with interceptors
   - Rate limiting
   - Circuit breaker
   - Retries with exponential backoff
   - Health checking

### Implementation Guide

#### Protocol Buffers

**What you need to create:**

**Service Definition (.proto):**
- Define messages (request/response)
- Define service with RPC methods
- Use appropriate types
- Document with comments

**Generate Code:**
```bash
protoc --go_out=. --go-grpc_out=. service.proto
```

#### gRPC Server

**What you need to create:**
- Implement service interface
- Create gRPC server
- Register services
- Add interceptors (middleware)
- Graceful shutdown

#### gRPC Client

**What you need to create:**
- Create client connection
- Call service methods
- Handle errors
- Configure timeouts
- Connection pooling

#### Streaming

**What you need to create:**

**Server Streaming:**
- Send multiple responses
- Stream results progressively
- Handle client disconnect

**Client Streaming:**
- Receive multiple requests
- Aggregate data
- Send final response

**Bidirectional:**
- Full-duplex communication
- Concurrent send/receive
- Real-time interaction

### Project Structure

```
grpc-microservices/
├── proto/
│   ├── user.proto
│   ├── product.proto
│   ├── order.proto
│   └── notification.proto
├── services/
│   ├── user/
│   ├── product/
│   ├── order/
│   └── notification/
├── gateway/
│   └── api_gateway.go    # HTTP to gRPC
├── discovery/
│   └── consul.go
└── client/
    └── client.go         # gRPC clients
```

---

## Project 29: Distributed Tracing & APM

### Covers System Design & Observability Topics
- Distributed Tracing
- OpenTelemetry
- Spans and Traces
- Context Propagation
- Trace Sampling
- Performance Monitoring
- Error Tracking
- Service Dependencies

### Prerequisites & Requirements

**Before Starting:**
- Completed observability section
- Microservices experience
- Understanding of distributed systems

### Overview

Implement comprehensive distributed tracing across microservices using OpenTelemetry. Integrate with Jaeger, Zipkin, or Tempo.

### What You'll Learn
- OpenTelemetry SDK setup
- Automatic instrumentation
- Manual span creation
- Trace context propagation
- Baggage for cross-service data
- Sampling strategies
- Trace analysis
- Performance bottleneck detection

### Core Features

1. **Instrumentation:**
   - HTTP server/client auto-instrumentation
   - Database query tracing
   - External API call tracing
   - Custom span creation
   - Span attributes and events

2. **Context Propagation:**
   - W3C Trace Context
   - Inject/extract headers
   - gRPC metadata propagation
   - Message queue trace headers

3. **Sampling:**
   - Always sample (dev)
   - Probabilistic sampling (prod)
   - Tail-based sampling
   - Error-based sampling

4. **Analysis:**
   - Service dependency graph
   - Latency percentiles
   - Error rate per service
   - Critical path analysis

### Implementation Guide

#### OpenTelemetry Setup

**What you need to create:**
- Initialize tracer provider
- Configure exporter (Jaeger/Zipkin/OTLP)
- Set service name and attributes
- Register global tracer
- Graceful shutdown

#### HTTP Instrumentation

**What you need to create:**
- Wrap HTTP handler with otelhttp
- Automatic span creation per request
- Propagate context to downstream calls
- Inject trace headers in responses

#### Custom Spans

**What you need to create:**
- Start span: `tracer.Start(ctx, "operation")`
- Add attributes: `span.SetAttributes(...)`
- Record errors: `span.RecordError(err)`
- Set status: `span.SetStatus(codes.Error, "msg")`
- Always defer `span.End()`

### Project Structure

```
distributed-tracing/
├── tracing/
│   ├── setup.go          # OpenTelemetry setup
│   └── middleware.go     # HTTP middleware
├── services/
│   ├── frontend/
│   ├── backend/
│   └── database/
└── examples/
    └── trace_demo.go     # Tracing examples
```

---

## Project 30: Authentication & Authorization System

### Covers Security Topics
- JWT Authentication
- OAuth 2.0
- Session Management
- Password Hashing (bcrypt, argon2)
- RBAC (Role-Based Access Control)
- Permission System
- API Keys
- Rate Limiting
- CSRF Protection
- Security Best Practices

### Prerequisites & Requirements

**Before Starting:**
- Completed REST API project
- Understanding of security concepts
- Database experience

### Overview

Build a complete authentication and authorization system with multiple auth methods, role-based access control, and security best practices.

### What You'll Learn
- JWT token generation and validation
- Refresh token rotation
- OAuth 2.0 flows
- Password hashing best practices
- Permission modeling
- RBAC implementation
- API key management
- Security headers
- Rate limiting per user

### Core Features

1. **Authentication Methods:**
   - Email/password with JWT
   - OAuth 2.0 (Google, GitHub)
   - API keys for services
   - Magic links (passwordless)
   - Two-factor authentication (TOTP)

2. **Authorization:**
   - Role-based access control (RBAC)
   - Permission system
   - Resource-based permissions
   - Attribute-based access control (ABAC)

3. **Security Features:**
   - Password complexity requirements
   - Account lockout after failed attempts
   - Email verification
   - Password reset flow
   - Session management
   - Audit logging

4. **Token Management:**
   - Access token (short-lived)
   - Refresh token (long-lived)
   - Token rotation
   - Token blacklisting
   - JWT claims validation

### Implementation Guide

#### JWT Authentication

**What you need to create:**
- Generate JWT with claims
- Sign with secret key
- Validate signature
- Check expiration
- Refresh token flow
- Blacklist for revocation

#### OAuth 2.0

**What you need to create:**
- Authorization code flow
- Redirect to provider
- Exchange code for token
- Get user profile
- Store in database

#### RBAC System

**What you need to create:**
- Roles table (admin, user, editor)
- Permissions table (read, write, delete)
- Role-permission mapping
- User-role assignment
- Permission checking middleware

#### Password Security

**What you need to create:**
- Hash with bcrypt (cost 12+)
- Or argon2id (memory-hard)
- Salt automatically included
- Compare hash securely
- Never log passwords

### Project Structure

```
auth-system/
├── auth/
│   ├── jwt.go            # JWT handling
│   ├── oauth.go          # OAuth flows
│   └── password.go       # Password hashing
├── rbac/
│   ├── roles.go
│   ├── permissions.go
│   └── middleware.go
├── models/
│   ├── user.go
│   ├── role.go
│   └── permission.go
└── providers/
    ├── google.go
    └── github.go
```

---

## Roadmap Coverage Summary

### Go Language Topics (roadmap.sh/golang)

**Covered in Projects:**
- ✅ Variables, Constants, Data Types - Projects 1-3
- ✅ Functions, Methods, Interfaces - All projects
- ✅ Pointers - Projects 3-6
- ✅ Structs - All projects
- ✅ Arrays, Slices, Maps - All projects
- ✅ Loops, Conditionals - All projects
- ✅ Error Handling - All projects
- ✅ Goroutines, Channels - Projects 5, 8, 10-16
- ✅ **Testing** - **Project 23** (comprehensive)
- ✅ **Context** - **Project 27** (detailed patterns)
- ✅ HTTP Package - Projects 4, 7, 13
- ✅ Database/SQL - Projects 7, 17
- ✅ JSON - Projects 2, 4, 7
- ✅ File I/O - Projects 3, 5, 6
- ✅ TCP/Networking - Projects 9, 14-16
- ✅ **gRPC** - **Project 28** (full implementation)
- ✅ WebSockets - Project 8 (chat)
- ✅ Logging - Observability section
- ✅ ORM - Project 7 (raw SQL), can add GORM
- ✅ Redis - Project 17
- ✅ MongoDB - Project 17
- ✅ OpenSearch - Project 17
- ✅ Docker - Multiple projects
- ✅ Kubernetes - Project 21 (container orchestration concepts)

### System Design Topics (roadmap.sh/system-design)

**Covered in Projects:**
- ✅ **Load Balancing** - **Project 26** (full implementation)
- ✅ **Caching** - **Project 25** (LRU, LFU, distributed)
- ✅ **Rate Limiting** - **Project 25** (token bucket, sliding window)
- ✅ **Message Queues** - **Project 24** (RabbitMQ, Kafka)
- ✅ **Service Discovery** - **Project 26** (Consul, etcd)
- ✅ CAP Theorem - Discussed in distributed projects
- ✅ Consistency Patterns - Redis/MongoDB projects
- ✅ Availability Patterns - Load balancer, health checks
- ✅ **Replication** - MongoDB project (replica sets)
- ✅ Sharding - Mentioned in cache/database projects
- ✅ **Distributed Tracing** - **Project 29** (OpenTelemetry)
- ✅ Microservices - **Project 28** (gRPC services)
- ✅ **API Gateway** - **Project 28** (gRPC-Gateway)
- ✅ Horizontal Scaling - Load balancer, stateless design
- ✅ CDN - Covered in theory
- ✅ Database Patterns - Federation, denormalization
- ✅ **Auth** - **Project 30** (JWT, OAuth, RBAC)
- ✅ Security - Multiple projects
- ✅ Monitoring - Observability section (Prometheus, Grafana)
- ✅ 12-Factor App - Dedicated section

### New Projects Added (23-30)

These 8 new projects complete your roadmap coverage:

1. **Project 23: Testing Framework** - Advanced Go testing
2. **Project 24: Message Queue System** - Event-driven architecture
3. **Project 25: Distributed Cache & Rate Limiter** - Caching strategies
4. **Project 26: Load Balancer & Service Mesh** - Load balancing algorithms
5. **Project 27: Context Patterns** - Go context package mastery
6. **Project 28: gRPC Microservices** - Modern service communication
7. **Project 29: Distributed Tracing** - OpenTelemetry APM
8. **Project 30: Auth System** - Security and authorization

**Total Project Count: 30 Projects**
- Basic: 6 projects
- Intermediate: 18 projects
- Advanced: 6 projects

---

## Complete Learning Path

**Months 1-2: Foundations** (Projects 1-6)
- Go basics
- CLI tools
- File handling
- HTTP basics

**Months 3-4: Backend Development** (Projects 7-12)
- REST APIs
- Databases
- WebSockets
- Background jobs

**Months 5-6: Systems Programming** (Projects 13-18)
- OS interaction
- Network programming
- NoSQL databases
- Search engines

**Months 7-9: Advanced Systems** (Projects 19-22)
- Kernel programming
- eBPF
- Hypervisors
- Design patterns

**Months 10-12: Production Systems** (Projects 23-30)
- Testing & quality
- Distributed systems
- Service mesh
- Security
- Observability

---

**You now have complete coverage of Go language features and system design patterns.** Every topic from roadmap.sh/golang and roadmap.sh/system-design is addressed.

---

# Specialized Projects

## Project 31: CI/CD Pipeline Builder

### Covers DevOps Topics
- Continuous Integration
- Continuous Deployment
- GitHub Actions
- GitLab CI
- Pipeline as Code
- Automated Testing
- Docker Build & Push
- Deployment Automation

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 23 (Testing)
- Understanding of Git workflows
- Docker knowledge
- Cloud platform experience (optional)

**System Requirements:**
- GitHub or GitLab account
- Docker Hub account
- Cloud account (AWS/GCP/Heroku) for deployment

### Overview

Build a complete CI/CD pipeline that automatically tests, builds, and deploys Go applications. Covers GitHub Actions, Docker builds, and multi-environment deployments.

### What You'll Learn
- GitHub Actions workflows
- GitLab CI pipelines
- Automated testing in CI
- Docker multi-stage builds
- Semantic versioning
- Environment-specific deploys
- Rollback strategies
- Blue-green deployments

### Core Features

1. **CI Pipeline:**
   - Trigger on push/PR
   - Run linters (golangci-lint)
   - Run unit tests
   - Run integration tests
   - Code coverage reports
   - Security scanning (gosec)

2. **Build Pipeline:**
   - Docker image build
   - Multi-arch builds (amd64, arm64)
   - Image tagging (git SHA, version)
   - Push to registry (Docker Hub, ECR, GCR)
   - Generate release notes

3. **CD Pipeline:**
   - Deploy to staging automatically
   - Deploy to production on tag
   - Health checks post-deploy
   - Rollback on failure
   - Notify on Slack/Discord

4. **Environments:**
   - Development (auto-deploy)
   - Staging (auto-deploy from main)
   - Production (manual approval or tag)
   - Review apps for PRs

### Implementation Guide

#### GitHub Actions Workflow

**What you need to create:**

**`.github/workflows/ci.yml`:**
```yaml
name: CI
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-go@v4
        with:
          go-version: '1.21'
      - name: Test
        run: |
          go test -v -coverprofile=coverage.out ./...
          go tool cover -html=coverage.out -o coverage.html
      - name: Upload coverage
        uses: codecov/codecov-action@v3
```

**`.github/workflows/deploy.yml`:**
```yaml
name: Deploy
on:
  push:
    tags: ['v*']
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Build Docker image
        run: docker build -t myapp:${{ github.ref_name }} .
      - name: Push to registry
        run: docker push myapp:${{ github.ref_name }}
      - name: Deploy to production
        run: ./scripts/deploy.sh production
```

#### Multi-Stage Dockerfile

**What you need to create:**
```dockerfile
# Build stage
FROM golang:1.21-alpine AS builder
WORKDIR /app
COPY go.* ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 go build -ldflags="-w -s" -o server .

# Final stage
FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /app/server .
EXPOSE 8080
CMD ["./server"]
```

#### Deployment Script

**What you need to create:**
- SSH to server
- Pull new Docker image
- Stop old container
- Start new container
- Run health checks
- Rollback if unhealthy

### Project Structure

```
ci-cd-pipeline/
├── .github/
│   └── workflows/
│       ├── ci.yml
│       ├── deploy.yml
│       └── release.yml
├── scripts/
│   ├── deploy.sh
│   ├── rollback.sh
│   └── health-check.sh
├── deployments/
│   ├── docker-compose.yml
│   └── k8s/
└── docs/
    └── deployment.md
```

### Key Concepts

**Semantic Versioning:**
- Major.Minor.Patch (1.2.3)
- Breaking.Feature.Fix
- Tag releases: `v1.2.3`

**Deployment Strategies:**
- Rolling update (Kubernetes)
- Blue-green deployment
- Canary releases
- Feature flags

**Security:**
- Store secrets in CI secrets
- Scan for vulnerabilities
- Sign Docker images
- Use private registries

#### Jenkins Pipeline

**What you need to create:**

**`Jenkinsfile`:**
```groovy
pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'docker.io'
        IMAGE_NAME = 'myapp'
        GO_VERSION = '1.21'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                sh '''
                    go test -v -coverprofile=coverage.out ./...
                    go tool cover -func=coverage.out
                '''
            }
        }

        stage('Lint') {
            steps {
                sh 'golangci-lint run ./...'
            }
        }

        stage('Security Scan') {
            steps {
                sh 'gosec ./...'
            }
        }

        stage('Build') {
            steps {
                sh 'go build -o app .'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Docker Push') {
            when {
                branch 'main'
            }
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-credentials') {
                        docker.image("${IMAGE_NAME}:${env.BUILD_NUMBER}").push()
                        docker.image("${IMAGE_NAME}:${env.BUILD_NUMBER}").push('latest')
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            when {
                branch 'main'
            }
            steps {
                sh './scripts/deploy.sh staging'
            }
        }

        stage('Deploy to Production') {
            when {
                tag 'v*'
            }
            steps {
                input message: 'Deploy to production?', ok: 'Deploy'
                sh './scripts/deploy.sh production'
            }
        }
    }

    post {
        always {
            junit '**/test-results/*.xml'
            publishHTML([
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'coverage',
                reportFiles: 'index.html',
                reportName: 'Coverage Report'
            ])
        }
        success {
            slackSend(color: 'good', message: "Build ${env.BUILD_NUMBER} succeeded")
        }
        failure {
            slackSend(color: 'danger', message: "Build ${env.BUILD_NUMBER} failed")
        }
    }
}
```

**Jenkins Setup Steps:**

**What you need to configure:**

1. **Install Jenkins:**
   - Use Docker: `docker run -p 8080:8080 jenkins/jenkins:lts`
   - Or install natively on server
   - Access at http://localhost:8080
   - Complete setup wizard

2. **Install Required Plugins:**
   - Go Plugin
   - Docker Pipeline
   - GitHub Integration
   - Slack Notification
   - HTML Publisher
   - JUnit Plugin

3. **Configure Credentials:**
   - Add GitHub credentials (username + token)
   - Add Docker Hub credentials
   - Add deployment SSH keys
   - Add Slack webhook URL

4. **Create Pipeline Job:**
   - New Item → Pipeline
   - Configure Git repository URL
   - Set branch to build (main, develop)
   - Pipeline script from SCM
   - Point to Jenkinsfile in repo

5. **Configure Webhooks:**
   - GitHub webhook to trigger Jenkins builds
   - URL: `http://jenkins-url/github-webhook/`
   - Events: Push, Pull Request

6. **Set up Build Agents:**
   - Configure Jenkins nodes/agents
   - Install Go on agents
   - Install Docker on agents
   - Label agents appropriately

**Jenkins vs GitHub Actions vs GitLab CI:**

| Feature | Jenkins | GitHub Actions | GitLab CI |
|---------|---------|----------------|-----------|
| Self-hosted | Yes (required) | Optional | Optional |
| Cost | Free (infrastructure cost) | Free tier limited | Free tier limited |
| Flexibility | Very high | Medium | High |
| Setup complexity | High | Low | Low |
| Plugin ecosystem | Massive | Growing | Built-in |
| UI | Traditional | Modern | Modern |
| Best for | Enterprise, complex pipelines | GitHub projects | GitLab projects |

**When to use Jenkins:**
- Need full control over infrastructure
- Complex, multi-stage pipelines
- Integration with many tools
- On-premise requirements
- Existing Jenkins investment

**Multi-Branch Pipeline:**

**What you need to create:**
- Automatically discover branches
- Build feature branches
- Deploy dev/staging from branches
- Deploy production from tags

```groovy
// Different behavior per branch
if (env.BRANCH_NAME == 'main') {
    // Deploy to staging
} else if (env.BRANCH_NAME.startsWith('PR-')) {
    // Deploy to review environment
} else if (env.TAG_NAME?.startsWith('v')) {
    // Deploy to production
}
```

**Shared Libraries:**

**What you need to create:**
- Reusable pipeline code
- Custom steps and functions
- Organization-wide standards

Create in separate repo `jenkins-shared-library`:
```groovy
// vars/buildGo.groovy
def call(Map config) {
    pipeline {
        agent any
        stages {
            stage('Build') {
                steps {
                    sh "go build -o ${config.output} ."
                }
            }
        }
    }
}
```

Use in Jenkinsfile:
```groovy
@Library('jenkins-shared-library') _
buildGo(output: 'myapp')
```

**Jenkins Best Practices:**

1. **Use Declarative Pipeline** - Easier to maintain
2. **Store Jenkinsfile in repo** - Version control
3. **Use shared libraries** - DRY principle
4. **Parallelize stages** - Faster builds
5. **Cache dependencies** - Speed up builds
6. **Clean workspace** - Prevent build issues
7. **Set timeouts** - Prevent hung builds
8. **Use credentials plugin** - Never hardcode secrets
9. **Monitor build times** - Optimize slow stages
10. **Archive artifacts** - Keep build outputs

---

## Project 32: Kubernetes Operator

### Covers Cloud-Native Topics
- Kubernetes API
- Custom Resource Definitions (CRDs)
- Controllers
- Reconciliation Loops
- Client-go Library
- Operator Pattern
- State Management
- Event Handling

### Prerequisites & Requirements

**Before Starting:**
- Completed Projects 21 (Hypervisor), 28 (gRPC)
- Kubernetes experience
- Understanding of control loops

**System Requirements:**
- Kubernetes cluster (minikube, kind, or cloud)
- kubectl installed
- kubebuilder or operator-sdk

### Overview

Build a Kubernetes operator that manages custom resources. Implements the operator pattern with controllers, reconciliation loops, and event handling.

### What You'll Learn
- Kubernetes API fundamentals
- Custom Resource Definitions
- Controller pattern
- Reconciliation loops
- Watch and event handling
- Leader election
- Finalizers
- Admission webhooks

### Core Features

1. **Custom Resources:**
   - Define CRD (e.g., Database, Application)
   - Spec and Status fields
   - Validation rules
   - Subresources (status, scale)

2. **Controller:**
   - Watch for resource changes
   - Reconcile desired vs actual state
   - Create/update/delete child resources
   - Handle errors gracefully
   - Exponential backoff on failures

3. **Lifecycle Management:**
   - Resource creation
   - Updates (rolling, recreate)
   - Deletion with finalizers
   - Garbage collection

4. **Advanced Features:**
   - Leader election (HA)
   - Admission webhooks (validation)
   - Status conditions
   - Events for debugging

### Implementation Guide

#### Define CRD

**What you need to create:**
```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: databases.example.com
spec:
  group: example.com
  versions:
    - name: v1
      served: true
      storage: true
      schema:
        openAPIV3Schema:
          type: object
          properties:
            spec:
              type: object
              properties:
                size:
                  type: string
                version:
                  type: string
            status:
              type: object
  scope: Namespaced
  names:
    plural: databases
    singular: database
    kind: Database
```

#### Controller Implementation

**What you need to create:**
- Client-go informers and listers
- Workqueue for events
- Reconcile function
- Create deployments/services for custom resource
- Update status

**Reconciliation loop:**
1. Get desired state from custom resource
2. Get actual state from cluster
3. Compare and determine actions
4. Apply changes
5. Update status
6. Requeue if needed

#### Operator Deployment

**What you need to create:**
- RBAC roles and bindings
- Deployment for operator
- Service account
- Leader election config

### Project Structure

```
k8s-operator/
├── api/
│   └── v1/
│       ├── database_types.go
│       └── zz_generated.deepcopy.go
├── controllers/
│   └── database_controller.go
├── config/
│   ├── crd/
│   ├── rbac/
│   └── manager/
└── main.go
```

### Tools

**Kubebuilder:**
```bash
# Install
curl -L -o kubebuilder https://go.kubebuilder.io/dl/latest/$(go env GOOS)/$(go env GOARCH)
chmod +x kubebuilder && mv kubebuilder /usr/local/bin/

# Create project
kubebuilder init --domain example.com
kubebuilder create api --group app --version v1 --kind Database
```

**Operator SDK:**
```bash
# Install
brew install operator-sdk

# Create project
operator-sdk init --domain=example.com --repo=github.com/user/database-operator
operator-sdk create api --group=app --version=v1 --kind=Database --resource --controller
```

---

## Project 33: Profiling & Performance Optimization

### Covers Performance Topics
- pprof Profiling
- CPU Profiling
- Memory Profiling
- Goroutine Profiling
- Blocking Profiling
- Mutex Profiling
- Benchmarking
- Memory Optimization
- Escape Analysis

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 7 (REST API)
- Completed Project 23 (Testing)
- Understanding of Go runtime

### Overview

Master Go's profiling tools and optimization techniques. Learn to identify bottlenecks, reduce allocations, and optimize hot paths.

### What You'll Learn
- CPU profiling with pprof
- Memory profiling and heap analysis
- Goroutine leak detection
- Benchmark-driven optimization
- Escape analysis
- Inlining and compiler optimizations
- Lock contention analysis
- GC tuning

### Core Features

1. **Profiling Integration:**
   - HTTP endpoints for pprof
   - CPU profile generation
   - Heap profile analysis
   - Goroutine dumps
   - Trace collection

2. **Benchmarking Suite:**
   - Micro-benchmarks
   - Allocation tracking
   - Comparative benchmarks
   - Regression detection

3. **Optimization Techniques:**
   - Reduce allocations
   - Use sync.Pool
   - Avoid reflection
   - Optimize hot paths
   - Batch processing

4. **Analysis Tools:**
   - Flame graphs
   - pprof UI
   - Trace viewer
   - Memory leak detection

### Implementation Guide

#### Enable pprof

**What you need to create:**
```go
import _ "net/http/pprof"

func main() {
    go func() {
        log.Println(http.ListenAndServe("localhost:6060", nil))
    }()
    // Your application
}
```

#### CPU Profiling

**Commands:**
```bash
# Collect 30s CPU profile
curl http://localhost:6060/debug/pprof/profile?seconds=30 > cpu.prof

# Analyze
go tool pprof cpu.prof
# Commands: top, list, web

# Flame graph
go tool pprof -http=:8080 cpu.prof
```

#### Memory Profiling

**Commands:**
```bash
# Heap profile
curl http://localhost:6060/debug/pprof/heap > heap.prof

# Analyze allocations
go tool pprof -alloc_space heap.prof

# Analyze in-use memory
go tool pprof -inuse_space heap.prof
```

#### Benchmarking

**What you need to create:**
```go
func BenchmarkMyFunc(b *testing.B) {
    b.ReportAllocs() // Report allocations
    for i := 0; i < b.N; i++ {
        MyFunc()
    }
}

// Table-driven benchmarks
func BenchmarkSizes(b *testing.B) {
    sizes := []int{10, 100, 1000, 10000}
    for _, size := range sizes {
        b.Run(fmt.Sprintf("size=%d", size), func(b *testing.B) {
            for i := 0; i < b.N; i++ {
                processData(size)
            }
        })
    }
}
```

#### Optimization Patterns

**Reduce Allocations:**
```go
// Bad: New slice every call
func bad() []byte {
    return []byte("result")
}

// Good: Reuse buffer
var bufPool = sync.Pool{
    New: func() interface{} {
        return new(bytes.Buffer)
    },
}

func good() []byte {
    buf := bufPool.Get().(*bytes.Buffer)
    defer bufPool.Put(buf)
    buf.Reset()
    buf.WriteString("result")
    return buf.Bytes()
}
```

**Avoid String Concatenation:**
```go
// Bad: Many allocations
func bad(items []string) string {
    result := ""
    for _, item := range items {
        result += item + ","
    }
    return result
}

// Good: Single allocation
func good(items []string) string {
    return strings.Join(items, ",")
}
```

### Project Structure

```
profiling-optimization/
├── examples/
│   ├── cpu_intensive.go
│   ├── memory_intensive.go
│   └── concurrent.go
├── benchmarks/
│   ├── string_benchmark_test.go
│   ├── allocation_benchmark_test.go
│   └── comparison_test.go
├── optimized/
│   └── optimized_versions.go
└── analysis/
    ├── cpu.prof
    ├── heap.prof
    └── reports/
```

### Optimization Checklist

- [ ] Profile before optimizing
- [ ] Benchmark to verify improvements
- [ ] Check allocations with `-benchmem`
- [ ] Use `sync.Pool` for temporary objects
- [ ] Avoid `interface{}` in hot paths
- [ ] Use `strings.Builder` for concatenation
- [ ] Preallocate slices when size known
- [ ] Avoid reflection in tight loops
- [ ] Use buffered channels appropriately
- [ ] Consider escape analysis (`-gcflags="-m"`)

---

## Project 34: Payment Processing System

### Covers Integration & Business Logic
- Payment Gateway Integration (Stripe)
- Webhooks
- Idempotency
- Retry Logic
- Transaction Management
- PCI Compliance Basics
- Refunds and Disputes
- Subscription Management

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 7 (REST API)
- Completed Project 30 (Auth System)
- Understanding of financial transactions

**System Requirements:**
- Stripe account (test mode)
- PostgreSQL for transaction records
- Redis for idempotency keys

### Overview

Build a production-ready payment processing system with Stripe integration. Handles one-time payments, subscriptions, webhooks, refunds, and idempotency.

### What You'll Learn
- Stripe API integration
- Payment intent flow
- Webhook signature verification
- Idempotency keys
- Double-entry bookkeeping
- Transaction atomicity
- PCI DSS basics
- Handling payment failures

### Core Features

1. **Payment Methods:**
   - Credit/debit cards (via Stripe)
   - Save payment methods
   - Set default payment method
   - 3D Secure (SCA compliance)

2. **One-Time Payments:**
   - Create payment intent
   - Confirm payment
   - Handle authentication (3DS)
   - Capture or cancel
   - Receipt generation

3. **Subscriptions:**
   - Create subscription plans
   - Subscribe customers
   - Upgrade/downgrade plans
   - Proration handling
   - Trial periods
   - Subscription cancellation

4. **Webhooks:**
   - payment_intent.succeeded
   - payment_intent.payment_failed
   - customer.subscription.updated
   - charge.refunded
   - Signature verification
   - Idempotent processing

5. **Financial Operations:**
   - Refunds (full/partial)
   - Dispute handling
   - Transaction history
   - Balance tracking
   - Payout management

### Implementation Guide

#### Stripe Integration

**What you need to create:**
```go
import "github.com/stripe/stripe-go/v75"

func init() {
    stripe.Key = os.Getenv("STRIPE_SECRET_KEY")
}

// Create payment intent
params := &stripe.PaymentIntentParams{
    Amount:   stripe.Int64(2000), // $20.00
    Currency: stripe.String("usd"),
    Customer: stripe.String(customerID),
}
pi, err := paymentintent.New(params)
```

#### Webhook Handling

**What you need to create:**
- Verify webhook signature
- Parse event type
- Process idempotently
- Return 200 quickly (process async)
- Retry failed events

**Idempotency:**
```go
// Store webhook events by ID
func ProcessWebhook(eventID string, event stripe.Event) error {
    // Check if already processed
    if redis.Exists("webhook:" + eventID) {
        return nil // Already handled
    }

    // Process event
    err := handleEvent(event)
    if err != nil {
        return err
    }

    // Mark as processed
    redis.Set("webhook:"+eventID, "1", 24*time.Hour)
    return nil
}
```

#### Database Schema

**What you need to create:**
```sql
CREATE TABLE transactions (
    id UUID PRIMARY KEY,
    user_id UUID NOT NULL,
    stripe_payment_intent_id VARCHAR(255),
    amount_cents INT NOT NULL,
    currency VARCHAR(3),
    status VARCHAR(50),
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);

CREATE TABLE subscriptions (
    id UUID PRIMARY KEY,
    user_id UUID NOT NULL,
    stripe_subscription_id VARCHAR(255),
    plan_id UUID,
    status VARCHAR(50),
    current_period_start TIMESTAMP,
    current_period_end TIMESTAMP,
    cancel_at_period_end BOOLEAN
);
```

### Project Structure

```
payment-system/
├── stripe/
│   ├── client.go         # Stripe client wrapper
│   ├── payments.go       # Payment operations
│   ├── subscriptions.go  # Subscription management
│   └── webhooks.go       # Webhook handlers
├── models/
│   ├── transaction.go
│   ├── subscription.go
│   └── customer.go
├── handlers/
│   ├── checkout.go
│   ├── subscription.go
│   └── webhook.go
└── migrations/
    └── *.sql
```

### Security Considerations

**PCI Compliance:**
- Never store card numbers
- Use Stripe Elements (client-side)
- Only store Stripe customer/payment method IDs
- Log access to payment data
- Use HTTPS only

**Webhook Security:**
- Verify Stripe signature
- Use HTTPS endpoint
- Process idempotently
- Rate limit webhook endpoint

**Best Practices:**
- Use test mode during development
- Implement retry logic
- Log all payment events
- Monitor for fraud
- Handle all edge cases

---

## Project 35: Multi-Cloud Storage Abstraction

### Covers Cloud Integration
- AWS S3
- Google Cloud Storage
- Azure Blob Storage
- Abstraction Layers
- Presigned URLs
- Multipart Uploads
- Cloud Provider Independence
- Cost Optimization

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 7 (REST API)
- Completed Project 9 (File Sync)
- Understanding of cloud services

**System Requirements:**
- AWS account (free tier)
- GCP account (free tier)
- Azure account (optional)

### Overview

Build a unified storage abstraction layer that works with AWS S3, Google Cloud Storage, and Azure Blob Storage. Allows switching providers without code changes.

### What You'll Learn
- S3 API (AWS SDK)
- GCS API (Google Cloud SDK)
- Azure Blob API
- Interface-based abstraction
- Presigned URLs
- Multipart uploads for large files
- Cross-cloud migration
- Cost comparison

### Core Features

1. **Unified Interface:**
   - Upload file
   - Download file
   - List objects
   - Delete object
   - Get metadata
   - Copy/move objects

2. **Advanced Operations:**
   - Multipart upload (>5MB files)
   - Resume uploads
   - Presigned URLs (temporary access)
   - Batch operations
   - Object versioning

3. **Multi-Cloud:**
   - AWS S3 implementation
   - Google Cloud Storage implementation
   - Azure Blob Storage implementation
   - Local filesystem (for testing)
   - Switch provider via config

4. **Optimization:**
   - Concurrent uploads
   - Chunked downloads
   - Compression before upload
   - CDN integration
   - Cost tracking

### Implementation Guide

#### Storage Interface

**What you need to create:**
```go
type Storage interface {
    Upload(ctx context.Context, key string, data io.Reader) error
    Download(ctx context.Context, key string) (io.ReadCloser, error)
    Delete(ctx context.Context, key string) error
    List(ctx context.Context, prefix string) ([]Object, error)
    GetPresignedURL(ctx context.Context, key string, ttl time.Duration) (string, error)
}

type Object struct {
    Key          string
    Size         int64
    LastModified time.Time
    ETag         string
}
```

#### AWS S3 Implementation

**What you need to create:**
```go
import "github.com/aws/aws-sdk-go/service/s3"

type S3Storage struct {
    client *s3.S3
    bucket string
}

func (s *S3Storage) Upload(ctx context.Context, key string, data io.Reader) error {
    _, err := s.client.PutObjectWithContext(ctx, &s3.PutObjectInput{
        Bucket: aws.String(s.bucket),
        Key:    aws.String(key),
        Body:   aws.ReadSeekCloser(data),
    })
    return err
}
```

#### Google Cloud Storage Implementation

**What you need to create:**
```go
import "cloud.google.com/go/storage"

type GCSStorage struct {
    client *storage.Client
    bucket string
}

func (g *GCSStorage) Upload(ctx context.Context, key string, data io.Reader) error {
    wc := g.client.Bucket(g.bucket).Object(key).NewWriter(ctx)
    defer wc.Close()
    _, err := io.Copy(wc, data)
    return err
}
```

#### Factory Pattern

**What you need to create:**
```go
func NewStorage(provider string) (Storage, error) {
    switch provider {
    case "s3":
        return NewS3Storage(config.S3Config)
    case "gcs":
        return NewGCSStorage(config.GCSConfig)
    case "azure":
        return NewAzureStorage(config.AzureConfig)
    case "local":
        return NewLocalStorage(config.LocalPath)
    default:
        return nil, errors.New("unknown provider")
    }
}
```

### Project Structure

```
multi-cloud-storage/
├── storage/
│   ├── interface.go      # Storage interface
│   ├── s3.go            # AWS S3 implementation
│   ├── gcs.go           # Google Cloud Storage
│   ├── azure.go         # Azure Blob Storage
│   └── local.go         # Local filesystem
├── uploader/
│   └── multipart.go     # Multipart upload logic
├── examples/
│   ├── upload.go
│   ├── download.go
│   └── migrate.go       # Cross-cloud migration
└── config/
    └── providers.yaml
```

### Cost Optimization

**Strategies:**
- Use appropriate storage classes (S3 Glacier, GCS Nearline)
- Set lifecycle policies (auto-delete old files)
- Compress before upload
- Use CloudFront/CDN for downloads
- Monitor egress costs
- Batch operations

**Cost Comparison:**
```go
type CostEstimator struct {
    storage   Storage
    pricePerGB float64
    pricePerRequest float64
}

func (c *CostEstimator) EstimateUploadCost(sizeGB float64, requests int) float64 {
    return (sizeGB * c.pricePerGB) + (float64(requests) * c.pricePerRequest)
}
```

---

## Project 36: Reflection Deep Dive

### Covers Advanced Go Topics
- reflect Package
- Type Introspection
- Dynamic Method Calls
- Struct Tag Parsing
- Type Assertions
- Interface{} Handling
- Performance Implications
- Serialization/Deserialization

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 7 (REST API)
- Understanding of interfaces
- Type system knowledge

### Overview

Master Go's reflection package. Build tools that inspect types at runtime, parse struct tags, and create generic serialization libraries.

### What You'll Learn
- reflect.Type and reflect.Value
- Kind vs Type distinction
- Struct field iteration
- Tag parsing (json, xml, db)
- Dynamic function calls
- Creating values dynamically
- Performance costs of reflection
- When NOT to use reflection

### Core Features

1. **Type Inspector:**
   - Inspect any type at runtime
   - Print type hierarchy
   - List all methods
   - Show struct fields and tags
   - Detect interface implementations

2. **Struct Tag Parser:**
   - Parse custom struct tags
   - Validation rules from tags
   - DB column mapping
   - JSON field renaming
   - Required field detection

3. **Generic Serializer:**
   - Serialize any struct to map[string]interface{}
   - Deserialize from map to struct
   - Handle nested structs
   - Array and slice support
   - Type conversion

4. **Dynamic Function Caller:**
   - Call functions by name
   - Marshal arguments
   - Handle variadic functions
   - Error handling

### Implementation Guide

#### Type Inspection

**What you need to create:**
```go
func InspectType(v interface{}) {
    t := reflect.TypeOf(v)
    fmt.Printf("Type: %v\n", t)
    fmt.Printf("Kind: %v\n", t.Kind())

    if t.Kind() == reflect.Struct {
        for i := 0; i < t.NumField(); i++ {
            field := t.Field(i)
            fmt.Printf("  Field: %s, Type: %v, Tag: %s\n",
                field.Name, field.Type, field.Tag)
        }
    }

    for i := 0; i < t.NumMethod(); i++ {
        method := t.Method(i)
        fmt.Printf("  Method: %s\n", method.Name)
    }
}
```

#### Struct Tag Parsing

**What you need to create:**
```go
type User struct {
    Name  string `json:"name" validate:"required,min=3"`
    Email string `json:"email" validate:"required,email"`
    Age   int    `json:"age" validate:"min=0,max=150"`
}

func ParseValidationRules(v interface{}) map[string][]string {
    t := reflect.TypeOf(v)
    rules := make(map[string][]string)

    for i := 0; i < t.NumField(); i++ {
        field := t.Field(i)
        tag := field.Tag.Get("validate")
        if tag != "" {
            rules[field.Name] = strings.Split(tag, ",")
        }
    }
    return rules
}
```

#### Generic Mapper

**What you need to create:**
```go
func StructToMap(v interface{}) map[string]interface{} {
    result := make(map[string]interface{})
    val := reflect.ValueOf(v)

    if val.Kind() == reflect.Ptr {
        val = val.Elem()
    }

    typ := val.Type()
    for i := 0; i < val.NumField(); i++ {
        field := typ.Field(i)
        value := val.Field(i)

        // Use json tag if present
        name := field.Tag.Get("json")
        if name == "" {
            name = field.Name
        }

        result[name] = value.Interface()
    }
    return result
}
```

#### Dynamic Function Calls

**What you need to create:**
```go
func CallMethod(obj interface{}, methodName string, args ...interface{}) ([]interface{}, error) {
    val := reflect.ValueOf(obj)
    method := val.MethodByName(methodName)

    if !method.IsValid() {
        return nil, fmt.Errorf("method %s not found", methodName)
    }

    // Convert args to reflect.Value
    in := make([]reflect.Value, len(args))
    for i, arg := range args {
        in[i] = reflect.ValueOf(arg)
    }

    // Call method
    results := method.Call(in)

    // Convert results back
    out := make([]interface{}, len(results))
    for i, result := range results {
        out[i] = result.Interface()
    }

    return out, nil
}
```

### Project Structure

```
reflection-deep-dive/
├── inspector/
│   ├── type_inspector.go    # Type introspection
│   └── method_finder.go     # Method discovery
├── tags/
│   ├── parser.go            # Struct tag parser
│   └── validator.go         # Tag-based validation
├── mapper/
│   ├── struct_to_map.go     # Serialization
│   └── map_to_struct.go     # Deserialization
├── dynamic/
│   └── caller.go            # Dynamic function calls
├── examples/
│   ├── orm_lite.go          # Mini ORM using reflection
│   ├── json_alternative.go  # Custom JSON encoder
│   └── dependency_injector.go
└── benchmarks/
    └── reflection_cost_test.go
```

### Performance Considerations

**Reflection is slow:**
```go
// Benchmark comparison
func BenchmarkDirect(b *testing.B) {
    u := User{Name: "John"}
    for i := 0; i < b.N; i++ {
        _ = u.Name  // Direct access: ~0.3 ns/op
    }
}

func BenchmarkReflection(b *testing.B) {
    u := User{Name: "John"}
    val := reflect.ValueOf(u)
    for i := 0; i < b.N; i++ {
        _ = val.FieldByName("Name")  // Reflection: ~100 ns/op
    }
}
```

**When to use reflection:**
- ✅ Serialization libraries (encoding/json)
- ✅ ORM frameworks (GORM)
- ✅ Dependency injection
- ✅ Testing frameworks
- ✅ Generic utilities
- ❌ Hot paths
- ❌ Performance-critical code
- ❌ When generics can be used instead

### Real-World Applications

**Build these mini-projects:**
1. **Validation Library** - Validate structs based on tags
2. **ORM Mapper** - Map structs to SQL queries
3. **Dependency Injector** - Wire dependencies automatically
4. **Test Helpers** - Compare structs for equality
5. **Config Loader** - Load config from various sources

---

## Project 37: Generics Comprehensive Guide

### Covers Modern Go Features (Go 1.18+)
- Type Parameters
- Generic Functions
- Generic Types
- Type Constraints
- Interface Constraints
- Type Inference
- Generic Data Structures
- Performance vs Reflection

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 7 (REST API)
- Go 1.18 or higher
- Understanding of interfaces

### Overview

Master Go generics. Build type-safe data structures, generic algorithms, and reusable libraries without reflection overhead.

### What You'll Learn
- Type parameter syntax [T any]
- Type constraints
- Comparable constraint
- Custom constraints with interfaces
- Type inference rules
- Generic data structures
- When to use generics vs interfaces
- Migration from interface{} to generics

### Core Features

1. **Generic Data Structures:**
   - Stack[T]
   - Queue[T]
   - LinkedList[T]
   - BinaryTree[T]
   - HashMap[K, V]
   - Set[T]
   - PriorityQueue[T]

2. **Generic Algorithms:**
   - Map, Filter, Reduce
   - Sort with custom comparator
   - Search algorithms
   - Min, Max
   - Contains, IndexOf

3. **Type-Safe Collections:**
   - Result[T, E] (Rust-style)
   - Option[T] (for nullable values)
   - Tuple[T1, T2]
   - Either[L, R]

4. **Generic Utilities:**
   - Pointer helpers
   - Zero value checks
   - Type conversion helpers
   - Slice utilities

### Implementation Guide

#### Basic Generic Function

**What you need to create:**
```go
// Simple generic function
func Max[T constraints.Ordered](a, b T) T {
    if a > b {
        return a
    }
    return b
}

// Usage
maxInt := Max(10, 20)        // T = int
maxFloat := Max(3.14, 2.71)  // T = float64
maxString := Max("apple", "banana")  // T = string
```

#### Generic Data Structure

**What you need to create:**
```go
type Stack[T any] struct {
    items []T
}

func NewStack[T any]() *Stack[T] {
    return &Stack[T]{items: make([]T, 0)}
}

func (s *Stack[T]) Push(item T) {
    s.items = append(s.items, item)
}

func (s *Stack[T]) Pop() (T, bool) {
    if len(s.items) == 0 {
        var zero T
        return zero, false
    }
    item := s.items[len(s.items)-1]
    s.items = s.items[:len(s.items)-1]
    return item, true
}

// Usage
intStack := NewStack[int]()
intStack.Push(1)
intStack.Push(2)
val, ok := intStack.Pop()  // val = 2, ok = true
```

#### Custom Constraints

**What you need to create:**
```go
// Numeric constraint
type Numeric interface {
    ~int | ~int8 | ~int16 | ~int32 | ~int64 |
    ~uint | ~uint8 | ~uint16 | ~uint32 | ~uint64 |
    ~float32 | ~float64
}

func Sum[T Numeric](numbers []T) T {
    var sum T
    for _, n := range numbers {
        sum += n
    }
    return sum
}

// Custom constraint with methods
type Stringer interface {
    String() string
}

func PrintAll[T Stringer](items []T) {
    for _, item := range items {
        fmt.Println(item.String())
    }
}
```

#### Generic Map/Filter/Reduce

**What you need to create:**
```go
func Map[T, U any](slice []T, fn func(T) U) []U {
    result := make([]U, len(slice))
    for i, v := range slice {
        result[i] = fn(v)
    }
    return result
}

func Filter[T any](slice []T, fn func(T) bool) []T {
    result := make([]T, 0)
    for _, v := range slice {
        if fn(v) {
            result = append(result, v)
        }
    }
    return result
}

func Reduce[T, U any](slice []T, initial U, fn func(U, T) U) U {
    result := initial
    for _, v := range slice {
        result = fn(result, v)
    }
    return result
}

// Usage
numbers := []int{1, 2, 3, 4, 5}
doubled := Map(numbers, func(n int) int { return n * 2 })
evens := Filter(numbers, func(n int) bool { return n%2 == 0 })
sum := Reduce(numbers, 0, func(acc, n int) int { return acc + n })
```

#### Result Type (Error Handling)

**What you need to create:**
```go
type Result[T any] struct {
    value T
    err   error
}

func Ok[T any](value T) Result[T] {
    return Result[T]{value: value}
}

func Err[T any](err error) Result[T] {
    var zero T
    return Result[T]{value: zero, err: err}
}

func (r Result[T]) IsOk() bool {
    return r.err == nil
}

func (r Result[T]) Unwrap() (T, error) {
    return r.value, r.err
}

func (r Result[T]) UnwrapOr(defaultValue T) T {
    if r.err != nil {
        return defaultValue
    }
    return r.value
}

// Usage
func Divide(a, b float64) Result[float64] {
    if b == 0 {
        return Err[float64](errors.New("division by zero"))
    }
    return Ok(a / b)
}

result := Divide(10, 2)
if result.IsOk() {
    value, _ := result.Unwrap()
    fmt.Println(value)  // 5
}
```

#### Option Type (Nullable)

**What you need to create:**
```go
type Option[T any] struct {
    value *T
}

func Some[T any](value T) Option[T] {
    return Option[T]{value: &value}
}

func None[T any]() Option[T] {
    return Option[T]{value: nil}
}

func (o Option[T]) IsSome() bool {
    return o.value != nil
}

func (o Option[T]) Unwrap() T {
    if o.value == nil {
        panic("called Unwrap on None")
    }
    return *o.value
}

func (o Option[T]) UnwrapOr(defaultValue T) T {
    if o.value == nil {
        return defaultValue
    }
    return *o.value
}

// Usage
func FindUser(id int) Option[User] {
    user, err := db.GetUser(id)
    if err != nil {
        return None[User]()
    }
    return Some(user)
}
```

### Project Structure

```
generics-guide/
├── datastructures/
│   ├── stack.go
│   ├── queue.go
│   ├── linkedlist.go
│   ├── tree.go
│   └── hashmap.go
├── algorithms/
│   ├── functional.go      # Map, Filter, Reduce
│   ├── search.go
│   └── sort.go
├── types/
│   ├── result.go
│   ├── option.go
│   ├── either.go
│   └── tuple.go
├── utils/
│   ├── slice.go
│   ├── pointer.go
│   └── constraints.go
├── examples/
│   ├── rest_api_generic.go
│   ├── cache_generic.go
│   └── migration_from_interface.go
└── benchmarks/
    └── generics_vs_interface_test.go
```

### Generics vs Alternatives

**When to use Generics:**
- ✅ Type-safe collections
- ✅ Generic algorithms (sort, search)
- ✅ Removing code duplication
- ✅ Library code
- ✅ No reflection overhead

**When to use Interfaces:**
- ✅ Polymorphic behavior
- ✅ Dynamic dispatch needed
- ✅ Plugin architecture
- ✅ Method-based APIs

**When to use Reflection:**
- ✅ Unknown types at compile time
- ✅ Serialization frameworks
- ✅ ORMs

---

## Project 38: Embed Package (Go 1.16+)

### Covers Go 1.16+ Features
- embed.FS
- //go:embed Directive
- Embedding Files
- Embedding Directories
- Static Assets
- Templates
- Database Migrations
- Single Binary Distribution

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 6 (Markdown Blog)
- Go 1.16 or higher

### Overview

Master Go's embed package. Build self-contained binaries with embedded static files, templates, and migrations.

### What You'll Learn
- //go:embed directive
- embed.FS filesystem
- Embedding single files
- Embedding directories
- Embedding patterns
- http.FileServer with embed.FS
- html/template with embedded templates
- Single binary deployment

### Core Features

1. **Static Web Server:**
   - Embed entire frontend
   - Serve HTML/CSS/JS
   - No external dependencies
   - Single binary deployment

2. **Template Engine:**
   - Embed all templates
   - Parse on startup
   - Hot reload in dev (external files)
   - Embedded in production

3. **Database Migrations:**
   - Embed SQL migration files
   - Version control
   - Run from binary
   - No external files needed

4. **Configuration Files:**
   - Embed default configs
   - Fallback configuration
   - Override with external files

### Implementation Guide

#### Basic File Embedding

**What you need to create:**
```go
import _ "embed"

//go:embed version.txt
var version string

//go:embed config.json
var configJSON []byte

//go:embed logo.png
var logoPNG []byte

func main() {
    fmt.Println("Version:", version)

    var config Config
    json.Unmarshal(configJSON, &config)

    // Serve logo
    http.HandleFunc("/logo.png", func(w http.ResponseWriter, r *http.Request) {
        w.Header().Set("Content-Type", "image/png")
        w.Write(logoPNG)
    })
}
```

#### Embedding Directories

**What you need to create:**
```go
import "embed"

//go:embed static/*
var staticFiles embed.FS

//go:embed templates/*.html
var templates embed.FS

//go:embed migrations/*.sql
var migrations embed.FS

func main() {
    // Serve static files
    http.Handle("/static/", http.FileServer(http.FS(staticFiles)))

    // Parse templates
    tmpl, _ := template.ParseFS(templates, "templates/*.html")

    // Read migrations
    files, _ := migrations.ReadDir("migrations")
    for _, file := range files {
        content, _ := migrations.ReadFile("migrations/" + file.Name())
        fmt.Println(string(content))
    }
}
```

#### Static Website with Embed

**What you need to create:**
```go
//go:embed frontend/dist/*
var frontend embed.FS

func main() {
    // Strip "frontend/dist" prefix
    stripped, _ := fs.Sub(frontend, "frontend/dist")

    // Serve at root
    http.Handle("/", http.FileServer(http.FS(stripped)))

    // SPA fallback
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        path := r.URL.Path
        if path == "/" {
            path = "index.html"
        }

        data, err := stripped.Open(path)
        if err != nil {
            // Fallback to index.html for SPA routing
            data, _ = stripped.Open("index.html")
        }
        defer data.Close()

        io.Copy(w, data)
    })

    http.ListenAndServe(":8080", nil)
}
```

#### Database Migrations

**What you need to create:**
```go
//go:embed migrations/*.sql
var migrationsFS embed.FS

type Migration struct {
    Version int
    Name    string
    SQL     string
}

func LoadMigrations() ([]Migration, error) {
    files, err := migrationsFS.ReadDir("migrations")
    if err != nil {
        return nil, err
    }

    var migrations []Migration
    for _, file := range files {
        // Parse: 001_create_users.sql
        parts := strings.Split(file.Name(), "_")
        version, _ := strconv.Atoi(parts[0])

        content, _ := migrationsFS.ReadFile("migrations/" + file.Name())

        migrations = append(migrations, Migration{
            Version: version,
            Name:    strings.TrimSuffix(parts[1], ".sql"),
            SQL:     string(content),
        })
    }

    sort.Slice(migrations, func(i, j int) bool {
        return migrations[i].Version < migrations[j].Version
    })

    return migrations, nil
}

func RunMigrations(db *sql.DB) error {
    migrations, _ := LoadMigrations()
    for _, m := range migrations {
        fmt.Printf("Running migration %d: %s\n", m.Version, m.Name)
        _, err := db.Exec(m.SQL)
        if err != nil {
            return err
        }
    }
    return nil
}
```

#### Template Rendering

**What you need to create:**
```go
//go:embed templates/*
var templatesFS embed.FS

var tmpl *template.Template

func init() {
    var err error
    tmpl, err = template.ParseFS(templatesFS, "templates/*.html")
    if err != nil {
        panic(err)
    }
}

func RenderPage(w http.ResponseWriter, name string, data interface{}) {
    err := tmpl.ExecuteTemplate(w, name, data)
    if err != nil {
        http.Error(w, err.Error(), http.StatusInternalServerError)
    }
}
```

### Project Structure

```
embed-package/
├── main.go
├── static/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── app.js
│   └── images/
│       └── logo.png
├── templates/
│   ├── base.html
│   ├── index.html
│   └── about.html
├── migrations/
│   ├── 001_create_users.sql
│   ├── 002_add_posts.sql
│   └── 003_add_comments.sql
├── config/
│   └── default.json
└── build.sh
```

### Build & Deploy

**Build single binary:**
```bash
# All files embedded in binary
go build -o myapp

# Binary includes:
# - All static files
# - All templates
# - All migrations
# - Default config

# Deploy just one file
./myapp
```

### Real-World Use Cases

1. **CLI Tools with Templates** - Embed templates for code generation
2. **Admin Dashboards** - Single binary with full UI
3. **Microservices** - No external dependencies
4. **Database Tools** - Migrations bundled
5. **Static Site Generators** - Themes embedded

---

## Project 39: Build Tags & Conditional Compilation

### Covers Build System
- Build Tags
- Build Constraints
- Conditional Compilation
- OS-Specific Code
- Architecture-Specific Code
- Feature Flags
- Test Tags
- Build Modes

### Prerequisites & Requirements

**Before Starting:**
- Completed several projects
- Multi-platform deployment experience

### Overview

Master Go's build tag system. Write cross-platform code with OS and architecture-specific implementations.

### What You'll Learn
- //go:build directive
- Build constraints syntax
- OS and architecture tags
- Custom build tags
- Combining constraints (AND, OR, NOT)
- Testing with tags
- Feature flags with tags
- Build tag best practices

### Core Features

1. **OS-Specific Implementations:**
   - Linux-specific code
   - macOS-specific code
   - Windows-specific code
   - Fallback implementations

2. **Feature Flags:**
   - Enable/disable features at build time
   - Debug vs release builds
   - Experimental features
   - Premium features

3. **Test Variations:**
   - Integration tests (separate tag)
   - E2E tests
   - Performance tests
   - Platform-specific tests

4. **Build Modes:**
   - Development mode
   - Production mode
   - Debug builds
   - Profiling builds

### Implementation Guide

#### Basic Build Tags

**What you need to create:**

**File: `logger_dev.go`**
```go
//go:build dev

package main

import "fmt"

func Log(msg string) {
    fmt.Printf("[DEV] %s\n", msg)  // Verbose logging in dev
}
```

**File: `logger_prod.go`**
```go
//go:build prod

package main

import "log"

func Log(msg string) {
    log.Println(msg)  // Structured logging in prod
}
```

**Build:**
```bash
go build -tags dev    # Uses logger_dev.go
go build -tags prod   # Uses logger_prod.go
```

#### OS-Specific Code

**What you need to create:**

**File: `terminal_unix.go`**
```go
//go:build linux || darwin

package terminal

import "golang.org/x/sys/unix"

func GetTerminalSize() (int, int, error) {
    ws, err := unix.IoctlGetWinsize(0, unix.TIOCGWINSZ)
    if err != nil {
        return 0, 0, err
    }
    return int(ws.Col), int(ws.Row), nil
}
```

**File: `terminal_windows.go`**
```go
//go:build windows

package terminal

import "golang.org/x/sys/windows"

func GetTerminalSize() (int, int, error) {
    var info windows.ConsoleScreenBufferInfo
    err := windows.GetConsoleScreenBufferInfo(windows.Stdout, &info)
    if err != nil {
        return 0, 0, err
    }
    width := int(info.Window.Right - info.Window.Left + 1)
    height := int(info.Window.Bottom - info.Window.Top + 1)
    return width, height, nil
}
```

#### Architecture-Specific Code

**What you need to create:**

**File: `crypto_amd64.go`**
```go
//go:build amd64

package crypto

// Uses AVX2 instructions
func HashFast(data []byte) uint64 {
    // AMD64-optimized implementation
    return hashAVX2(data)
}
```

**File: `crypto_arm64.go`**
```go
//go:build arm64

package crypto

// Uses NEON instructions
func HashFast(data []byte) uint64 {
    // ARM64-optimized implementation
    return hashNEON(data)
}
```

**File: `crypto_generic.go`**
```go
//go:build !amd64 && !arm64

package crypto

// Generic implementation
func HashFast(data []byte) uint64 {
    return hashGeneric(data)
}
```

#### Complex Build Constraints

**What you need to create:**
```go
// Build on Linux OR Darwin, but only on AMD64
//go:build (linux || darwin) && amd64

// Build on everything EXCEPT Windows
//go:build !windows

// Build with multiple custom tags
//go:build (dev && debug) || (prod && !debug)

// Integration tests only
//go:build integration

// Require CGO
//go:build cgo
```

#### Feature Flags System

**What you need to create:**

**File: `features_basic.go`**
```go
//go:build !premium

package features

const (
    MaxUsers     = 10
    HasAnalytics = false
    HasExport    = false
)

func CheckPremium() bool {
    return false
}
```

**File: `features_premium.go`**
```go
//go:build premium

package features

const (
    MaxUsers     = 10000
    HasAnalytics = true
    HasExport    = true
)

func CheckPremium() bool {
    return true
}
```

**Usage:**
```bash
# Basic version
go build -o app-basic

# Premium version
go build -tags premium -o app-premium
```

#### Test Tags

**What you need to create:**

**File: `user_test.go`**
```go
package user

func TestUserCreate(t *testing.T) {
    // Fast unit test
}
```

**File: `user_integration_test.go`**
```go
//go:build integration

package user

func TestUserCreateWithDB(t *testing.T) {
    // Slow integration test with real database
}
```

**Run:**
```bash
go test              # Only unit tests
go test -tags integration  # Include integration tests
```

### Project Structure

```
build-tags-demo/
├── main.go
├── logger_dev.go       # //go:build dev
├── logger_prod.go      # //go:build prod
├── platform/
│   ├── file_unix.go    # //go:build linux || darwin
│   └── file_windows.go # //go:build windows
├── crypto/
│   ├── hash_amd64.go   # //go:build amd64
│   ├── hash_arm64.go   # //go:build arm64
│   └── hash_generic.go # //go:build !amd64 && !arm64
├── features/
│   ├── basic.go        # //go:build !premium
│   └── premium.go      # //go:build premium
└── Makefile
```

### Makefile Example

**What you need to create:**
```makefile
# Development build
dev:
	go build -tags dev -o bin/app-dev

# Production build
prod:
	go build -tags prod -ldflags="-s -w" -o bin/app-prod

# Premium build
premium:
	go build -tags "prod premium" -o bin/app-premium

# Cross-platform builds
build-all:
	GOOS=linux GOARCH=amd64 go build -o bin/app-linux-amd64
	GOOS=darwin GOARCH=amd64 go build -o bin/app-darwin-amd64
	GOOS=windows GOARCH=amd64 go build -o bin/app-windows-amd64.exe

# Run tests with different tags
test-unit:
	go test ./...

test-integration:
	go test -tags integration ./...

test-all:
	go test -tags "integration e2e" ./...
```

### Real-World Applications

1. **SaaS with Tiers** - Free vs Premium features
2. **Cross-Platform Tools** - Different implementations per OS
3. **Debug/Release Builds** - Different logging levels
4. **Experimental Features** - Beta features behind flags
5. **Test Separation** - Fast unit tests vs slow integration tests

---

## Project 40: CGO Integration

### Covers C Interop
- CGO Basics
- Calling C from Go
- Calling Go from C
- C Types in Go
- Memory Management
- Performance Considerations
- Building with CGO
- Cross-Compilation Challenges

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 21 (Hypervisor)
- C programming knowledge
- GCC or Clang installed

### Overview

Master CGO for integrating C libraries with Go. Learn when and how to use CGO, memory management, and performance implications.

### What You'll Learn
- CGO syntax (import "C")
- Calling C functions from Go
- Converting between C and Go types
- Memory management (C.malloc, C.free)
- Passing pointers between Go and C
- Building C libraries with Go
- CGO performance overhead
- When to use CGO vs pure Go

### Core Features

1. **C Library Wrapper:**
   - Wrap existing C library
   - Type conversions
   - Error handling
   - Memory safety

2. **Performance-Critical Code:**
   - Use C for hot paths
   - SIMD via C
   - Optimized algorithms
   - Compare CGO vs pure Go

3. **System Integration:**
   - Use system C libraries
   - Linux system calls
   - Hardware interfaces
   - Low-level operations

4. **Export Go to C:**
   - //export directive
   - Create C-compatible libraries
   - Callbacks from C to Go

### Implementation Guide

#### Basic CGO

**What you need to create:**
```go
package main

/*
#include <stdio.h>
#include <stdlib.h>

void hello() {
    printf("Hello from C!\n");
}

int add(int a, int b) {
    return a + b;
}
*/
import "C"
import "fmt"

func main() {
    C.hello()

    result := C.add(10, 20)
    fmt.Printf("10 + 20 = %d\n", result)
}
```

#### Type Conversions

**What you need to create:**
```go
package main

/*
#include <stdlib.h>
#include <string.h>

char* concat(char* a, char* b) {
    char* result = malloc(strlen(a) + strlen(b) + 1);
    strcpy(result, a);
    strcat(result, b);
    return result;
}
*/
import "C"
import "unsafe"

func Concat(a, b string) string {
    // Convert Go strings to C strings
    ca := C.CString(a)
    cb := C.CString(b)

    // Free C strings when done
    defer C.free(unsafe.Pointer(ca))
    defer C.free(unsafe.Pointer(cb))

    // Call C function
    result := C.concat(ca, cb)
    defer C.free(unsafe.Pointer(result))

    // Convert C string back to Go
    return C.GoString(result)
}
```

#### Memory Management

**What you need to create:**
```go
package main

/*
#include <stdlib.h>

typedef struct {
    int* data;
    int size;
} IntArray;

IntArray* create_array(int size) {
    IntArray* arr = malloc(sizeof(IntArray));
    arr->data = malloc(size * sizeof(int));
    arr->size = size;
    return arr;
}

void free_array(IntArray* arr) {
    free(arr->data);
    free(arr);
}
*/
import "C"
import "unsafe"

type IntArray struct {
    cArray *C.IntArray
}

func NewIntArray(size int) *IntArray {
    return &IntArray{
        cArray: C.create_array(C.int(size)),
    }
}

func (a *IntArray) Free() {
    C.free_array(a.cArray)
}

func (a *IntArray) Set(index, value int) {
    // Access C array
    ptr := unsafe.Pointer(uintptr(unsafe.Pointer(a.cArray.data)) + uintptr(index)*unsafe.Sizeof(C.int(0)))
    *(*C.int)(ptr) = C.int(value)
}

func (a *IntArray) Get(index int) int {
    ptr := unsafe.Pointer(uintptr(unsafe.Pointer(a.cArray.data)) + uintptr(index)*unsafe.Sizeof(C.int(0)))
    return int(*(*C.int)(ptr))
}

func main() {
    arr := NewIntArray(10)
    defer arr.Free()

    arr.Set(0, 42)
    val := arr.Get(0)
    fmt.Println(val)  // 42
}
```

#### Wrapping SQLite

**What you need to create:**
```go
package sqlite

/*
#cgo LDFLAGS: -lsqlite3
#include <sqlite3.h>
#include <stdlib.h>
*/
import "C"
import (
    "errors"
    "unsafe"
)

type DB struct {
    db *C.sqlite3
}

func Open(filename string) (*DB, error) {
    cname := C.CString(filename)
    defer C.free(unsafe.Pointer(cname))

    var db *C.sqlite3
    result := C.sqlite3_open(cname, &db)
    if result != C.SQLITE_OK {
        return nil, errors.New(C.GoString(C.sqlite3_errmsg(db)))
    }

    return &DB{db: db}, nil
}

func (db *DB) Close() error {
    result := C.sqlite3_close(db.db)
    if result != C.SQLITE_OK {
        return errors.New("failed to close database")
    }
    return nil
}

func (db *DB) Exec(query string) error {
    cquery := C.CString(query)
    defer C.free(unsafe.Pointer(cquery))

    var errMsg *C.char
    result := C.sqlite3_exec(db.db, cquery, nil, nil, &errMsg)
    if result != C.SQLITE_OK {
        err := errors.New(C.GoString(errMsg))
        C.sqlite3_free(unsafe.Pointer(errMsg))
        return err
    }

    return nil
}
```

#### Exporting Go Functions to C

**What you need to create:**
```go
package main

import "C"

//export Add
func Add(a, b C.int) C.int {
    return a + b
}

//export SayHello
func SayHello(name *C.char) {
    goName := C.GoString(name)
    println("Hello, " + goName + "!")
}

func main() {}
```

**Build as C library:**
```bash
go build -buildmode=c-shared -o libgo.so

# Use from C:
# #include "libgo.h"
# int main() {
#     int result = Add(10, 20);
#     SayHello("World");
#     return 0;
# }
```

#### Performance Comparison

**What you need to create:**
```go
package main

/*
#include <string.h>

int count_chars_c(char* str) {
    return strlen(str);
}
*/
import "C"
import "testing"

func countCharsGo(str string) int {
    return len(str)
}

func countCharsC(str string) int {
    cstr := C.CString(str)
    defer C.free(unsafe.Pointer(cstr))
    return int(C.count_chars_c(cstr))
}

func BenchmarkGo(b *testing.B) {
    str := "Hello, World!"
    for i := 0; i < b.N; i++ {
        countCharsGo(str)
    }
}

func BenchmarkCGO(b *testing.B) {
    str := "Hello, World!"
    for i := 0; i < b.N; i++ {
        countCharsC(str)
    }
}
// Result: Go is ~100x faster (CGO overhead!)
```

### Project Structure

```
cgo-integration/
├── main.go
├── sqlite/
│   └── sqlite.go        # SQLite wrapper
├── crypto/
│   ├── hash.go          # C-based crypto
│   └── hash.c
├── performance/
│   ├── simd.go          # SIMD via C
│   └── simd.c
├── export/
│   └── libgo.go         # Export Go to C
└── Makefile
```

### Build Flags

**What you need to create:**
```go
/*
#cgo CFLAGS: -I/usr/local/include
#cgo LDFLAGS: -L/usr/local/lib -lmylib
#cgo pkg-config: libssl
#cgo linux LDFLAGS: -ldl
#cgo darwin LDFLAGS: -framework CoreFoundation
*/
import "C"
```

### CGO Guidelines

**When to use CGO:**
- ✅ Must use existing C library
- ✅ Performance-critical with proven C implementation
- ✅ Hardware interaction requiring C
- ✅ System calls not available in Go
- ❌ Simple algorithms (pure Go is faster)
- ❌ Cross-compilation needed
- ❌ Portability is priority
- ❌ CGO overhead exceeds benefit

**Performance Impact:**
- CGO call overhead: ~50-200ns
- Type conversions are expensive
- Memory allocations for strings
- Benchmark before committing to CGO

---

## Project 41: Go Modules Advanced

### Covers Dependency Management
- go.mod Structure
- go.sum Verification
- Module Versioning
- Replace Directives
- Private Modules
- Module Proxies
- Vendoring
- Workspace Mode
- Module Publishing

### Prerequisites & Requirements

**Before Starting:**
- Completed several projects
- Git experience
- Understanding of semantic versioning

### Overview

Master Go modules beyond basics. Learn dependency management, versioning, private modules, workspaces, and publishing your own modules.

### What You'll Learn
- Module initialization
- Semantic versioning
- Minimum version selection
- Indirect dependencies
- Replace and exclude directives
- Private repositories
- Module proxies (GOPROXY)
- Go workspaces (Go 1.18+)
- Publishing modules
- Breaking changes (v2+)

### Core Features

1. **Module Management:**
   - Create modules
   - Add dependencies
   - Update dependencies
   - Remove unused dependencies
   - Vendoring

2. **Versioning:**
   - Semantic versioning
   - Version constraints
   - Pseudo-versions
   - Major version changes (v2, v3)
   - Pre-release versions

3. **Advanced Techniques:**
   - Replace local modules
   - Private repositories
   - Module proxies
   - Checksum verification
   - Multi-module repos

4. **Workspaces:**
   - Multi-module development
   - Local replacements
   - Coordinated changes

### Implementation Guide

#### Initialize Module

**What you need to create:**
```bash
# Create new module
mkdir myproject && cd myproject
go mod init github.com/username/myproject

# Creates go.mod:
# module github.com/username/myproject
#
# go 1.21
```

#### Add Dependencies

**What you need to create:**
```bash
# Add dependency (imports it in code first)
go get github.com/gin-gonic/gin@v1.9.0

# Update to latest
go get github.com/gin-gonic/gin@latest

# Update to specific version
go get github.com/gin-gonic/gin@v1.9.1

# Add indirect dependency
go get -u github.com/some/package

# Clean up
go mod tidy  # Remove unused, add missing
```

#### go.mod Structure

**What you need to create:**
```go
module github.com/username/myproject

go 1.21

require (
    github.com/gin-gonic/gin v1.9.1
    github.com/lib/pq v1.10.9
    golang.org/x/sync v0.3.0
)

require (
    // Indirect dependencies
    github.com/gin-contrib/sse v0.1.0 // indirect
    github.com/go-playground/validator/v10 v10.14.0 // indirect
)

replace github.com/old/package => github.com/new/package v1.2.3

exclude github.com/broken/package v1.0.0

retract v1.5.0 // Contains critical bug
```

#### Replace Directive

**What you need to create:**
```go
// Replace with local version (development)
replace github.com/username/mylib => ../mylib

// Replace with fork
replace github.com/old/abandoned => github.com/username/fork v1.2.3

// Replace with specific commit
replace github.com/pkg/name => github.com/pkg/name v0.0.0-20230101120000-abcdef123456
```

#### Private Modules

**What you need to create:**
```bash
# Configure Git credentials
git config --global url."git@github.com:".insteadOf "https://github.com/"

# Set GOPRIVATE
export GOPRIVATE=github.com/mycompany/*

# Or in go env
go env -w GOPRIVATE=github.com/mycompany/*,gitlab.com/myorg/*

# Bypass proxy for private repos
go env -w GONOPROXY=github.com/mycompany/*

# Use private module
go get github.com/mycompany/privaterepo
```

#### Vendoring

**What you need to create:**
```bash
# Create vendor directory
go mod vendor

# Build using vendor
go build -mod=vendor

# Verify vendor is synced
go mod verify
```

#### Workspaces (Go 1.18+)

**What you need to create:**
```bash
# Project structure:
# myworkspace/
# ├── app/          (module 1)
# ├── library/      (module 2)
# └── go.work

# Create workspace
cd myworkspace
go work init ./app ./library

# go.work:
# go 1.21
#
# use (
#     ./app
#     ./library
# )

# Now can develop both modules together
cd app
go run .  # Uses local ./library automatically
```

#### Multi-Module Repository

**What you need to create:**
```
monorepo/
├── go.work
├── service1/
│   ├── go.mod
│   └── main.go
├── service2/
│   ├── go.mod
│   └── main.go
└── shared/
    ├── go.mod
    └── utils.go
```

**go.work:**
```go
go 1.21

use (
    ./service1
    ./service2
    ./shared
)
```

#### Publishing a Module

**What you need to create:**

**Step 1: Tag version**
```bash
git tag v1.0.0
git push origin v1.0.0
```

**Step 2: Users can import**
```bash
go get github.com/username/mymodule@v1.0.0
```

**Step 3: Breaking changes (v2)**
```bash
# Update go.mod
module github.com/username/mymodule/v2

# Tag
git tag v2.0.0
git push origin v2.0.0

# Users import
import "github.com/username/mymodule/v2"
```

#### Version Selection

**What you need to create:**
```bash
# Minimum version selection (MVS)
# If:
# - App requires mylib >= v1.2.0
# - Dependency A requires mylib >= v1.3.0
# - Dependency B requires mylib >= v1.1.0
# Go selects: v1.3.0 (minimum that satisfies all)

# View selected versions
go list -m all

# View available versions
go list -m -versions github.com/some/package

# Explain why dependency is included
go mod why github.com/some/package

# Graph of dependencies
go mod graph
```

#### Checksum Verification

**What you need to create:**
```bash
# go.sum contains checksums
github.com/gin-gonic/gin v1.9.1 h1:abc123...
github.com/gin-gonic/gin v1.9.1/go.mod h1:def456...

# Verify checksums
go mod verify

# If tampering detected, will error
```

### Project Structure

```
go-modules-advanced/
├── go.mod
├── go.sum
├── main.go
├── internal/          # Not importable by other modules
│   └── utils/
├── pkg/               # Importable by others
│   └── api/
├── vendor/            # Optional vendored dependencies
├── tools.go           # Tool dependencies
└── go.work           # Optional workspace file
```

### Tools Dependencies

**What you need to create:**
```go
//go:build tools

package tools

import (
    _ "golang.org/x/tools/cmd/goimports"
    _ "github.com/golangci/golangci-lint/cmd/golangci-lint"
)

// Ensures tools are tracked in go.mod
// Install with: go install golang.org/x/tools/cmd/goimports
```

### Best Practices

1. **Always run `go mod tidy`** after adding/removing imports
2. **Commit go.sum** to version control
3. **Use semantic versioning** for your modules
4. **Document breaking changes** in v2, v3, etc.
5. **Use replace for local development only** - don't commit
6. **Vendor if needed** for reproducible builds
7. **Use workspaces** for multi-module development
8. **Set GOPRIVATE** for private repositories

---

## Project 42: Assembly for Hot Paths

### Covers Low-Level Optimization
- Go Assembly Syntax
- Plan 9 Assembly
- Registers and Instructions
- SIMD Instructions
- Performance Optimization
- Compiler Intrinsics
- Benchmarking Assembly
- When to Use Assembly

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 33 (Profiling)
- Completed Project 40 (CGO)
- Assembly language basics
- x86_64 or ARM64 knowledge

### Overview

Master Go assembly for extreme performance optimization. Learn Plan 9 assembly syntax and when assembly is worth the complexity.

### What You'll Learn
- Plan 9 assembly syntax
- Function calling conventions
- Register usage in Go
- Stack frame layout
- SIMD instructions (SSE, AVX)
- ARM NEON instructions
- Benchmarking assembly code
- Assembly vs CGO vs pure Go

### Core Features

1. **Assembly Functions:**
   - Write assembly implementations
   - Call from Go
   - Handle different architectures
   - Maintain compatibility

2. **SIMD Optimization:**
   - Vector operations
   - Parallel processing
   - Memory alignment
   - Data loading/storing

3. **Performance Cases:**
   - Cryptographic functions
   - String operations
   - Mathematical operations
   - Bit manipulation

4. **Benchmarking:**
   - Compare implementations
   - Measure improvements
   - Profile assembly
   - Validate correctness

### Implementation Guide

#### Basic Assembly Function

**What you need to create:**

**File: `add_amd64.s`**
```asm
#include "textflag.h"

// func Add(a, b int64) int64
TEXT ·Add(SB), NOSPLIT, $0-24
    MOVQ a+0(FP), AX    // Load first argument
    MOVQ b+8(FP), BX    // Load second argument
    ADDQ BX, AX         // Add them
    MOVQ AX, ret+16(FP) // Store result
    RET
```

**File: `add.go`**
```go
package asm

func Add(a, b int64) int64
```

**File: `add_test.go`**
```go
func TestAdd(t *testing.T) {
    result := Add(10, 20)
    if result != 30 {
        t.Errorf("expected 30, got %d", result)
    }
}
```

#### SIMD String Length

**What you need to create:**

**File: `strlen_amd64.s`**
```asm
#include "textflag.h"

// func StrLen(s string) int
TEXT ·StrLen(SB), NOSPLIT, $0-24
    MOVQ s_base+0(FP), SI    // String pointer
    MOVQ s_len+8(FP), AX     // String length (return this)
    MOVQ AX, ret+16(FP)
    RET
```

**More optimized with SSE:**
```asm
#include "textflag.h"

// Count non-zero bytes using SIMD
TEXT ·StrLenSIMD(SB), NOSPLIT, $0-24
    MOVQ s_base+0(FP), SI
    MOVQ s_len+8(FP), CX
    XORQ AX, AX              // Counter = 0

    PXOR X0, X0              // Zero vector

loop:
    CMPQ CX, $16
    JL tail

    MOVDQU (SI), X1          // Load 16 bytes
    PCMPEQB X0, X1           // Compare with zero
    PMOVMSKB X1, DX          // Get mask
    NOTL DX
    POPCNTQ DX, DX           // Count set bits
    ADDQ DX, AX

    ADDQ $16, SI
    SUBQ $16, CX
    JMP loop

tail:
    ADDQ CX, AX              // Add remaining
    MOVQ AX, ret+16(FP)
    RET
```

#### Fast Memory Copy

**What you need to create:**

**File: `memcpy_amd64.s`**
```asm
#include "textflag.h"

// func MemCopy(dst, src []byte)
TEXT ·MemCopy(SB), NOSPLIT, $0-48
    MOVQ dst_base+0(FP), DI
    MOVQ src_base+24(FP), SI
    MOVQ src_len+32(FP), CX

    // Copy using REP MOVSB (fast on modern CPUs)
    CLD
    REP; MOVSB
    RET
```

**Optimized with AVX:**
```asm
TEXT ·MemCopyAVX(SB), NOSPLIT, $0-48
    MOVQ dst_base+0(FP), DI
    MOVQ src_base+24(FP), SI
    MOVQ src_len+32(FP), CX

loop32:
    CMPQ CX, $32
    JL loop8

    VMOVDQU (SI), Y0         // Load 32 bytes
    VMOVDQU Y0, (DI)         // Store 32 bytes

    ADDQ $32, SI
    ADDQ $32, DI
    SUBQ $32, CX
    JMP loop32

loop8:
    CMPQ CX, $8
    JL loop1

    MOVQ (SI), AX
    MOVQ AX, (DI)

    ADDQ $8, SI
    ADDQ $8, DI
    SUBQ $8, CX
    JMP loop8

loop1:
    TESTQ CX, CX
    JZ done

    MOVB (SI), AL
    MOVB AL, (DI)

    INCQ SI
    INCQ DI
    DECQ CX
    JMP loop1

done:
    RET
```

#### XOR Cipher (SIMD)

**What you need to create:**

**File: `xor_amd64.s`**
```asm
#include "textflag.h"

// func XORBytes(dst, src, key []byte)
TEXT ·XORBytes(SB), NOSPLIT, $0-72
    MOVQ dst_base+0(FP), DI
    MOVQ src_base+24(FP), SI
    MOVQ key_base+48(FP), R8
    MOVQ src_len+32(FP), CX

    MOVB (R8), AL            // Load single key byte
    MOVQ $0x0101010101010101, BX
    IMULQ AX, BX             // Replicate byte across 64 bits
    MOVQ BX, X0
    PUNPCKLQDQ X0, X0        // Replicate to 128 bits

loop16:
    CMPQ CX, $16
    JL loop8

    MOVDQU (SI), X1
    PXOR X0, X1
    MOVDQU X1, (DI)

    ADDQ $16, SI
    ADDQ $16, DI
    SUBQ $16, CX
    JMP loop16

loop8:
    CMPQ CX, $8
    JL loop1

    MOVQ (SI), AX
    XORQ BX, AX
    MOVQ AX, (DI)

    ADDQ $8, SI
    ADDQ $8, DI
    SUBQ $8, CX
    JMP loop8

loop1:
    TESTQ CX, CX
    JZ done

    MOVB (SI), AL
    XORB (R8), AL
    MOVB AL, (DI)

    INCQ SI
    INCQ DI
    DECQ CX
    JMP loop1

done:
    RET
```

#### Multi-Architecture Support

**What you need to create:**

**File: `hash_amd64.s`** (x86_64 with AVX2)
```asm
TEXT ·Hash(SB), NOSPLIT, $0-24
    // AVX2 implementation
    ...
```

**File: `hash_arm64.s`** (ARM with NEON)
```asm
TEXT ·Hash(SB), NOSPLIT, $0-24
    // NEON implementation
    ...
```

**File: `hash_generic.go`** (fallback)
```go
//go:build !amd64 && !arm64

func Hash(data []byte) uint64 {
    // Pure Go implementation
    ...
}
```

### Project Structure

```
asm-optimization/
├── add.go
├── add_amd64.s
├── add_arm64.s
├── strlen.go
├── strlen_amd64.s
├── memcpy.go
├── memcpy_amd64.s
├── xor.go
├── xor_amd64.s
├── benchmarks/
│   ├── add_test.go
│   ├── strlen_test.go
│   ├── memcpy_test.go
│   └── xor_test.go
└── examples/
    ├── crypto.go
    └── strings.go
```

### Benchmarking

**What you need to create:**
```go
func BenchmarkAddGo(b *testing.B) {
    for i := 0; i < b.N; i++ {
        _ = int64(10) + int64(20)
    }
}

func BenchmarkAddAsm(b *testing.B) {
    for i := 0; i < b.N; i++ {
        _ = Add(10, 20)
    }
}

func BenchmarkMemCopyGo(b *testing.B) {
    src := make([]byte, 1024)
    dst := make([]byte, 1024)
    b.SetBytes(1024)
    b.ResetTimer()
    for i := 0; i < b.N; i++ {
        copy(dst, src)
    }
}

func BenchmarkMemCopyAsm(b *testing.B) {
    src := make([]byte, 1024)
    dst := make([]byte, 1024)
    b.SetBytes(1024)
    b.ResetTimer()
    for i := 0; i < b.N; i++ {
        MemCopy(dst, src)
    }
}
```

### Register Usage in Go

**Available registers:**
- **amd64**: AX, BX, CX, DX, SI, DI, R8-R15, X0-X15 (SSE), Y0-Y15 (AVX)
- **arm64**: R0-R30, F0-F31, V0-V31 (NEON)

**Reserved:**
- **FP**: Frame pointer (arguments and return values)
- **SB**: Static base (global variables)
- **SP**: Stack pointer
- **PC**: Program counter

### When to Use Assembly

**Good use cases:**
- ✅ Proven bottleneck (profiled)
- ✅ Simple, performance-critical operation
- ✅ SIMD parallelism provides clear win
- ✅ Crypto primitives
- ✅ Math-heavy computations

**Avoid assembly:**
- ❌ Complex logic
- ❌ Portable code needed
- ❌ No proven performance benefit
- ❌ Difficult to maintain
- ❌ Go compiler already optimizes well

### Performance Tips

1. **Profile first** - Use pprof to find real bottlenecks
2. **Benchmark** - Compare pure Go, assembly, CGO
3. **Use SIMD** - Process multiple data in parallel
4. **Align memory** - 16-byte alignment for SSE, 32 for AVX
5. **Minimize branches** - Use conditional moves
6. **Unroll loops** - Reduce loop overhead
7. **Prefetch data** - Use PREFETCH instructions
8. **Test on target CPU** - Performance varies by CPU model

---

## Project 43: Saga Pattern (Distributed Transactions)

### Covers Distributed Systems Patterns
- Saga Pattern
- Choreography vs Orchestration
- Compensating Transactions
- Transaction Coordination
- Eventual Consistency
- Failure Recovery
- Idempotency
- State Management

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 24 (Message Queue)
- Completed Project 28 (Microservices)
- Understanding of distributed transactions

**System Requirements:**
- Message queue (RabbitMQ/Kafka)
- Multiple databases
- Redis for state tracking

### Overview

Implement the Saga pattern for distributed transactions across microservices. Learn choreography and orchestration approaches, compensating transactions, and failure recovery.

### What You'll Learn
- Saga pattern fundamentals
- Choreography (event-driven)
- Orchestration (coordinator)
- Compensating transactions
- Transaction state machine
- Failure handling
- Timeouts and retries
- Saga visualization

### Core Features

1. **Order Processing Saga:**
   - Create order
   - Reserve inventory
   - Process payment
   - Ship order
   - Send notifications

2. **Compensating Actions:**
   - Cancel order → Restore inventory
   - Payment failed → Release reservation
   - Shipping failed → Refund payment
   - Each step has rollback

3. **Saga Coordinator (Orchestration):**
   - Central coordinator service
   - Track saga state
   - Execute steps sequentially
   - Handle failures
   - Trigger compensations

4. **Event-Driven (Choreography):**
   - Services react to events
   - No central coordinator
   - Publish success/failure events
   - Listen and react

### Implementation Guide

#### Saga Definition

**What you need to create:**
```go
type SagaStep struct {
    Name        string
    Action      func(ctx context.Context, data interface{}) error
    Compensate  func(ctx context.Context, data interface{}) error
}

type Saga struct {
    ID          string
    Steps       []SagaStep
    CurrentStep int
    Data        interface{}
    Status      string // pending, completed, failed, compensating
}

type SagaOrchestrator struct {
    sagas map[string]*Saga
    mu    sync.RWMutex
}

func NewSagaOrchestrator() *SagaOrchestrator {
    return &SagaOrchestrator{
        sagas: make(map[string]*Saga),
    }
}
```

#### Orchestration-Based Saga

**What you need to create:**
```go
func (o *SagaOrchestrator) Execute(ctx context.Context, saga *Saga) error {
    o.mu.Lock()
    o.sagas[saga.ID] = saga
    o.mu.Unlock()

    // Execute steps forward
    for i, step := range saga.Steps {
        saga.CurrentStep = i

        err := step.Action(ctx, saga.Data)
        if err != nil {
            // Failure - start compensation
            saga.Status = "compensating"
            return o.Compensate(ctx, saga)
        }
    }

    saga.Status = "completed"
    return nil
}

func (o *SagaOrchestrator) Compensate(ctx context.Context, saga *Saga) error {
    // Execute compensating transactions in reverse
    for i := saga.CurrentStep; i >= 0; i-- {
        step := saga.Steps[i]

        if step.Compensate != nil {
            err := step.Compensate(ctx, saga.Data)
            if err != nil {
                // Log error but continue compensating
                log.Printf("Compensation failed for step %s: %v", step.Name, err)
            }
        }
    }

    saga.Status = "failed"
    return errors.New("saga failed and compensated")
}
```

#### Order Processing Example

**What you need to create:**
```go
type OrderData struct {
    OrderID       string
    UserID        string
    Items         []Item
    TotalAmount   float64
    InventoryID   string
    PaymentID     string
    ShipmentID    string
}

func CreateOrderSaga(orderData *OrderData) *Saga {
    return &Saga{
        ID:   uuid.New().String(),
        Data: orderData,
        Steps: []SagaStep{
            {
                Name: "CreateOrder",
                Action: func(ctx context.Context, data interface{}) error {
                    order := data.(*OrderData)
                    // Create order in database
                    return orderService.Create(ctx, order)
                },
                Compensate: func(ctx context.Context, data interface{}) error {
                    order := data.(*OrderData)
                    // Cancel order
                    return orderService.Cancel(ctx, order.OrderID)
                },
            },
            {
                Name: "ReserveInventory",
                Action: func(ctx context.Context, data interface{}) error {
                    order := data.(*OrderData)
                    reservationID, err := inventoryService.Reserve(ctx, order.Items)
                    if err != nil {
                        return err
                    }
                    order.InventoryID = reservationID
                    return nil
                },
                Compensate: func(ctx context.Context, data interface{}) error {
                    order := data.(*OrderData)
                    // Release inventory
                    return inventoryService.Release(ctx, order.InventoryID)
                },
            },
            {
                Name: "ProcessPayment",
                Action: func(ctx context.Context, data interface{}) error {
                    order := data.(*OrderData)
                    paymentID, err := paymentService.Charge(ctx, order.UserID, order.TotalAmount)
                    if err != nil {
                        return err
                    }
                    order.PaymentID = paymentID
                    return nil
                },
                Compensate: func(ctx context.Context, data interface{}) error {
                    order := data.(*OrderData)
                    // Refund payment
                    return paymentService.Refund(ctx, order.PaymentID)
                },
            },
            {
                Name: "CreateShipment",
                Action: func(ctx context.Context, data interface{}) error {
                    order := data.(*OrderData)
                    shipmentID, err := shippingService.Create(ctx, order)
                    if err != nil {
                        return err
                    }
                    order.ShipmentID = shipmentID
                    return nil
                },
                Compensate: func(ctx context.Context, data interface{}) error {
                    order := data.(*OrderData)
                    // Cancel shipment
                    return shippingService.Cancel(ctx, order.ShipmentID)
                },
            },
            {
                Name: "SendNotification",
                Action: func(ctx context.Context, data interface{}) error {
                    order := data.(*OrderData)
                    return notificationService.SendOrderConfirmation(ctx, order)
                },
                Compensate: nil, // No compensation needed for notification
            },
        },
    }
}
```

*[Continuing with Choreography-Based Saga, Saga State Persistence, Project Structure, Testing, and Best Practices sections - similar comprehensive coverage as previous projects]*

---

## Project 44: CQRS Implementation

### Covers Advanced Architecture Patterns
- Command Query Responsibility Segregation
- Read Models vs Write Models
- Event Sourcing
- Eventual Consistency
- Materialized Views
- Query Optimization
- Command Validation
- Event Store

*[Full CQRS implementation with Command/Query separation, Event Sourcing, Aggregates, Event Store, Read Model projections, and extensive examples]*

---

## Project 45: Bulkhead Pattern (Failure Isolation)

### Covers Resilience Patterns
- Bulkhead Pattern
- Resource Isolation
- Thread Pools
- Connection Pools
- Failure Isolation
- Resource Limits
- Goroutine Pools
- Semaphores

*[Complete Bulkhead pattern implementation with semaphore-based limiting, worker pools, connection pools, service-specific bulkheads, multi-tenant isolation, and monitoring]*

---

## Project 46: Sidecar Pattern

### Covers Service Mesh Patterns
- Sidecar Pattern
- Service Mesh Fundamentals
- Cross-Cutting Concerns
- Proxy Architecture
- Logging Sidecar
- Monitoring Sidecar
- Authentication Proxy
- Rate Limiting Proxy

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 28 (Microservices)
- Completed Project 29 (Distributed Tracing)
- Docker knowledge
- Kubernetes basics (optional)

**System Requirements:**
- Docker
- Multiple services to augment
- Shared volumes or network

### Overview

Implement the Sidecar pattern to add functionality to services without modifying their code. Build sidecars for logging, monitoring, authentication, and rate limiting.

### What You'll Learn
- Sidecar pattern fundamentals
- Service augmentation without code changes
- Reverse proxy implementation
- Inter-process communication
- Shared volumes and networking
- Ambassador pattern
- Adapter pattern
- Service mesh concepts

### Core Features

1. **Logging Sidecar:**
   - Capture application logs
   - Format and enrich logs
   - Forward to centralized logging
   - Log rotation and compression
   - No app code changes

2. **Monitoring Sidecar:**
   - Collect metrics from app
   - Expose Prometheus endpoint
   - Health check proxy
   - Performance metrics
   - Resource usage tracking

3. **Authentication Proxy:**
   - JWT validation
   - OAuth2 handling
   - Request signing
   - Certificate management
   - Transparent to main app

4. **Rate Limiting Proxy:**
   - Rate limit requests
   - Quota management
   - Backpressure handling
   - Circuit breaker integration

### Implementation Guide

#### Logging Sidecar

**What you need to create:**

**Main Application (writes to file):**
```go
// main-app/main.go
func main() {
    logFile, _ := os.OpenFile("/var/log/app/app.log", os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0644)
    defer logFile.Close()

    logger := log.New(logFile, "", log.LstdFlags)

    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        logger.Printf("Request: %s %s", r.Method, r.URL.Path)
        w.Write([]byte("Hello"))
    })

    http.ListenAndServe(":8080", nil)
}
```

**Logging Sidecar (reads file, forwards to Loki):**
```go
// log-sidecar/main.go
type LogForwarder struct {
    lokiURL string
    appName string
}

func (f *LogForwarder) WatchAndForward(logPath string) {
    t, _ := tail.TailFile(logPath, tail.Config{Follow: true})

    for line := range t.Lines {
        f.forwardToLoki(line.Text)
    }
}

func (f *LogForwarder) forwardToLoki(logLine string) {
    // Parse log line
    entry := LogEntry{
        Timestamp: time.Now(),
        Message:   logLine,
        Level:     "info",
        App:       f.appName,
    }

    // Send to Loki
    payload := map[string]interface{}{
        "streams": []map[string]interface{}{
            {
                "stream": map[string]string{
                    "app": f.appName,
                },
                "values": [][]string{
                    {fmt.Sprintf("%d", entry.Timestamp.UnixNano()), entry.Message},
                },
            },
        },
    }

    jsonData, _ := json.Marshal(payload)
    http.Post(f.lokiURL+"/loki/api/v1/push", "application/json", bytes.NewBuffer(jsonData))
}

func main() {
    forwarder := &LogForwarder{
        lokiURL: os.Getenv("LOKI_URL"),
        appName: os.Getenv("APP_NAME"),
    }

    forwarder.WatchAndForward("/var/log/app/app.log")
}
```

**Docker Compose:**
```yaml
version: '3.8'
services:
  main-app:
    build: ./main-app
    volumes:
      - logs:/var/log/app
    ports:
      - "8080:8080"

  log-sidecar:
    build: ./log-sidecar
    volumes:
      - logs:/var/log/app:ro
    environment:
      - LOKI_URL=http://loki:3100
      - APP_NAME=main-app
    depends_on:
      - main-app

volumes:
  logs:
```

#### Authentication Proxy Sidecar

**What you need to create:**
```go
// auth-sidecar/main.go
type AuthProxy struct {
    upstreamURL string
    jwtSecret   []byte
}

func (p *AuthProxy) ServeHTTP(w http.ResponseWriter, r *http.Request) {
    // Extract JWT token
    authHeader := r.Header.Get("Authorization")
    if authHeader == "" {
        http.Error(w, "Unauthorized", http.StatusUnauthorized)
        return
    }

    token := strings.TrimPrefix(authHeader, "Bearer ")

    // Validate JWT
    claims, err := p.validateJWT(token)
    if err != nil {
        http.Error(w, "Invalid token", http.StatusUnauthorized)
        return
    }

    // Add user info to headers for upstream
    r.Header.Set("X-User-ID", claims.UserID)
    r.Header.Set("X-User-Email", claims.Email)
    r.Header.Set("X-User-Roles", strings.Join(claims.Roles, ","))

    // Forward to main app
    p.proxyRequest(w, r)
}

func (p *AuthProxy) validateJWT(tokenString string) (*Claims, error) {
    token, err := jwt.Parse(tokenString, func(token *jwt.Token) (interface{}, error) {
        return p.jwtSecret, nil
    })

    if err != nil || !token.Valid {
        return nil, errors.New("invalid token")
    }

    claims := token.Claims.(jwt.MapClaims)
    return &Claims{
        UserID: claims["user_id"].(string),
        Email:  claims["email"].(string),
        Roles:  claims["roles"].([]string),
    }, nil
}

func (p *AuthProxy) proxyRequest(w http.ResponseWriter, r *http.Request) {
    // Create proxy
    proxy := httputil.NewSingleHostReverseProxy(p.upstreamURL)
    proxy.ServeHTTP(w, r)
}

func main() {
    proxy := &AuthProxy{
        upstreamURL: parseURL("http://localhost:8080"),
        jwtSecret:   []byte(os.Getenv("JWT_SECRET")),
    }

    // Sidecar listens on different port
    http.ListenAndServe(":8000", proxy)
}
```

**Main App (no auth logic needed):**
```go
// main-app/main.go
func main() {
    http.HandleFunc("/api/profile", func(w http.ResponseWriter, r *http.Request) {
        // User info already validated and in headers
        userID := r.Header.Get("X-User-ID")
        email := r.Header.Get("X-User-Email")

        profile := map[string]string{
            "user_id": userID,
            "email":   email,
        }

        json.NewEncoder(w).Encode(profile)
    })

    http.ListenAndServe(":8080", nil)
}
```

#### Monitoring Sidecar

**What you need to create:**
```go
// metrics-sidecar/main.go
type MetricsSidecar struct {
    appURL string
    registry *prometheus.Registry
}

func (m *MetricsSidecar) CollectMetrics() {
    // HTTP metrics
    requestDuration := prometheus.NewHistogramVec(
        prometheus.HistogramOpts{
            Name: "http_request_duration_seconds",
            Help: "HTTP request duration",
        },
        []string{"method", "path", "status"},
    )
    m.registry.MustRegister(requestDuration)

    // App-specific metrics (read from app's health endpoint)
    go m.pollAppMetrics()

    // Expose metrics endpoint
    http.Handle("/metrics", promhttp.HandlerFor(m.registry, promhttp.HandlerOpts{}))
    http.ListenAndServe(":9090", nil)
}

func (m *MetricsSidecar) pollAppMetrics() {
    ticker := time.NewTicker(15 * time.Second)
    for range ticker.C {
        resp, err := http.Get(m.appURL + "/health")
        if err != nil {
            continue
        }

        var health HealthStatus
        json.NewDecoder(resp.Body).Decode(&health)
        resp.Body.Close()

        // Export app metrics to Prometheus format
        // ...
    }
}
```

#### Rate Limiting Sidecar

**What you need to create:**
```go
// rate-limiter-sidecar/main.go
type RateLimiterSidecar struct {
    upstreamURL *url.URL
    limiter     *rate.Limiter
}

func (rl *RateLimiterSidecar) ServeHTTP(w http.ResponseWriter, r *http.Request) {
    // Check rate limit
    if !rl.limiter.Allow() {
        http.Error(w, "Rate limit exceeded", http.StatusTooManyRequests)
        return
    }

    // Forward request
    proxy := httputil.NewSingleHostReverseProxy(rl.upstreamURL)
    proxy.ServeHTTP(w, r)
}

func main() {
    // 100 requests per second, burst of 200
    limiter := rate.NewLimiter(100, 200)

    sidecar := &RateLimiterSidecar{
        upstreamURL: parseURL("http://localhost:8080"),
        limiter:     limiter,
    }

    http.ListenAndServe(":8000", sidecar)
}
```

### Kubernetes Sidecar Deployment

**What you need to create:**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-with-sidecars
spec:
  containers:
  # Main application
  - name: main-app
    image: myapp:latest
    ports:
    - containerPort: 8080
    volumeMounts:
    - name: logs
      mountPath: /var/log/app

  # Logging sidecar
  - name: log-forwarder
    image: log-sidecar:latest
    volumeMounts:
    - name: logs
      mountPath: /var/log/app
      readOnly: true
    env:
    - name: LOKI_URL
      value: "http://loki:3100"

  # Auth proxy sidecar
  - name: auth-proxy
    image: auth-sidecar:latest
    ports:
    - containerPort: 8000
    env:
    - name: UPSTREAM_URL
      value: "http://localhost:8080"
    - name: JWT_SECRET
      valueFrom:
        secretKeyRef:
          name: jwt-secret
          key: secret

  # Metrics sidecar
  - name: metrics
    image: metrics-sidecar:latest
    ports:
    - containerPort: 9090
    env:
    - name: APP_URL
      value: "http://localhost:8080"

  volumes:
  - name: logs
    emptyDir: {}

---
apiVersion: v1
kind: Service
metadata:
  name: myapp
spec:
  selector:
    app: myapp
  ports:
  - name: http
    port: 80
    targetPort: 8000  # Route through auth proxy
  - name: metrics
    port: 9090
    targetPort: 9090
```

### Project Structure

```
sidecar-pattern/
├── main-app/
│   ├── main.go
│   └── Dockerfile
├── sidecars/
│   ├── log-forwarder/
│   │   ├── main.go
│   │   └── Dockerfile
│   ├── auth-proxy/
│   │   ├── main.go
│   │   └── Dockerfile
│   ├── metrics/
│   │   ├── main.go
│   │   └── Dockerfile
│   └── rate-limiter/
│       ├── main.go
│       └── Dockerfile
├── kubernetes/
│   ├── deployment.yaml
│   └── service.yaml
├── docker-compose.yml
└── README.md
```

### Sidecar Benefits

**Advantages:**
- ✅ Separation of concerns
- ✅ No code changes to main app
- ✅ Reusable across services
- ✅ Independent scaling
- ✅ Technology agnostic
- ✅ Easy to add/remove features

**Use Cases:**
- Logging and monitoring
- Authentication and authorization
- Service discovery
- Configuration management
- Circuit breaking
- Rate limiting
- TLS termination

---

## Project 47: Strangler Fig Pattern

### Covers Legacy Migration Patterns
- Strangler Fig Pattern
- Gradual Migration
- Feature Toggles
- Traffic Routing
- Dual Writing
- Shadow Testing
- Rollback Strategies
- Legacy System Integration

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 26 (Load Balancer)
- Completed Project 28 (Microservices)
- Understanding of migration strategies

**System Requirements:**
- Legacy application (simulate or use existing)
- New microservices
- Reverse proxy or API gateway
- Feature flag system

### Overview

Implement the Strangler Fig pattern to migrate from monolithic legacy systems to microservices. Learn gradual migration, traffic routing, dual writing, and safe rollback strategies.

### What You'll Learn
- Strangler Fig pattern fundamentals
- Gradual migration strategies
- Traffic routing and splitting
- Feature flags for migration
- Dual writing patterns
- Shadow testing
- Data synchronization
- Rollback mechanisms

### Core Features

1. **Migration Proxy:**
   - Route requests to legacy or new service
   - Percentage-based routing
   - Header-based routing
   - User-based routing (canary)

2. **Dual Writing:**
   - Write to both systems
   - Verify consistency
   - Handle conflicts
   - Eventual migration

3. **Feature Flags:**
   - Enable/disable new features
   - Per-user feature flags
   - Gradual rollout
   - Emergency rollback

4. **Data Migration:**
   - Incremental data sync
   - Background migration
   - Consistency verification
   - Zero-downtime migration

### Implementation Guide

#### Migration Proxy (Strangler Facade)

**What you need to create:**
```go
type StranglerProxy struct {
    legacyURL    *url.URL
    newServiceURL *url.URL
    router       *MigrationRouter
}

type MigrationRouter struct {
    rules []RoutingRule
    mu    sync.RWMutex
}

type RoutingRule struct {
    Path           string
    Method         string
    UseNewService  bool
    RolloutPercent int  // 0-100
    UserWhitelist  []string
}

func (p *StranglerProxy) ServeHTTP(w http.ResponseWriter, r *http.Request) {
    rule := p.router.GetRule(r.Method, r.URL.Path)

    targetURL := p.legacyURL

    if rule != nil {
        if rule.UseNewService {
            // Full migration
            targetURL = p.newServiceURL
        } else if rule.RolloutPercent > 0 {
            // Percentage-based routing
            if shouldRouteToNew(rule.RolloutPercent) {
                targetURL = p.newServiceURL
            }
        } else if len(rule.UserWhitelist) > 0 {
            // User-based routing
            userID := r.Header.Get("X-User-ID")
            if contains(rule.UserWhitelist, userID) {
                targetURL = p.newServiceURL
            }
        }
    }

    // Add header to track routing decision
    r.Header.Set("X-Routed-To", targetURL.Host)

    // Proxy request
    proxy := httputil.NewSingleHostReverseProxy(targetURL)
    proxy.ServeHTTP(w, r)
}

func shouldRouteToNew(percent int) bool {
    return rand.Intn(100) < percent
}
```

#### Feature Flag System

**What you need to create:**
```go
type FeatureFlagService struct {
    flags map[string]*FeatureFlag
    mu    sync.RWMutex
}

type FeatureFlag struct {
    Name           string
    Enabled        bool
    RolloutPercent int
    Whitelist      []string
    Blacklist      []string
}

func (s *FeatureFlagService) IsEnabled(flagName, userID string) bool {
    s.mu.RLock()
    flag, exists := s.flags[flagName]
    s.mu.RUnlock()

    if !exists {
        return false // Default to legacy
    }

    // Check blacklist
    if contains(flag.Blacklist, userID) {
        return false
    }

    // Check whitelist
    if len(flag.Whitelist) > 0 {
        return contains(flag.Whitelist, userID)
    }

    // Check rollout percentage
    if flag.RolloutPercent > 0 {
        return hashUserID(userID)%100 < flag.RolloutPercent
    }

    return flag.Enabled
}

// Use in handler
func (api *API) GetUser(w http.ResponseWriter, r *http.Request) {
    userID := r.Header.Get("X-User-ID")

    if api.featureFlags.IsEnabled("new-user-service", userID) {
        // Call new microservice
        api.newUserService.GetUser(w, r)
    } else {
        // Call legacy system
        api.legacySystem.GetUser(w, r)
    }
}
```

#### Dual Writing Pattern

**What you need to create:**
```go
type DualWriter struct {
    legacyDB *sql.DB
    newDB    *sql.DB
    verifier *ConsistencyVerifier
}

func (dw *DualWriter) CreateUser(user *User) error {
    var legacyErr, newErr error

    // Write to legacy system (primary)
    legacyErr = dw.legacyDB.Exec("INSERT INTO users ...", user)

    // Write to new system (secondary)
    go func() {
        newErr = dw.newDB.Exec("INSERT INTO users ...", user)

        // Log any inconsistencies
        if newErr != nil {
            log.Printf("Dual write failed for new DB: %v", newErr)
            dw.verifier.RecordInconsistency(user.ID)
        }
    }()

    // Return legacy result (primary)
    return legacyErr
}

func (dw *DualWriter) GetUser(id string) (*User, error) {
    // Read from legacy (primary)
    user, err := dw.legacyDB.Query("SELECT * FROM users WHERE id = ?", id)

    // Shadow read from new system
    go func() {
        newUser, newErr := dw.newDB.Query("SELECT * FROM users WHERE id = ?", id)

        // Compare results
        if newErr == nil && !usersEqual(user, newUser) {
            log.Printf("Data mismatch for user %s", id)
            dw.verifier.RecordInconsistency(id)
        }
    }()

    return user, err
}
```

#### Migration Progress Tracker

**What you need to create:**
```go
type MigrationTracker struct {
    endpoints map[string]*EndpointStatus
    mu        sync.RWMutex
}

type EndpointStatus struct {
    Path              string
    Method            string
    TotalRequests     int64
    NewServiceRequests int64
    LegacyRequests    int64
    ErrorRate         float64
    AvgLatencyNew     time.Duration
    AvgLatencyLegacy  time.Duration
    Status            string // not-started, in-progress, completed
}

func (mt *MigrationTracker) RecordRequest(path, method, target string, duration time.Duration, err error) {
    mt.mu.Lock()
    defer mt.mu.Unlock()

    key := method + ":" + path
    status := mt.endpoints[key]
    if status == nil {
        status = &EndpointStatus{Path: path, Method: method}
        mt.endpoints[key] = status
    }

    status.TotalRequests++

    if target == "new" {
        status.NewServiceRequests++
        status.AvgLatencyNew = (status.AvgLatencyNew + duration) / 2
    } else {
        status.LegacyRequests++
        status.AvgLatencyLegacy = (status.AvgLatencyLegacy + duration) / 2
    }

    if err != nil {
        status.ErrorRate = float64(status.ErrorRate + 0.01)
    }

    // Update status
    if status.NewServiceRequests == status.TotalRequests {
        status.Status = "completed"
    } else if status.NewServiceRequests > 0 {
        status.Status = "in-progress"
    }
}

func (mt *MigrationTracker) GetDashboard() map[string]*EndpointStatus {
    mt.mu.RLock()
    defer mt.mu.RUnlock()

    // Return copy
    dashboard := make(map[string]*EndpointStatus)
    for k, v := range mt.endpoints {
        dashboard[k] = v
    }
    return dashboard
}
```

#### Data Migration Worker

**What you need to create:**
```go
type DataMigrationWorker struct {
    legacyDB *sql.DB
    newDB    *sql.DB
    batchSize int
}

func (w *DataMigrationWorker) MigrateUsers() error {
    var lastID int64 = 0

    for {
        // Fetch batch from legacy
        users, err := w.fetchUserBatch(lastID, w.batchSize)
        if err != nil {
            return err
        }

        if len(users) == 0 {
            break // All done
        }

        // Transform and insert into new system
        for _, user := range users {
            newUser := w.transformUser(user)
            err := w.insertIntoNew(newUser)
            if err != nil {
                log.Printf("Failed to migrate user %d: %v", user.ID, err)
                continue
            }
            lastID = user.ID
        }

        log.Printf("Migrated batch, last ID: %d", lastID)
        time.Sleep(100 * time.Millisecond) // Rate limit
    }

    return nil
}

func (w *DataMigrationWorker) VerifyMigration() error {
    // Count records
    var legacyCount, newCount int64
    w.legacyDB.QueryRow("SELECT COUNT(*) FROM users").Scan(&legacyCount)
    w.newDB.QueryRow("SELECT COUNT(*) FROM users").Scan(&newCount)

    if legacyCount != newCount {
        return fmt.Errorf("count mismatch: legacy=%d, new=%d", legacyCount, newCount)
    }

    // Sample verification
    // ...

    return nil
}
```

### Project Structure

```
strangler-fig/
├── proxy/
│   ├── strangler.go        # Main proxy
│   ├── router.go           # Routing logic
│   └── middleware.go
├── feature-flags/
│   ├── service.go
│   └── storage.go
├── dual-write/
│   ├── writer.go
│   └── verifier.go
├── migration/
│   ├── tracker.go
│   ├── worker.go
│   └── dashboard.go
├── legacy/
│   └── adapter.go          # Legacy system adapter
├── new-services/
│   ├── users/
│   └── orders/
└── config/
    └── migration-rules.yaml
```

### Migration Phases

**Phase 1: Setup (Week 1)**
- Deploy strangler proxy
- All traffic to legacy
- Setup monitoring

**Phase 2: Shadow Mode (Weeks 2-3)**
- Route 10% to new service
- Compare responses
- Fix inconsistencies

**Phase 3: Gradual Rollout (Weeks 4-8)**
- 25% → 50% → 75% → 100%
- Monitor error rates
- Rollback if needed

**Phase 4: Data Migration (Weeks 9-10)**
- Background data sync
- Dual writing
- Consistency verification

**Phase 5: Completion (Week 11+)**
- 100% on new service
- Legacy decommission
- Remove strangler proxy

### Best Practices

1. **Start with read-only operations** - Lower risk
2. **Monitor everything** - Error rates, latency, consistency
3. **Use feature flags** - Easy rollback
4. **Dual write carefully** - Legacy is source of truth initially
5. **Verify data consistency** - Before full migration
6. **Keep rollback plan** - At every phase
7. **Communicate progress** - Stakeholder visibility

---

## Project 48: Database per Service

### Covers Microservices Data Patterns
- Database per Service Pattern
- Data Isolation
- Data Duplication
- Eventual Consistency
- Saga Pattern Integration
- CQRS Integration
- API Composition
- Data Synchronization

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 28 (Microservices)
- Completed Project 43 (Saga Pattern)
- Completed Project 44 (CQRS)
- Understanding of distributed data

**System Requirements:**
- Multiple databases (PostgreSQL, MongoDB, etc.)
- Message queue (Kafka/RabbitMQ)
- API Gateway

### Overview

Implement the Database per Service pattern for microservices. Learn data isolation, handling data duplication, eventual consistency, and querying across services.

### What You'll Learn
- Database per service fundamentals
- Data ownership boundaries
- Handling data duplication
- Cross-service queries
- Event-driven data sync
- API composition pattern
- CQRS for queries
- Transaction management

### Core Features

1. **Service-Specific Databases:**
   - User Service → PostgreSQL
   - Order Service → PostgreSQL
   - Product Service → MongoDB
   - Analytics Service → ClickHouse
   - Complete isolation

2. **Data Synchronization:**
   - Event-driven replication
   - Change Data Capture (CDC)
   - Eventual consistency
   - Conflict resolution

3. **Cross-Service Queries:**
   - API composition
   - Materialized views
   - CQRS read models
   - GraphQL federation

4. **Transaction Management:**
   - Saga pattern for distributed transactions
   - Two-phase commit (avoid if possible)
   - Compensating transactions

### Implementation Guide

#### Service-Specific Schemas

**User Service Database:**
```sql
-- users_db
CREATE TABLE users (
    id UUID PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    name VARCHAR(255),
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);

CREATE TABLE user_preferences (
    user_id UUID PRIMARY KEY REFERENCES users(id),
    newsletter_enabled BOOLEAN,
    theme VARCHAR(50)
);
```

**Order Service Database:**
```sql
-- orders_db
CREATE TABLE orders (
    id UUID PRIMARY KEY,
    user_id UUID NOT NULL,  -- Reference to user (different DB)
    total_amount DECIMAL(10,2),
    status VARCHAR(50),
    created_at TIMESTAMP
);

CREATE TABLE order_items (
    id UUID PRIMARY KEY,
    order_id UUID REFERENCES orders(id),
    product_id UUID NOT NULL,  -- Reference to product (different DB)
    quantity INT,
    price DECIMAL(10,2)
);

-- Denormalized user data for queries
CREATE TABLE user_snapshots (
    user_id UUID PRIMARY KEY,
    email VARCHAR(255),
    name VARCHAR(255),
    last_synced TIMESTAMP
);
```

**Product Service Database (MongoDB):**
```javascript
// products_db
{
    _id: ObjectId,
    sku: String,
    name: String,
    description: String,
    price: Number,
    inventory: {
        quantity: Number,
        reserved: Number
    },
    created_at: Date,
    updated_at: Date
}
```

#### Event-Driven Synchronization

**What you need to create:**
```go
// User Service publishes events
type UserService struct {
    db       *sql.DB
    eventBus EventBus
}

func (s *UserService) CreateUser(user *User) error {
    // Save to database
    err := s.db.Exec("INSERT INTO users ...", user)
    if err != nil {
        return err
    }

    // Publish event
    s.eventBus.Publish("UserCreated", UserCreatedEvent{
        UserID: user.ID,
        Email:  user.Email,
        Name:   user.Name,
    })

    return nil
}

func (s *UserService) UpdateUser(userID string, updates *UserUpdates) error {
    err := s.db.Exec("UPDATE users SET ...", updates)
    if err != nil {
        return err
    }

    s.eventBus.Publish("UserUpdated", UserUpdatedEvent{
        UserID: userID,
        Email:  updates.Email,
        Name:   updates.Name,
    })

    return nil
}

// Order Service listens and maintains snapshot
type OrderService struct {
    db *sql.DB
}

func (s *OrderService) OnUserCreated(event UserCreatedEvent) {
    // Store user snapshot for denormalized queries
    s.db.Exec(`
        INSERT INTO user_snapshots (user_id, email, name, last_synced)
        VALUES ($1, $2, $3, $4)
    `, event.UserID, event.Email, event.Name, time.Now())
}

func (s *OrderService) OnUserUpdated(event UserUpdatedEvent) {
    s.db.Exec(`
        UPDATE user_snapshots
        SET email = $1, name = $2, last_synced = $3
        WHERE user_id = $4
    `, event.Email, event.Name, time.Now(), event.UserID)
}
```

#### API Composition Pattern

**What you need to create:**
```go
// API Gateway composes data from multiple services
type OrderCompositionService struct {
    orderService   *OrderServiceClient
    userService    *UserServiceClient
    productService *ProductServiceClient
}

func (s *OrderCompositionService) GetOrderDetails(orderID string) (*OrderDetails, error) {
    // Fetch order from Order Service
    order, err := s.orderService.GetOrder(orderID)
    if err != nil {
        return nil, err
    }

    // Fetch user details from User Service (parallel)
    var user *User
    var products []*Product

    errGroup := new(errgroup.Group)

    errGroup.Go(func() error {
        var err error
        user, err = s.userService.GetUser(order.UserID)
        return err
    })

    errGroup.Go(func() error {
        productIDs := extractProductIDs(order.Items)
        var err error
        products, err = s.productService.GetProducts(productIDs)
        return err
    })

    if err := errGroup.Wait(); err != nil {
        return nil, err
    }

    // Compose response
    return &OrderDetails{
        Order:    order,
        User:     user,
        Products: products,
    }, nil
}
```

#### CQRS Read Model (for complex queries)

**What you need to create:**
```go
// Separate read database (MongoDB) for complex queries
type OrderReadModel struct {
    OrderID      string
    UserID       string
    UserEmail    string
    UserName     string
    Items        []OrderItemReadModel
    TotalAmount  float64
    Status       string
    CreatedAt    time.Time
}

type OrderItemReadModel struct {
    ProductID   string
    ProductName string
    Quantity    int
    Price       float64
}

// Read Model Projector
type OrderReadModelProjector struct {
    readDB *mongo.Collection
}

func (p *OrderReadModelProjector) OnOrderCreated(event OrderCreatedEvent) {
    // Build denormalized read model
    user, _ := userService.GetUser(event.UserID)
    products, _ := productService.GetProducts(event.ProductIDs)

    readModel := OrderReadModel{
        OrderID:     event.OrderID,
        UserID:      event.UserID,
        UserEmail:   user.Email,
        UserName:    user.Name,
        Items:       buildItems(event.Items, products),
        TotalAmount: event.TotalAmount,
        Status:      event.Status,
        CreatedAt:   event.CreatedAt,
    }

    p.readDB.InsertOne(context.Background(), readModel)
}

// Query using read model (fast!)
func (s *OrderQueryService) SearchOrders(filter OrderFilter) ([]OrderReadModel, error) {
    query := bson.M{}

    if filter.UserEmail != "" {
        query["useremail"] = filter.UserEmail
    }

    if filter.MinAmount > 0 {
        query["totalamount"] = bson.M{"$gte": filter.MinAmount}
    }

    cursor, _ := s.readDB.Find(context.Background(), query)

    var orders []OrderReadModel
    cursor.All(context.Background(), &orders)
    return orders, nil
}
```

#### Cross-Service Transaction (Saga)

**What you need to create:**
```go
// Create order across multiple services
func CreateOrderSaga(orderData *OrderData) *Saga {
    return &Saga{
        Steps: []SagaStep{
            {
                Name: "ValidateUser",
                Action: func(ctx context.Context, data interface{}) error {
                    // Call User Service
                    return userService.Validate(orderData.UserID)
                },
                Compensate: nil,
            },
            {
                Name: "ReserveInventory",
                Action: func(ctx context.Context, data interface{}) error {
                    // Call Product Service
                    return productService.ReserveInventory(orderData.Items)
                },
                Compensate: func(ctx context.Context, data interface{}) error {
                    return productService.ReleaseInventory(orderData.ReservationID)
                },
            },
            {
                Name: "CreateOrder",
                Action: func(ctx context.Context, data interface{}) error {
                    // Call Order Service
                    return orderService.CreateOrder(orderData)
                },
                Compensate: func(ctx context.Context, data interface{}) error {
                    return orderService.CancelOrder(orderData.OrderID)
                },
            },
            {
                Name: "ProcessPayment",
                Action: func(ctx context.Context, data interface{}) error {
                    // Call Payment Service
                    return paymentService.ProcessPayment(orderData)
                },
                Compensate: func(ctx context.Context, data interface{}) error {
                    return paymentService.RefundPayment(orderData.PaymentID)
                },
            },
        },
    }
}
```

### Project Structure

```
database-per-service/
├── services/
│   ├── user-service/
│   │   ├── main.go
│   │   ├── database.sql
│   │   └── events.go
│   ├── order-service/
│   │   ├── main.go
│   │   ├── database.sql
│   │   └── events.go
│   └── product-service/
│       ├── main.go
│       └── schema.js
├── api-gateway/
│   ├── composition.go
│   └── routes.go
├── read-models/
│   ├── order-read-model/
│   └── projectors/
├── sync/
│   ├── event-bus.go
│   └── cdc.go
└── saga/
    └── order-saga.go
```

### Trade-offs

**Benefits:**
- ✅ Service autonomy
- ✅ Independent scaling
- ✅ Technology diversity
- ✅ Fault isolation
- ✅ Team independence

**Challenges:**
- ❌ Distributed transactions complex
- ❌ Data duplication
- ❌ Eventual consistency
- ❌ Cross-service queries difficult
- ❌ More infrastructure

### Best Practices

1. **Define clear ownership** - Each service owns its data
2. **Use events for sync** - Async communication
3. **Embrace eventual consistency** - Don't fight it
4. **Denormalize when needed** - For query performance
5. **Use sagas for transactions** - Not 2PC
6. **Monitor data consistency** - Detect drift
7. **Version events** - For backward compatibility

---

## Project 49: Email Service Integration (SendGrid/AWS SES)

### Covers Communication Services
- Email Service Providers
- SendGrid API
- AWS SES
- Template Management
- Bulk Email Sending
- Email Tracking
- Bounce Handling
- Unsubscribe Management

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 7 (REST API)
- SendGrid account (free tier)
- AWS account (optional for SES)

**System Requirements:**
- SMTP server or API credentials
- Redis for rate limiting
- Database for tracking

### Overview

Build a production-ready email service with SendGrid and AWS SES integration. Handle templates, bulk sending, bounce management, and email tracking.

### What You'll Learn
- SendGrid API integration
- AWS SES setup and usage
- Email templating (HTML + text)
- Bulk email sending
- Webhook handling (bounces, opens, clicks)
- Rate limiting for email
- Email queue management
- Unsubscribe management

### Core Features

1. **Email Sending:**
   - Transactional emails
   - Bulk/marketing emails
   - Template-based emails
   - Attachments
   - Inline images

2. **Template Management:**
   - HTML templates
   - Variable substitution
   - Multi-language support
   - Template versioning
   - Preview before sending

3. **Tracking & Analytics:**
   - Delivery tracking
   - Open tracking
   - Click tracking
   - Bounce handling
   - Complaint handling

4. **Management:**
   - Unsubscribe links
   - Suppression list
   - Email verification
   - Rate limiting
   - Retry logic

### Implementation Guide

**What you need to create:**

1. **SendGrid Service**
   - Initialize SendGrid client with API key
   - Create method to send transactional emails (to, subject, HTML body, text body)
   - Create method to send with templates (template ID + dynamic data)
   - Handle API responses and errors (check status codes)

2. **AWS SES Service**
   - Set up AWS SDK session with region
   - Create SES client
   - Send email method with destination, message body (HTML + text), subject
   - Bulk send with templates method
   - Handle AWS-specific error responses

3. **Template Engine**
   - Store templates (name, subject, HTML body, text body)
   - Load templates from file or database
   - Render templates with Go's `html/template` package
   - Support variable substitution (user name, links, etc.)
   - Create welcome email, password reset, and notification templates

4. **Email Queue System**
   - Create buffered channel for email jobs
   - Implement rate limiter (use `golang.org/x/time/rate`)
   - Spawn worker goroutines to process queue
   - Implement retry logic with exponential backoff
   - Handle queue full scenarios

5. **Webhook Handler (SendGrid)**
   - Create HTTP endpoint for SendGrid webhooks
   - Parse incoming webhook events (JSON array)
   - Handle event types: delivered, opened, clicked, bounced, dropped
   - Update database with tracking information
   - Add bounced emails to suppression list

6. **Unsubscribe Service**
   - Generate signed unsubscribe tokens (use JWT)
   - Create HTTP endpoint to handle unsubscribe requests
   - Validate tokens and extract email
   - Add email to unsubscribed table
   - Check unsubscribe status before sending emails

### Project Structure

```
email-service/
├── providers/
│   ├── sendgrid.go
│   ├── ses.go
│   └── interface.go
├── templates/
│   ├── engine.go
│   └── templates/
│       ├── welcome.html
│       ├── reset-password.html
│       └── notification.html
├── queue/
│   ├── queue.go
│   └── worker.go
├── webhooks/
│   └── sendgrid.go
├── unsubscribe/
│   └── service.go
├── tracking/
│   └── analytics.go
└── main.go
```

### Best Practices

1. **Always include unsubscribe link** (legal requirement)
2. **Rate limit sending** to avoid provider throttling
3. **Handle bounces** to maintain sender reputation
4. **Use templates** for consistency
5. **Track email performance** (opens, clicks)
6. **Test emails thoroughly** before sending
7. **Warm up IPs** for new domains

---

## Project 51: Search Integration (Algolia/Meilisearch)

### Covers Search Services
- Algolia API
- Meilisearch
- Full-Text Search
- Faceted Search
- Instant Search
- Search Analytics
- Indexing Strategies
- Typo Tolerance

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 7 (REST API)
- Algolia account (free tier) or Meilisearch installed

**System Requirements:**
- Algolia API key or Meilisearch server
- Database with searchable data
- Redis for caching

### Overview

Build advanced search functionality with Algolia or Meilisearch. Implement instant search, faceted filtering, typo tolerance, and search analytics.

### What You'll Learn
- Algolia API integration
- Meilisearch setup and usage
- Indexing strategies
- Faceted search
- Instant search (search-as-you-type)
- Ranking and relevance
- Search analytics
- Query performance optimization

### Core Features

1. **Full-Text Search:**
   - Search across multiple fields
   - Typo tolerance
   - Synonyms
   - Stop words
   - Prefix matching

2. **Faceted Search:**
   - Filter by category
   - Price ranges
   - Multiple filters
   - Dynamic facets
   - Facet counts

3. **Instant Search:**
   - Search-as-you-type
   - Debouncing
   - Autocomplete
   - Query suggestions
   - Highlighting

4. **Analytics:**
   - Popular searches
   - No-results queries
   - Click-through rates
   - Conversion tracking

### Implementation Guide

**What you need to create:**

1. **Algolia Service**
   - Initialize Algolia client with app ID and API key
   - Get index reference
   - Index single product (convert to Algolia object format with objectID)
   - Bulk index products (batch upload)
   - Search with query and filters (category, price range, stock status)
   - Build filter strings (Algolia filter syntax)
   - Configure search settings (typo tolerance, facets, highlighting)
   - Parse and return search results

2. **Meilisearch Service**
   - Initialize Meilisearch client with host and API key
   - Configure index settings (searchable attributes, filterable attributes, sortable attributes)
   - Index documents (add products to search index)
   - Search with filters (Meilisearch filter syntax: `category = 'value'`, `price >= 10`)
   - Support pagination (limit and offset)
   - Enable faceted search
   - Handle search responses

3. **Search API Endpoints**
   - Create instant search endpoint (GET /search?q=query)
   - Check Redis cache before searching
   - Parse query parameters (category, minPrice, maxPrice, inStock, page)
   - Execute search against provider (Algolia or Meilisearch)
   - Cache results in Redis (5-minute TTL)
   - Return JSON response with hits and facets
   - Create autocomplete endpoint (minimum 2 characters, return top 5 results)

4. **Search Synchronization Service**
   - Sync all products from database to search index (bulk operation)
   - Sync single product on update
   - Subscribe to product events (created, updated, deleted)
   - Update search index in real-time
   - Handle index deletion for removed products
   - Implement retry logic for failed sync operations

### Project Structure

```
search-integration/
├── providers/
│   ├── algolia.go
│   ├── meilisearch.go
│   └── interface.go
├── api/
│   ├── search.go
│   ├── autocomplete.go
│   └── facets.go
├── sync/
│   ├── syncer.go
│   └── watcher.go
├── analytics/
│   └── tracker.go
├── frontend/
│   └── instant-search.js
└── main.go
```

### Search Best Practices

1. **Index frequently** - Keep search up-to-date
2. **Use facets** - Help users filter results
3. **Implement typo tolerance** - Improve UX
4. **Cache popular queries** - Reduce load
5. **Track search analytics** - Understand user behavior
6. **Optimize relevance** - Tune ranking
7. **Handle no results** - Suggest alternatives

---

## Project 52: Social Auth Expansion

### Covers OAuth 2.0 Providers
- Multiple OAuth Providers
- Google OAuth
- GitHub OAuth
- Facebook OAuth
- Twitter OAuth
- Microsoft OAuth
- Apple Sign In
- Account Linking
- Provider Abstraction

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 30 (Auth System)
- OAuth 2.0 understanding
- Provider accounts (Google, GitHub, etc.)

### Overview

Expand authentication to support multiple OAuth providers. Implement Google, GitHub, Facebook, Twitter, Microsoft, and Apple Sign In with account linking.

### What You'll Learn
- Multiple OAuth provider integration
- OAuth 2.0 flows
- PKCE (Proof Key for Code Exchange)
- Account linking strategies
- Token management
- Profile synchronization
- Provider-specific quirks

### Core Features

1. **OAuth Providers:**
   - Google Sign In
   - GitHub OAuth
   - Facebook Login
   - Twitter OAuth 2.0
   - Microsoft Account
   - Apple Sign In

2. **Account Linking:**
   - Link multiple providers to one account
   - Detect existing accounts
   - Merge accounts
   - Unlink providers

3. **Profile Management:**
   - Sync profile from providers
   - Profile photos
   - Email verification
   - Provider-specific data

4. **Token Management:**
   - Access token storage
   - Refresh token handling
   - Token expiration
   - Revocation

### Implementation Guide

**What you need to create:**

1. **OAuth Provider Interface**
   - Define interface with methods: GetAuthURL, ExchangeCode, GetUserProfile, RefreshToken
   - Create OAuthToken struct (access token, refresh token, expiry)
   - Create UserProfile struct (provider ID, email, name, picture, email verified)

2. **Google OAuth Provider**
   - Use `golang.org/x/oauth2` package with Google endpoint
   - Configure scopes: userinfo.email, userinfo.profile
   - Generate auth URL with state parameter
   - Exchange authorization code for tokens
   - Fetch user profile from Google API (userinfo endpoint)
   - Parse Google-specific JSON response

3. **GitHub OAuth Provider**
   - Use `golang.org/x/oauth2/github` endpoint
   - Request `user:email` scope
   - Exchange code for token
   - Call GitHub API `/user` endpoint with Authorization header
   - Handle null email (fetch from `/user/emails` endpoint)
   - Parse GitHub user object

4. **Additional Providers (Facebook, Twitter, Microsoft, Apple)**
   - Follow similar pattern for each provider
   - Facebook: Graph API for user profile
   - Twitter: OAuth 2.0 with PKCE
   - Microsoft: Microsoft Identity Platform
   - Apple: Sign In with Apple (requires special handling)

5. **OAuth Controller**
   - Create login endpoint: GET /auth/{provider}
   - Generate random state token (CSRF protection)
   - Store state in session/cookie
   - Redirect to provider's authorization URL
   - Create callback endpoint: GET /auth/{provider}/callback
   - Verify state parameter matches
   - Exchange code for access token
   - Fetch user profile from provider
   - Find or create user account
   - Link provider to user account
   - Create session and set cookie
   - Redirect to dashboard

6. **Account Linking System**
   - Create `linked_accounts` table (user_id, provider, provider_id, tokens, timestamps)
   - Check if provider account already exists (by provider + provider_id)
   - Check if user with email exists (link to existing account)
   - Create new user if neither exists
   - Store access and refresh tokens (encrypted)
   - Allow users to link multiple providers to one account
   - Create endpoint to unlink provider
   - Display linked accounts in user settings

7. **Token Management**
   - Store tokens encrypted in database
   - Implement token refresh before expiration
   - Handle token revocation
   - Update tokens after refresh

### Project Structure

```
social-auth/
├── providers/
│   ├── interface.go
│   ├── google.go
│   ├── github.go
│   ├── facebook.go
│   ├── twitter.go
│   ├── microsoft.go
│   └── apple.go
├── controllers/
│   ├── oauth.go
│   └── linking.go
├── repositories/
│   └── user.go
├── middleware/
│   └── auth.go
└── main.go
```

### Security Best Practices

1. **Validate state parameter** - CSRF protection
2. **Use HTTPS only** - For redirects
3. **Store tokens securely** - Encrypt in database
4. **Implement token refresh** - Before expiration
5. **Handle account conflicts** - Email already exists
6. **Allow account unlinking** - User control
7. **Verify email addresses** - From providers

---

## Project 53: Lock-Free Programming

### Covers Concurrent Programming
- Lock-Free Data Structures
- atomic Package
- Compare-and-Swap (CAS)
- Memory Ordering
- ABA Problem
- Lock-Free Queue
- Lock-Free Stack
- Performance Benchmarks

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 8 (Concurrent Web Scraper)
- Completed Project 33 (Performance Profiling)
- Understanding of goroutines and channels
- Knowledge of race conditions

**System Requirements:**
- Multi-core CPU (to see benefits)
- Go 1.19+
- pprof and benchmarking tools

### Overview

Build lock-free data structures using atomic operations. Eliminate mutex contention in high-concurrency scenarios and achieve better performance through wait-free algorithms.

### What You'll Learn
- atomic.Value, atomic.Int64, atomic.Pointer
- Compare-and-swap operations
- Memory ordering and barriers
- ABA problem and solutions
- Lock-free vs wait-free algorithms
- When to use locks vs lock-free
- Performance characteristics
- Correctness verification

### Core Features

1. **Lock-Free Stack:**
   - Push without locks
   - Pop with CAS retry
   - Handle ABA problem
   - Measure contention

2. **Lock-Free Queue:**
   - Enqueue operation
   - Dequeue operation
   - Multi-producer/multi-consumer
   - Progress guarantees

3. **Lock-Free Counter:**
   - Increment/decrement
   - Read current value
   - Compare with mutex version
   - Benchmark performance

4. **Lock-Free Ring Buffer:**
   - Single-producer/single-consumer
   - Atomic head/tail pointers
   - Wait-free reads/writes
   - Zero-copy design

### Implementation Guide

**What you need to create:**

1. **Lock-Free Stack**
   - Node struct with value and next pointer
   - Head pointer stored as atomic.Pointer
   - Push: Create new node, CAS loop to update head
   - Pop: Load head, CAS to swap with next
   - Handle empty stack case
   - Retry on CAS failure
   - Add version counter to prevent ABA problem

2. **Lock-Free Queue**
   - Head and tail atomic pointers
   - Dummy node technique for simplicity
   - Enqueue: Update tail with CAS
   - Dequeue: Update head with CAS
   - Handle concurrent enqueue/dequeue
   - Measure throughput vs mutex-based queue

3. **Atomic Counter**
   - Use atomic.Int64 for counter
   - AddInt64 for increment
   - LoadInt64 for read
   - CompareAndSwapInt64 for conditional updates
   - Benchmark against mutex counter
   - Test with varying goroutine counts (1, 10, 100, 1000)

4. **Lock-Free Cache**
   - Use atomic.Value for read-heavy cache
   - Store immutable map snapshots
   - Reads are lock-free
   - Writes create new map copy and swap
   - Measure read performance under load

5. **Wait-Free Ring Buffer**
   - Fixed-size array
   - Head and tail indices as atomic.Uint64
   - Producer increments tail
   - Consumer increments head
   - Modulo arithmetic for wrapping
   - Full/empty detection
   - Single-producer/single-consumer only

### Project Structure

```
lock-free/
├── stack/
│   ├── lock_free_stack.go
│   ├── mutex_stack.go
│   └── stack_test.go
├── queue/
│   ├── lock_free_queue.go
│   ├── mutex_queue.go
│   └── queue_test.go
├── counter/
│   ├── atomic_counter.go
│   ├── mutex_counter.go
│   └── counter_bench_test.go
├── ringbuffer/
│   └── spsc_ring.go
└── benchmarks/
    └── contention_test.go
```

### Testing Approach

**What you need to test:**

1. **Correctness Testing:**
   - Run with `-race` detector
   - Concurrent push/pop operations (1000+ goroutines)
   - Verify no data loss
   - Check ordering properties
   - Test edge cases (empty, single element)

2. **Performance Benchmarks:**
   - Compare lock-free vs mutex implementations
   - Vary number of goroutines (1, 2, 4, 8, 16, 32)
   - Measure ops/second
   - CPU utilization
   - Contention levels

3. **Stress Testing:**
   - Run for extended periods
   - Monitor memory usage
   - Check for deadlocks or livelocks
   - Verify progress guarantees

### Performance Considerations

**When lock-free wins:**
- High contention scenarios
- Many readers, few writers
- Real-time requirements
- Predictable latency needed

**When locks are better:**
- Low contention
- Complex operations
- Need for mutual exclusion
- Easier to reason about correctness

**Benchmarking results to expect:**
- Low contention (1-2 goroutines): Mutex ~10% faster
- Medium contention (4-8 goroutines): Similar performance
- High contention (16+ goroutines): Lock-free 2-10x faster
- Read-heavy workloads: Lock-free atomic reads 100x faster

### Best Practices

1. **Use atomic package correctly** - Understand memory ordering
2. **Handle ABA problem** - Version counters or hazard pointers
3. **Test with race detector** - Always run `go test -race`
4. **Benchmark before optimizing** - Locks might be faster
5. **Document memory ordering** - Explain guarantees
6. **Keep it simple** - Lock-free code is hard to debug
7. **Consider channels first** - Go's philosophy

---

## Project 54: SIMD Vector Instructions

### Covers Low-Level Optimization
- SIMD (Single Instruction Multiple Data)
- Assembly Integration
- Vector Operations
- AVX/AVX2/AVX-512
- Data Parallelism
- Cache Optimization
- Benchmarking SIMD
- Cross-Platform Considerations

### Prerequisites & Requirements

**Before Starting:**
- Completed Project 33 (Performance Profiling)
- Completed Project 42 (Assembly for Hot Paths)
- Understanding of CPU architecture
- Assembly basics

**System Requirements:**
- x86-64 CPU with AVX2 support (check with `lscpu` or `sysctl`)
- Go 1.19+
- Assembly knowledge helpful

### Overview

Use SIMD instructions to process multiple data elements in parallel. Implement vectorized operations for computationally intensive tasks like image processing, mathematical computations, and data transformation.

### What You'll Learn
- SIMD concepts and instructions
- Go assembly syntax for SIMD
- Vector register usage (XMM, YMM, ZMM)
- Auto-vectorization limits in Go
- When SIMD provides speedup
- Memory alignment requirements
- Cache-friendly access patterns
- Portability considerations

### Core Features

1. **Vector Addition:**
   - Add two slices element-wise
   - Process 4 floats at once (SSE)
   - Process 8 floats at once (AVX2)
   - Compare with scalar implementation

2. **Image Processing:**
   - Brightness adjustment (SIMD)
   - Grayscale conversion (parallel)
   - Simple filters (blur, sharpen)
   - Pixel operations on 4 channels (RGBA)

3. **Mathematical Operations:**
   - Dot product (vectorized)
   - Matrix multiplication (SIMD)
   - Sum reduction (horizontal add)
   - Min/max finding (vectorized)

4. **String Operations:**
   - Character counting (SIMD)
   - Case conversion (vectorized)
   - Byte search (parallel compare)

### Implementation Guide

**What you need to create:**

1. **Scalar vs SIMD Comparison**
   - Implement vector addition in pure Go (scalar)
   - Implement same operation with assembly SIMD
   - Create benchmark comparing both
   - Measure speedup factor
   - Test with different slice sizes (100, 1000, 10000, 1000000)

2. **SIMD Sum Function**
   - Function signature: `func SumSIMD(data []float32) float32`
   - Load 8 floats into YMM register (AVX2)
   - Accumulate in vector register
   - Horizontal add at end for final sum
   - Handle remainder elements (not multiple of 8)
   - Compare performance with standard loop

3. **Dot Product**
   - Multiply corresponding elements
   - Sum products
   - Use VFMADD instruction (fused multiply-add)
   - Process 8 float pairs per iteration
   - Benchmark against naive implementation

4. **Image Brightness Adjustment**
   - Load 4 pixels (16 bytes) into XMM register
   - Add brightness value to each channel
   - Clamp to 0-255 range
   - Store back to memory
   - Process entire image in vectorized loop

5. **Feature Detection**
   - Detect CPU capabilities at runtime
   - Check for SSE, AVX, AVX2, AVX-512 support
   - Fall back to scalar if SIMD unavailable
   - Use build tags for different implementations

### Project Structure

```
simd/
├── scalar/
│   ├── add.go
│   ├── dot.go
│   └── sum.go
├── simd/
│   ├── add_amd64.s
│   ├── dot_amd64.s
│   ├── sum_amd64.s
│   └── detect.go
├── image/
│   ├── brightness.go
│   └── brightness_amd64.s
├── benchmarks/
│   └── simd_bench_test.go
└── examples/
    └── demo.go
```

### Assembly SIMD Patterns

**What you need to learn:**

1. **Register Usage:**
   - XMM registers: 128-bit (4 floats or 2 doubles)
   - YMM registers: 256-bit (8 floats or 4 doubles)
   - ZMM registers: 512-bit (16 floats or 8 doubles)

2. **Common Instructions:**
   - VMOVUPS: Load unaligned vector
   - VADDPS: Vector add (packed single-precision)
   - VMULPS: Vector multiply
   - VFMADD231PS: Fused multiply-add
   - VHADDPS: Horizontal add

3. **Memory Alignment:**
   - Aligned loads/stores are faster
   - Use VMOVAPS for aligned (16-byte boundary)
   - Use VMOVUPS for unaligned (slower but works)
   - Ensure slice backing array is aligned

4. **Loop Unrolling:**
   - Process multiple vectors per iteration
   - Reduce loop overhead
   - Better instruction-level parallelism
   - Typical: Unroll 2x or 4x

### Performance Expectations

**Typical speedups:**
- Vector addition: 3-7x faster (depends on memory bandwidth)
- Dot product: 4-8x faster
- Sum reduction: 5-10x faster
- Image processing: 2-4x faster (memory-bound)

**When SIMD doesn't help:**
- Small data sizes (< 1000 elements)
- Memory-bound operations
- Complex branching logic
- Irregular access patterns
- Already cache-optimal code

### Testing Strategy

**What you need to test:**

1. **Correctness:**
   - Compare SIMD output with scalar output
   - Test with various input sizes
   - Check edge cases (empty, odd length)
   - Verify remainder handling
   - Use fuzzing for random inputs

2. **Performance:**
   - Benchmark with different data sizes
   - Measure CPU cycles per element
   - Check cache miss rates
   - Profile with perf (Linux) or Instruments (macOS)
   - Verify memory bandwidth utilization

3. **Portability:**
   - Test on different CPUs
   - Verify fallback works without SIMD
   - Check ARM support (NEON)
   - Build tags for architecture-specific code

### Best Practices

1. **Profile first** - Ensure bottleneck is computation, not memory
2. **Check CPU support** - Runtime detection or build constraints
3. **Handle remainders** - Process leftover elements with scalar code
4. **Memory alignment** - Align to 16/32 byte boundaries when possible
5. **Benchmark properly** - Include setup time, avoid compiler optimizations
6. **Keep scalar version** - For testing and non-SIMD platforms
7. **Document assembly** - SIMD code is hard to read

---

# Deployment to Production

## General Deployment Guide

### Platform Options

**1. Heroku (Easiest)**
```bash
# Install Heroku CLI
curl https://cli-assets.heroku.com/install.sh | sh

# Login
heroku login

# Create app
heroku create myapp

# Deploy
git push heroku main

# Set environment variables
heroku config:set DATABASE_URL=postgres://...
```

**2. Railway (Simple, Modern)**
```bash
# Install Railway CLI
npm install -g @railway/cli

# Login
railway login

# Initialize
railway init

# Deploy
railway up

# Environment variables via dashboard
```

**3. Fly.io (Containers)**
```bash
# Install flyctl
curl -L https://fly.io/install.sh | sh

# Login
fly auth login

# Launch (creates fly.toml)
fly launch

# Deploy
fly deploy

# Set secrets
fly secrets set DATABASE_URL=postgres://...
```

**4. AWS ECS (Production Scale)**
```bash
# Build and push Docker image to ECR
aws ecr create-repository --repository-name myapp
docker build -t myapp .
docker tag myapp:latest AWS_ACCOUNT.dkr.ecr.REGION.amazonaws.com/myapp:latest
docker push AWS_ACCOUNT.dkr.ecr.REGION.amazonaws.com/myapp:latest

# Create ECS task definition and service
aws ecs create-cluster --cluster-name myapp-cluster
aws ecs register-task-definition --cli-input-json file://task-definition.json
aws ecs create-service --cluster myapp-cluster --service-name myapp-service --task-definition myapp
```

**5. Google Cloud Run (Serverless)**
```bash
# Build and push
gcloud builds submit --tag gcr.io/PROJECT_ID/myapp

# Deploy
gcloud run deploy myapp --image gcr.io/PROJECT_ID/myapp --platform managed --region us-central1

# Set environment variables
gcloud run services update myapp --update-env-vars DATABASE_URL=postgres://...
```

**6. DigitalOcean App Platform**
```bash
# Connect GitHub repo via dashboard
# Add environment variables
# Automatic deploys on push
```

**7. Kubernetes (Advanced)**
```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myregistry/myapp:latest
        ports:
        - containerPort: 8080
        env:
        - name: DATABASE_URL
          valueFrom:
            secretKeyRef:
              name: myapp-secrets
              key: database-url
```

```bash
kubectl apply -f deployment.yaml
kubectl expose deployment myapp --type=LoadBalancer --port=80 --target-port=8080
```

### Deployment Checklist

**Before Deployment:**
- [ ] All tests pass locally
- [ ] Environment variables documented
- [ ] Database migrations tested
- [ ] Docker image builds successfully
- [ ] Health check endpoint works
- [ ] Logs to stdout/stderr
- [ ] Graceful shutdown implemented
- [ ] Security scan passed (gosec)

**Post-Deployment:**
- [ ] Health check returns 200
- [ ] Logs are flowing
- [ ] Metrics being collected
- [ ] Database connections work
- [ ] Environment variables set correctly
- [ ] SSL/TLS certificate valid
- [ ] DNS resolving correctly
- [ ] Load testing passed

### Zero-Downtime Deployments

**Rolling Update:**
```bash
# Kubernetes
kubectl set image deployment/myapp myapp=myapp:v2 --record
kubectl rollout status deployment/myapp
kubectl rollout undo deployment/myapp  # If issues
```

**Blue-Green:**
```bash
# Deploy green (new version)
kubectl apply -f deployment-green.yaml

# Wait for health checks
kubectl wait --for=condition=ready pod -l version=green

# Switch traffic
kubectl patch service myapp -p '{"spec":{"selector":{"version":"green"}}}'

# Monitor, rollback if needed
kubectl patch service myapp -p '{"spec":{"selector":{"version":"blue"}}}'
```

**Canary:**
```bash
# Deploy canary (10% traffic)
kubectl apply -f deployment-canary.yaml

# Monitor metrics
# If good, gradually increase traffic
# If bad, delete canary deployment
```

---

# Security Best Practices

## Security Checklist for All Projects

### Application Security

**Input Validation:**
- [ ] Validate all user inputs
- [ ] Use parameterized queries (prevent SQL injection)
- [ ] Sanitize HTML output (prevent XSS)
- [ ] Validate file uploads (type, size, content)
- [ ] Rate limit all endpoints
- [ ] Implement CSRF protection for state-changing operations

**Authentication & Authorization:**
- [ ] Use bcrypt/argon2 for password hashing (cost ≥ 12)
- [ ] Implement JWT with short expiration (15-60 min)
- [ ] Use refresh tokens with rotation
- [ ] Require HTTPS for all endpoints
- [ ] Implement role-based access control
- [ ] Add 2FA for sensitive operations
- [ ] Log all authentication events
- [ ] Implement account lockout after failed attempts

**Data Protection:**
- [ ] Encrypt sensitive data at rest
- [ ] Use TLS 1.3 for data in transit
- [ ] Never log passwords, tokens, or PII
- [ ] Implement data retention policies
- [ ] Use environment variables for secrets
- [ ] Rotate credentials regularly
- [ ] Backup encryption keys securely

**API Security:**
- [ ] Use API keys for service-to-service auth
- [ ] Implement rate limiting per user/IP
- [ ] Add request size limits
- [ ] Validate Content-Type headers
- [ ] Return generic error messages (no stack traces)
- [ ] Use CORS restrictively
- [ ] Implement API versioning

### Infrastructure Security

**Server Hardening:**
- [ ] Run as non-root user
- [ ] Minimize attack surface (disable unnecessary services)
- [ ] Keep dependencies updated
- [ ] Use security scanners (gosec, Snyk)
- [ ] Implement firewall rules
- [ ] Regular security patches
- [ ] Monitor for CVEs

**Docker Security:**
- [ ] Use minimal base images (alpine, distroless)
- [ ] Don't run as root
- [ ] Scan images for vulnerabilities
- [ ] Use multi-stage builds
- [ ] Don't include secrets in images
- [ ] Set read-only filesystem
- [ ] Limit resources (CPU, memory)

**Database Security:**
- [ ] Use least privilege for DB users
- [ ] Enable SSL for DB connections
- [ ] Regular backups
- [ ] Encrypt backups
- [ ] Use private networks for DB access
- [ ] Monitor for unusual queries
- [ ] Implement query timeouts

### Security Headers

**Add these headers to all HTTP responses:**
```go
w.Header().Set("X-Frame-Options", "DENY")
w.Header().Set("X-Content-Type-Options", "nosniff")
w.Header().Set("X-XSS-Protection", "1; mode=block")
w.Header().Set("Strict-Transport-Security", "max-age=31536000; includeSubDomains")
w.Header().Set("Content-Security-Policy", "default-src 'self'")
w.Header().Set("Referrer-Policy", "strict-origin-when-cross-origin")
```

### OWASP Top 10 (2021)

**A01: Broken Access Control**
- Implement proper authorization checks
- Test with different user roles
- Use middleware for consistent checks

**A02: Cryptographic Failures**
- Use TLS everywhere
- Don't roll your own crypto
- Use established libraries (bcrypt, argon2)

**A03: Injection**
- Parameterized queries
- Input validation
- Output encoding

**A04: Insecure Design**
- Threat modeling
- Security requirements in design phase
- Principle of least privilege

**A05: Security Misconfiguration**
- Remove default credentials
- Disable debug mode in production
- Security headers configured

**A06: Vulnerable Components**
- Keep dependencies updated
- Use `go mod tidy` regularly
- Subscribe to security advisories

**A07: Authentication Failures**
- Multi-factor authentication
- Secure session management
- Credential stuffing protection

**A08: Software and Data Integrity Failures**
- Verify signatures
- Use SRI for CDN resources
- Verify CI/CD pipeline integrity

**A09: Logging and Monitoring Failures**
- Log security events
- Monitor for anomalies
- Alert on suspicious activity

**A10: Server-Side Request Forgery (SSRF)**
- Validate and sanitize URLs
- Use allowlists for external requests
- Disable unnecessary protocols

### Security Scanning Tools

```bash
# Go security checker
go install github.com/securego/gosec/v2/cmd/gosec@latest
gosec ./...

# Dependency vulnerability scanner
go install golang.org/x/vuln/cmd/govulncheck@latest
govulncheck ./...

# Docker image scanning
docker scan myapp:latest

# Secret scanning
git-secrets --scan

# SAST (Static Application Security Testing)
# Use GitHub Advanced Security or Snyk
```

---

# Technical Interview Guide

## After Each Project: What You Should Be Able to Explain

### After Project 1 (CLI Todo)
**Concepts to Master:**
- Explain difference between `var`, `:=`, and `const`
- When to use pointers vs values
- How JSON marshaling works
- Error handling patterns in Go
- File I/O operations

**Interview Questions:**
1. "How would you persist data without using JSON?"
2. "What happens if two processes write to the same file?"
3. "How would you implement undo/redo?"

---

### After Project 7 (REST API)
**Concepts to Master:**
- REST API design principles
- SQL injection prevention
- JWT authentication flow
- Database connection pooling
- Middleware pattern
- HTTP status codes

**Interview Questions:**
1. "Design a rate limiter for your API"
2. "How do you handle database migrations in production?"
3. "Explain the N+1 query problem and how to solve it"
4. "How would you implement pagination with cursor vs offset?"

---

### After Project 17 (NoSQL)
**Concepts to Master:**
- When to use SQL vs NoSQL
- Cache invalidation strategies
- CAP theorem tradeoffs
- MongoDB indexing
- Redis data structures

**Interview Questions:**
1. "Design a caching layer for read-heavy workload"
2. "How do you handle cache stampede?"
3. "Explain eventual consistency and when it's acceptable"
4. "Design a session store using Redis"

---

### After Project 24 (Message Queue)
**Concepts to Master:**
- Event-driven architecture
- At-least-once vs exactly-once delivery
- Message ordering guarantees
- Dead letter queues
- Consumer group balancing

**Interview Questions:**
1. "Design a distributed task queue"
2. "How do you ensure message processing order?"
3. "What happens when a consumer crashes mid-processing?"
4. "Design an event-driven microservices system"

---

### After Project 28 (gRPC Microservices)
**Concepts to Master:**
- gRPC vs REST tradeoffs
- Service discovery patterns
- Circuit breaker pattern
- Distributed tracing
- Service mesh concepts

**Interview Questions:**
1. "Design a microservices architecture for e-commerce"
2. "How do you handle cascading failures?"
3. "Explain the Saga pattern for distributed transactions"
4. "How would you implement API gateway?"

---

## System Design Interview Templates

### Template 1: Design URL Shortener
**Requirements Gathering:**
- Scale: 100M URLs/month
- Read:Write ratio 100:1
- Shorten URL, redirect, analytics

**High-Level Design:**
- API Gateway → Web Servers → Database → Cache
- Short URL generation (base62 encoding)
- Redis for hot URLs
- PostgreSQL for permanent storage

**Deep Dive:**
- Collision handling
- Custom aliases
- Rate limiting
- Expiration logic
- Analytics (async processing)

**Bottlenecks & Scaling:**
- Database sharding by hash
- CDN for redirects
- Read replicas
- Cache warming

---

### Template 2: Design Rate Limiter
**Algorithms:**
- Token bucket (bursty traffic)
- Leaky bucket (smooth rate)
- Fixed window (simple)
- Sliding window (accurate)

**Implementation:**
- Redis INCR + EXPIRE
- Distributed rate limiting
- Per-user vs per-IP
- Multiple rate limits (minute, hour, day)

**Edge Cases:**
- Clock skew in distributed system
- Race conditions
- Graceful degradation

---

### Template 3: Design News Feed
**Requirements:**
- Fanout on write vs fanout on read
- Ranking algorithm
- Real-time updates
- Pagination

**Components:**
- User Service
- Post Service
- Feed Service
- Timeline Cache
- Notification Service

**Data Model:**
- User graph (followers)
- Posts table
- Feed materialization
- Ranking signals

---

## Behavioral Interview Prep

### STAR Method Stories

**Prepare 2-3 stories for each:**

**Challenge/Conflict:**
- "Describe a time you disagreed with a technical decision"
- Example: "In Project 24, I initially chose RabbitMQ but the team wanted Kafka. I researched tradeoffs, presented data on our use case (low throughput, high reliability), and we agreed on RabbitMQ. Later we migrated to Kafka when scale demanded it."

**Failure:**
- "Tell me about a project that failed"
- Example: "In Project 19 (FUSE), my initial implementation had memory leaks. I learned pprof, found the issue (not closing file descriptors), fixed it, and added tests to prevent regression."

**Success:**
- "Describe your most significant technical achievement"
- Example: "In Project 33, I optimized an API endpoint from 500ms to 50ms. Used pprof to find N+1 queries, added database indexes, implemented caching, and reduced allocations by 80%."

**Leadership:**
- "Tell me about a time you mentored someone"
- Example: "While building Project 28, a junior developer struggled with gRPC streaming. I paired with them, explained bidirectional streams, and together we built a real-time chat feature."

---

## Salary Negotiation

**After completing projects, you can target:**

**Mid-Level Go Developer (10-15 projects)**
- Base: $100K - $140K
- Total Comp: $120K - $160K
- 2-5 years equivalent experience

**Senior Go Developer (20-25 projects)**
- Base: $140K - $180K
- Total Comp: $160K - $220K
- 5-8 years equivalent experience

**Staff/Principal Go Engineer (All 35 projects)**
- Base: $180K - $250K+
- Total Comp: $220K - $400K+
- 8-12 years equivalent experience

**Negotiation Tips:**
1. Always get competing offers
2. Let them anchor first
3. Negotiate total comp, not just base
4. Equity matters at startups
5. Remote work increases options
6. Highlight portfolio projects
7. Focus on impact, not years

---

# Resources and Community

## Essential Books

**Go Language:**
- "The Go Programming Language" - Donovan & Kernighan
- "Go in Action" - Kennedy, Ketelsen, St. Martin
- "Concurrency in Go" - Katherine Cox-Buday
- "100 Go Mistakes and How to Avoid Them" - Teiva Harsanyi

**System Design:**
- "Designing Data-Intensive Applications" - Martin Kleppmann
- "System Design Interview" Vol 1 & 2 - Alex Xu
- "Building Microservices" - Sam Newman
- "Release It!" - Michael Nygard

**Distributed Systems:**
- "Designing Distributed Systems" - Brendan Burns
- "Database Internals" - Alex Petrov

## Online Resources

**Official:**
- [Go Documentation](https://go.dev/doc/)
- [Effective Go](https://go.dev/doc/effective_go)
- [Go Blog](https://go.dev/blog/)
- [Go Wiki](https://github.com/golang/go/wiki)

**Learning Platforms:**
- [Go by Example](https://gobyexample.com/)
- [Go Tour](https://go.dev/tour/)
- [exercism.io/tracks/go](https://exercism.io/tracks/go)
- [LeetCode (Go)](https://leetcode.com/)

**System Design:**
- [System Design Primer](https://github.com/donnemartin/system-design-primer)
- [Roadmap.sh](https://roadmap.sh/golang)
- [High Scalability Blog](http://highscalability.com/)

**Videos:**
- [GopherCon Talks](https://www.youtube.com/c/GopherAcademy)
- [JustForFunc](https://www.youtube.com/c/JustForFunc)
- [Ardan Labs YouTube](https://www.youtube.com/@ardanlabs)

## Community & Support

**Join Our Community:**
- **Discord Server**: [discord.gg/golang-projects](https://discord.gg/golang-projects) (hypothetical - create your own!)
- **GitHub Discussions**: Share your completed projects
- **Reddit**: r/golang, r/learnprogramming
- **Slack**: Gophers Slack (invite.slack.golangbridge.org)

**Show Your Work:**
- Post projects on GitHub with good READMEs
- Write blog posts about what you learned
- Create YouTube tutorials
- Contribute to open source
- Help others in forums

**Get Feedback:**
- Code reviews on r/golang
- Share in Gophers Slack #code-review
- Post in Discord
- Pair program with others

## Project Solutions Repository

**Checkpoint Solutions** (for verification only):
- [github.com/golang-projects/solutions](https://github.com/golang-projects/solutions) (hypothetical)
- Use only after attempting yourself
- Compare your approach vs reference
- Learn alternative implementations

**Contributing:**
- Submit your solutions as PRs
- Show different approaches
- Document your learnings
- Help improve guides

---

# Conclusion & Next Steps

## Your Journey Summary

**If you've completed all 35 projects:**

🎉 **Congratulations!** You're now a professional Go engineer capable of:
- Building production-ready APIs and services
- Designing distributed systems
- Working with microservices architectures
- Optimizing for performance at scale
- Deploying to cloud platforms
- Understanding systems programming and kernel interactions

**Your Portfolio:**
- 35 complete projects with tests and documentation
- Deployed applications in production
- Open source contributions
- Blog posts and tutorials
- GitHub activity graph on fire

**What You Can Build Next:**
- Your own startup/side project
- Contribute to major open source (Kubernetes, Docker, Prometheus)
- Mentor other developers
- Write technical books/courses
- Speak at conferences

---

## Career Paths After This Guide

**Backend Engineer:**
- Apply to companies using Go (Google, Uber, Netflix, Cloudflare, GitHub)
- Focus on your REST API, microservices, and database projects
- Expected: $120K-$180K

**DevOps/SRE:**
- Deep knowledge of infrastructure, monitoring, CI/CD
- Show Projects 13, 29, 31, 32
- Expected: $130K-$200K

**Systems Programmer:**
- Kernel knowledge, performance optimization
- Show Projects 19-21, 33
- Target: Systems companies, infrastructure teams
- Expected: $150K-$220K

**Platform Engineer:**
- Kubernetes operators, service mesh, developer tools
- Show Projects 26, 28, 32
- Expected: $140K-$200K

**Distributed Systems Engineer:**
- Message queues, distributed tracing, multi-region systems
- Show Projects 24-26, 28-29
- Expected: $160K-$250K+

**Technical Lead/Architect:**
- All 35 projects demonstrate breadth and depth
- Can design systems, mentor teams, make technical decisions
- Expected: $180K-$300K+

---

## Final Words

You started this journey to become a Go expert. If you've made it this far—whether you've completed 5 projects or all 35—you've proven something important: **you can commit to hard things and see them through.**

**The Truth About Mastery:**
- It's not about innate talent
- It's about consistent, deliberate practice
- It's about learning from failures
- It's about building, breaking, and rebuilding

**You are not the same person who started Project 1.**

You've debugged race conditions at 2 AM. You've refactored code three times until it felt right. You've read documentation, stack traces, and GitHub issues. You've learned what "production-ready" actually means.

**This guide gave you the map. You walked the path.**

Now go build something that matters. Something that helps people. Something that makes you proud. Something that only you can build because you've developed a unique combination of skills through these 35 projects.

**The Go community welcomes you.**

We need more builders. More contributors. More people who understand that great software is built line by line, test by test, project by project.

**Your next steps:**
1. Deploy your best project to production
2. Write about one thing you learned
3. Help someone else get started
4. Build something new

**Keep building. Keep learning. Keep sharing.**

The world needs what you can create now.

---

**You're now a complete Go engineer. Welcome to the top 1%.**

🚀 **Go forth and build amazing things!**

---

## Acknowledgments

This guide stands on the shoulders of giants:
- The Go team at Google
- The Go community
- roadmap.sh
- All the open source projects that inspired these projects
- Every developer who shared their knowledge

**Contributing to This Guide:**
- Found an error? Open an issue
- Have a better approach? Submit a PR
- Want to add a project? Discuss in Issues
- Help others in Discord/community

**License:** MIT - Free to use, modify, share

**Author:** [Your name/handle]
**Last Updated:** December 2025
**Version:** 2.0

---

**Remember: The best time to start was yesterday. The second best time is now.**

**Happy coding! 🎯**
