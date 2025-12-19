# Project 26: Service Mesh & Load Balancer

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a production-grade load balancer with multiple algorithms, health checking, and service discovery implementing service mesh patterns.

**Difficulty:** Expert  
**Estimated Time:** 5-6 weeks  
**Prerequisites:** Network programming, understanding of microservices, TCP/HTTP protocols

## What You'll Learn

- Round robin load balancing
- Least connections algorithm
- Weighted load balancing
- Consistent hashing (sticky sessions)
- Active/passive health checks
- Service registry integration
- Retry and timeout policies
- Connection pooling

## Core Features

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
   - Automatic backend removal

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

## Round Robin Implementation

```go
type RoundRobin struct {
    backends []*Backend
    current  uint64
    mu       sync.RWMutex
}

func (rr *RoundRobin) Next() *Backend {
    n := atomic.AddUint64(&rr.current, 1)
    
    rr.mu.RLock()
    defer rr.mu.RUnlock()
    
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

## Least Connections

```go
type LeastConnections struct {
    backends []*Backend
    mu       sync.RWMutex
}

func (lc *LeastConnections) Next() *Backend {
    lc.mu.RLock()
    defer lc.mu.RUnlock()
    
    var selected *Backend
    minConns := int(^uint(0) >> 1) // Max int
    
    for _, backend := range lc.backends {
        if backend.IsHealthy() {
            conns := backend.ActiveConnections()
            if conns < minConns {
                minConns = conns
                selected = backend
            }
        }
    }
    
    return selected
}
```

## Health Checker

```go
type HealthChecker struct {
    backend  *Backend
    interval time.Duration
    timeout  time.Duration
}

func (hc *HealthChecker) Start(ctx context.Context) {
    ticker := time.NewTicker(hc.interval)
    defer ticker.Stop()
    
    for {
        select {
        case <-ctx.Done():
            return
        case <-ticker.C:
            hc.check()
        }
    }
}

func (hc *HealthChecker) check() {
    ctx, cancel := context.WithTimeout(context.Background(), hc.timeout)
    defer cancel()
    
    req, _ := http.NewRequestWithContext(ctx, "GET", 
        hc.backend.URL+"/health", nil)
    
    resp, err := http.DefaultClient.Do(req)
    if err != nil || resp.StatusCode != 200 {
        hc.backend.MarkUnhealthy()
    } else {
        hc.backend.MarkHealthy()
    }
}
```

## Reverse Proxy

```go
type LoadBalancer struct {
    balancer Balancer
    health   *HealthChecker
}

func (lb *LoadBalancer) ServeHTTP(w http.ResponseWriter, r *http.Request) {
    backend := lb.balancer.Next()
    if backend == nil {
        http.Error(w, "No healthy backends", 
            http.StatusServiceUnavailable)
        return
    }
    
    backend.IncrementConnections()
    defer backend.DecrementConnections()
    
    // Reverse proxy
    proxy := httputil.NewSingleHostReverseProxy(backend.URL)
    proxy.ErrorHandler = lb.handleError
    proxy.ServeHTTP(w, r)
}
```

## Project Structure

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
  health_check_timeout: 5s

circuit_breaker:
  failure_threshold: 5
  timeout: 30s
```

## Full Details

Complete implementation in `golang-learning-projects.md` (search "Project 26"):
- All balancing algorithms
- Health check implementation
- Service discovery integration
- Circuit breaker logic
- WebSocket proxying
- TLS termination
- Comprehensive metrics

---

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)
