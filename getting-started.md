# Getting Started with Golang Learning Projects

This guide will help you prepare for your Go learning journey. Follow these steps to set up your environment and choose the right learning path.

---

## 📋 Table of Contents

- [How to Use This Guide](#how-to-use-this-guide)
- [Prerequisites Flowchart](#prerequisites-flowchart)
- [Learning Paths](#learning-paths)
- [Skill Assessment](#skill-assessment)
- [Development Environment Setup](#development-environment-setup)
- [Project Template](#project-template)
- [Troubleshooting](#troubleshooting)

---

## How to Use This Guide

### For Complete Beginners
1. Start with **[Project 1: CLI Todo](projects/01-basic/project-01-cli-todo.md)**
2. Complete all **[Basic projects (1-6)](projects/01-basic/)** in order
3. Follow the **[Foundations learning path](#🎯-backend-engineer-path)**
4. Move to Intermediate only after completing all Basic

### For Experienced Developers
1. Review the [Prerequisites Flowchart](#prerequisites-flowchart)
2. Take the [Skill Assessment](#skill-assessment)
3. Jump to your level, but complete prerequisite projects first
4. Consider doing projects 23 (Testing) and 27 (Context) early

### For Career Switchers
1. Follow the [Backend Engineer Path](#🎯-backend-engineer-path) (Projects 1-18, 23, 27-30)
2. Budget 12-18 months of part-time work
3. Build a portfolio site showcasing 3-5 completed projects
4. Focus on projects 7, 17, 28, 30 for interviews

### For Systems Programmers
1. Complete Basic and Intermediate quickly (review if needed)
2. Focus on Advanced (19-21) and Expert (22-25) projects
3. Add Specialized projects for production skills
4. Deep dive into performance optimization (Project 33)

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
         [Project 7: REST API] ← Prerequisite for most Intermediate
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
         ┌─────────────────────────┐
         │ EXPERT & SPECIALIZED    │
         │ (Can do in any order)   │
         └─────────────────────────┘
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
         └→ [35: Multi-Cloud] (needs 7, 9)
              ↓
         ALL COMPLETE ✓
         YOU'RE NOW A GO EXPERT!
```

### Dependency Matrix

**Independent Tracks** (can learn in parallel):
- **Web Track**: 1→4→7→8→17→18→28→30
- **Systems Track**: 1→3→11→12→13→14→15→16→19→20→21
- **Infrastructure Track**: 7→23→24→25→26→29→31→32
- **Optimization Track**: 23→27→33

**Critical Path** (fastest to employability):
Projects: 1, 4, 7, 17, 23, 27, 28, 30 (≈300-400 hours)

---

## Learning Paths

### 🎯 Backend Engineer Path
**Goal**: Full-stack backend engineer ready for industry  
**Time**: 12-18 months part-time

**Phase 1**: Foundations (Months 1-2)
- [Projects 1-6](projects/01-basic/) (all Basic)

**Phase 2**: Backend Core (Months 3-6)
- [Project 7: REST API](projects/02-intermediate/project-07-rest-api.md)
- [Project 17: NoSQL](projects/02-intermediate/project-17-nosql-api.md)
- [Project 18: Search](projects/02-intermediate/project-18-search-engine.md)
- [Project 23: Testing](projects/04-expert/project-23-testing-framework.md)
- Add comprehensive tests to Phase 1 projects

**Phase 3**: Real-time & Distributed (Months 7-10)
- [Project 8: WebSocket](projects/02-intermediate/project-08-websocket-chat.md)
- [Project 24: Message Queue](projects/04-expert/project-24-message-queue.md)
- [Project 26: Load Balancer](projects/05-specialized/project-26-load-balancer.md)
- [Project 27: Context](projects/05-specialized/project-27-context-patterns.md)
- [Project 28: gRPC](projects/05-specialized/project-28-grpc-microservices.md)

**Phase 4**: Production Ready (Months 11-15)
- [Project 29: Tracing](projects/05-specialized/project-29-distributed-tracing.md)
- [Project 30: Auth](projects/05-specialized/project-30-auth-system.md)
- [Project 31: CI/CD](projects/05-specialized/project-31-cicd-pipeline.md)
- [Project 34: Payments](projects/05-specialized/project-34-payment-processing.md)
- [Project 35: Cloud Storage](projects/05-specialized/project-35-multi-cloud-storage.md)
- Add [observability](guides/observability-monitoring.md) to all previous projects

**Phase 5**: Portfolio & Interview Prep (Months 16-18)
- Deploy 3-5 projects to production
- Document architecture decisions
- Practice system design interviews
- Contribute to open source

**Interview Focus**: Projects 7, 17, 28, 30, 26

---

### 🔧 Systems Programmer Path
**Goal**: Low-level systems, infrastructure, performance  
**Time**: 15-24 months

**Phase 1**: Foundations (Months 1-2)
- [Projects 1-6](projects/01-basic/)

**Phase 2**: Systems Basics (Months 3-5)
- [Projects 11-16](projects/02-intermediate/) (all OS interaction)
- [Project 14: Shell](projects/02-intermediate/project-14-custom-shell.md) is critical

**Phase 3**: Advanced Systems (Months 6-12)
- [Project 19: FUSE](projects/03-advanced/project-19-fuse-filesystem.md)
- [Project 20: eBPF](projects/03-advanced/project-20-ebpf-monitor.md)
- [Project 21: Hypervisor](projects/03-advanced/project-21-hypervisor.md)
- These are challenging - take your time

**Phase 4**: Performance & Optimization (Months 13-18)
- [Project 23: Testing](projects/04-expert/project-23-testing-framework.md)
- [Project 27: Context](projects/05-specialized/project-27-context-patterns.md)
- [Project 33: Profiling](projects/05-specialized/project-33-profiling-optimization.md)
- Optimize previous projects for performance

**Phase 5**: Production Systems (Months 19-24)
- [Project 22: Patterns](projects/04-expert/project-22-design-patterns.md)
- [Project 26: Load Balancer](projects/05-specialized/project-26-load-balancer.md)
- [Project 32: K8s Operator](projects/05-specialized/project-32-kubernetes-operator.md)
- Contribute to systems projects (containerd, runc, etc.)

**Interview Focus**: Projects 19-21, 33, deep dives into kernel/performance

---

### ☁️ DevOps/SRE Path
**Goal**: Cloud-native operations, reliability engineering  
**Time**: 12-18 months

**Phase 1**: Foundations (Months 1-2)
- [Projects 1-6](projects/01-basic/)

**Phase 2**: Backend Understanding (Months 3-5)
- [Project 7: REST API](projects/02-intermediate/project-07-rest-api.md)
- [Project 8: WebSocket Chat](projects/02-intermediate/project-08-websocket-chat.md)
- [Project 17: NoSQL](projects/02-intermediate/project-17-nosql-api.md)
- (understand what you'll deploy)

**Phase 3**: Observability & Monitoring (Months 6-9)
- [Project 13: System Monitor](projects/02-intermediate/project-13-system-monitor.md)
- Complete **[Observability section](guides/observability-monitoring.md)** (Prometheus, Grafana, Loki)
- [Project 29: Distributed Tracing](projects/05-specialized/project-29-distributed-tracing.md)
- Add monitoring to all previous projects

**Phase 4**: Infrastructure (Months 10-15)
- [Project 24: Message Queue](projects/04-expert/project-24-message-queue.md)
- [Project 26: Load Balancer](projects/05-specialized/project-26-load-balancer.md)
- [Project 28: gRPC](projects/05-specialized/project-28-grpc-microservices.md) (service mesh concepts)
- [Project 31: CI/CD Pipeline](projects/05-specialized/project-31-cicd-pipeline.md)
- [Project 32: Kubernetes Operator](projects/05-specialized/project-32-kubernetes-operator.md)

**Phase 5**: Production Mastery (Months 16-18)
- [Project 25: Caching/Rate Limiting](projects/04-expert/project-25-distributed-cache.md)
- [Project 30: Auth](projects/05-specialized/project-30-auth-system.md)
- Implement on-call runbooks
- Chaos engineering experiments
- Multi-region deployments

**Interview Focus**: Projects 29, 31, 32, observability, incident response

---

### 🚀 Full-Stack Path
**Goal**: Frontend + Backend + Deployment  
**Time**: 15-20 months

**Phase 1**: Foundations (Months 1-2)
- [Projects 1-6](projects/01-basic/)

**Phase 2**: Backend (Months 3-8)
- [Projects 7, 8, 17, 18, 23](projects/02-intermediate/)
- Learn React/Vue alongside (not covered here)

**Phase 3**: Integration (Months 9-14)
- [Project 28: gRPC](projects/05-specialized/project-28-grpc-microservices.md) (for BFF)
- [Project 30: Auth](projects/05-specialized/project-30-auth-system.md)
- [Project 34: Payments](projects/05-specialized/project-34-payment-processing.md)
- [Project 35: File Upload](projects/05-specialized/project-35-multi-cloud-storage.md)
- Build frontend for projects 7, 8, 17

**Phase 4**: Production (Months 15-20)
- [Project 29: Tracing](projects/05-specialized/project-29-distributed-tracing.md)
- [Project 31: CI/CD](projects/05-specialized/project-31-cicd-pipeline.md)
- [Project 25: Rate Limiting](projects/04-expert/project-25-distributed-cache.md)
- [Project 26: Load Balancer](projects/05-specialized/project-26-load-balancer.md)
- Deploy full-stack apps with CDN, edge

**Interview Focus**: End-to-end system design, both frontend and backend

---

### 📊 Data Engineer Path
**Goal**: Data pipelines, ETL, analytics  
**Time**: 12-16 months

**Phase 1**: Foundations (Months 1-2)
- [Projects 1-6](projects/01-basic/)

**Phase 2**: Data Processing (Months 3-7)
- [Project 10: Web Scraper](projects/02-intermediate/project-10-web-scraper.md)
- [Project 12: Log Analyzer](projects/02-intermediate/project-12-log-analyzer.md)
- [Project 17: NoSQL](projects/02-intermediate/project-17-nosql-api.md)
- [Project 18: OpenSearch](projects/02-intermediate/project-18-search-engine.md)
- Learn Apache Kafka concepts in [Project 24](projects/04-expert/project-24-message-queue.md)

**Phase 3**: Pipelines & Orchestration (Months 8-12)
- [Project 24: Message Queue](projects/04-expert/project-24-message-queue.md) (data streaming)
- [Project 9: File Sync](projects/02-intermediate/project-09-file-sync.md) (data transfer)
- Build ETL pipelines combining previous projects

**Phase 4**: Infrastructure (Months 13-16)
- [Project 25: Caching](projects/04-expert/project-25-distributed-cache.md)
- [Project 31: CI/CD](projects/05-specialized/project-31-cicd-pipeline.md) for data pipelines
- [Project 28: gRPC](projects/05-specialized/project-28-grpc-microservices.md) for data services
- Implement data warehouse patterns

**Interview Focus**: Projects 10, 12, 24, SQL optimization, streaming

---

## Skill Assessment

**Take this quiz to find your starting point:**

### Beginner (Start at [Project 1](projects/01-basic/project-01-cli-todo.md))
- [ ] I've never written Go code
- [ ] I don't know what goroutines are
- [ ] I'm new to programming
- [ ] I've never built a web server

### Intermediate (Start at [Project 7](projects/02-intermediate/project-07-rest-api.md) after reviewing 1-6)
- [ ] I've built CLI tools in Go
- [ ] I understand goroutines and channels
- [ ] I've worked with JSON and HTTP
- [ ] I can write functions and structs

### Advanced (Start at [Project 11](projects/02-intermediate/project-11-process-monitor.md) after completing 1-10)
- [ ] I've built REST APIs with databases
- [ ] I understand concurrency patterns
- [ ] I've deployed Go applications
- [ ] I'm comfortable with testing

### Expert (Start at [Project 19](projects/03-advanced/project-19-fuse-filesystem.md) after completing 1-18)
- [ ] I've built production systems in Go
- [ ] I understand distributed systems concepts
- [ ] I've worked with multiple databases
- [ ] I can debug complex performance issues

### Master (Cherry-pick [projects 22-35](projects-index.md))
- [ ] I've built systems programming projects
- [ ] I understand kernel interactions
- [ ] I've designed distributed architectures
- [ ] I contribute to major open source projects

---

## Development Environment Setup

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

### Database Setup

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

### Monitoring Stack

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

---

## Project Template

Use this template to quickly initialize new Go projects:

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

**Usage:**
```bash
cd ~/go-projects/template
./init_project.sh my-awesome-project
cd my-awesome-project
make run
```

---

## Troubleshooting

### "go: command not found"
```bash
# Add Go to PATH
export PATH=$PATH:/usr/local/go/bin
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc
```

### "cannot find package"
```bash
# Update dependencies
go mod tidy
go mod download

# Clear cache if needed
go clean -modcache
```

### "port already in use"
```bash
# Find process using port
lsof -i :8080  # macOS/Linux
netstat -ano | findstr :8080  # Windows

# Kill process
kill -9 <PID>
```

### Docker permission denied
```bash
# Linux: Add user to docker group
sudo usermod -aG docker $USER
newgrp docker
```

### PostgreSQL connection refused
```bash
# Check if running
brew services list  # macOS
sudo systemctl status postgresql  # Linux

# Start if not running
brew services start postgresql@15
sudo systemctl start postgresql
```

---

## Next Steps

✅ **Setup Complete!** You're ready to start building.

1. **[Review the Projects Index](projects-index.md)** to see all available projects
2. **[Start with Project 1](projects/01-basic/project-01-cli-todo.md)** - CLI Todo Application
3. **[Learn about Observability](guides/observability-monitoring.md)** to build production-ready apps
4. **[Join the Community](resources.md#community--support)** for help and discussion

**Remember**: The journey is long, but every project makes you stronger. Start simple, build consistently, and you'll be amazed at what you can create.

Good luck! 🚀
