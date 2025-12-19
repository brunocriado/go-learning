# Project 31: CI/CD Pipeline Builder

[← Back to Specialized Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a complete CI/CD pipeline that automatically tests, builds, and deploys Go applications covering GitHub Actions, Docker builds, and multi-environment deployments.

**Difficulty:** Specialized  
**Estimated Time:** 3-4 weeks  
**Prerequisites:** Project 23 (Testing), Docker knowledge, Git experience

## What You'll Learn

- GitHub Actions workflows
- GitLab CI pipelines
- Automated testing in CI
- Docker multi-stage builds
- Semantic versioning
- Environment-specific deploys
- Rollback strategies
- Blue-green deployments

## Core Features

1. **CI Pipeline:** Linters, unit tests, integration tests, code coverage, security scanning
2. **Build Pipeline:** Docker image build, multi-arch builds, image tagging, registry push
3. **CD Pipeline:** Deploy to staging/production, health checks, rollback on failure
4. **Environments:** Development, Staging, Production, Review apps for PRs

## GitHub Actions Workflow Example

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
```

## Multi-Stage Dockerfile

```dockerfile
FROM golang:1.21-alpine AS builder
WORKDIR /app
COPY go.* ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 go build -ldflags="-w -s" -o server .

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /app/server .
EXPOSE 8080
CMD ["./server"]
```

## Full Details

Complete implementation in `golang-learning-projects.md` (search "Project 31"):
- Complete GitHub Actions and GitLab CI configs
- Jenkins pipeline setup
- Deployment scripts
- Multi-environment configuration
- Rollback procedures
- Security scanning integration

---

[← Back to Specialized Projects](README.md) | [↑ Back to Index](../../projects-index.md)
