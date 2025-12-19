# Project 21: Load Balancer & API Gateway

[← Back to Advanced Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a production-grade load balancer with health checking, multiple algorithms, circuit breaking, and API gateway features.

**Difficulty:** Advanced  
**Estimated Time:** 70-100 hours  
**Prerequisites:** HTTP protocol deep knowledge, networking

## What You'll Learn

- Reverse proxy implementation
- Load balancing algorithms (round-robin, least connections, weighted, consistent hashing)
- Health checks (active and passive)
- Circuit breaker pattern
- Rate limiting (token bucket, sliding window)
- Middleware chain
- TLS termination
- WebSocket proxying
- Prometheus metrics

## Core Features

1. **HTTP/HTTPS Reverse Proxy**
2. **Load Balancing:**
   - Round-robin
   - Least connections
   - Weighted round-robin
   - Consistent hashing (sticky sessions)

3. **Health Checking:**
   - HTTP health checks
   - TCP health checks
   - Configurable intervals and thresholds

4. **Circuit Breaker:**
   - Fail fast when backend unhealthy
   - Automatic recovery

5. **Rate Limiting:**
   - Per client/IP
   - Token bucket algorithm
   - Return 429 Too Many Requests

6. **Middleware:**
   - Logging
   - Metrics
   - CORS
   - Authentication
   - Request transformation

## Implementation Guide

```go
type LoadBalancer struct {
    backends   []*Backend
    balancer   Balancer
    health     *HealthChecker
    middleware []Middleware
}

func (lb *LoadBalancer) ServeHTTP(w http.ResponseWriter, r *http.Request) {
    // Select backend
    backend := lb.balancer.Next()
    if backend == nil {
        http.Error(w, "No healthy backends", http.StatusServiceUnavailable)
        return
    }
    
    // Apply middleware
    handler := lb.applyMiddleware(backend.ReverseProxy)
    handler.ServeHTTP(w, r)
}

// Round-robin balancer
type RoundRobin struct {
    backends []*Backend
    current  uint64
}

func (rr *RoundRobin) Next() *Backend {
    n := atomic.AddUint64(&rr.current, 1)
    
    // Skip unhealthy backends
    for i := 0; i < len(rr.backends); i++ {
        idx := int(n+uint64(i)) % len(rr.backends)
        backend := rr.backends[idx]
        if backend.IsHealthy() {
            return backend
        }
    }
    
    return nil
}
```

## Project Structure

```
load-balancer/
├── main.go
├── proxy/
│   ├── proxy.go          # Core reverse proxy
│   └── websocket.go      # WebSocket handling
├── balancer/
│   ├── interface.go      # Balancer interface
│   ├── roundrobin.go
│   ├── leastconn.go
│   ├── weighted.go
│   └── consistent.go     # Consistent hashing
├── health/
│   ├── checker.go        # Health check orchestrator
│   ├── http.go
│   └── tcp.go
├── middleware/
│   ├── ratelimit.go
│   ├── auth.go
│   ├── circuitbreaker.go
│   ├── retry.go
│   ├── cors.go
│   └── logger.go
├── backend/
│   ├── pool.go           # Backend pool
│   └── server.go
└── metrics/
    └── prometheus.go
```

## Configuration Example

```yaml
backends:
  - url: http://backend1:8080
    weight: 10
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

## Full Details

Complete implementation in `golang-learning-projects.md` (search "Project 21" or around line 8500-9500):
- All balancing algorithms
- Health check implementation
- Circuit breaker logic
- Rate limiting algorithms
- Middleware system
- WebSocket proxying
- Service discovery integration

---

[← Back to Advanced Projects](README.md) | [↑ Back to Index](../../projects-index.md)
