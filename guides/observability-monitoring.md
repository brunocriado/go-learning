# Observability & Monitoring in Go

A comprehensive guide to implementing logging, metrics, tracing, and monitoring in your Go applications.

---

## Table of Contents

1. [Introduction](#introduction)
2. [The Three Pillars](#the-three-pillars)
3. [Logging](#logging)
4. [Metrics](#metrics)
5. [Distributed Tracing](#distributed-tracing)
6. [Dashboards & Visualization](#dashboards--visualization)
7. [Complete Example](#complete-example)
8. [Best Practices](#best-practices)

---

## Introduction

**Observability** is the ability to understand the internal state of your system by examining its external outputs. For production Go applications, this means implementing:

- **Logging**: What happened?
- **Metrics**: How much/how often?
- **Tracing**: Where did time go?

This guide will show you how to implement all three in Go using industry-standard tools.

---

## The Three Pillars

### 1. Logs
- **What**: Events that happened in your system
- **When**: Debugging, auditing, compliance
- **Tools**: Zerolog, Zap, Loki

### 2. Metrics
- **What**: Numerical measurements over time
- **When**: Performance, capacity planning, alerting
- **Tools**: Prometheus, Grafana

### 3. Traces
- **What**: Request flow through distributed systems
- **When**: Latency analysis, bottleneck identification
- **Tools**: Jaeger, OpenTelemetry

---

## Logging

### Structured Logging with Zerolog

```go
package main

import (
    "os"
    "github.com/rs/zerolog"
    "github.com/rs/zerolog/log"
)

func init() {
    // Pretty console output for development
    if os.Getenv("ENV") == "development" {
        log.Logger = log.Output(zerolog.ConsoleWriter{Out: os.Stderr})
    }
    
    // JSON output for production
    zerolog.TimeFieldFormat = zerolog.TimeFormatUnix
}

func main() {
    // Different log levels
    log.Debug().Msg("This is debug")
    log.Info().Msg("This is info")
    log.Warn().Msg("This is warning")
    log.Error().Msg("This is error")
    
    // Structured fields
    log.Info().
        Str("user_id", "123").
        Int("count", 42).
        Dur("elapsed", 10).
        Msg("User action completed")
    
    // Error logging
    err := performAction()
    if err != nil {
        log.Error().
            Err(err).
            Str("action", "performAction").
            Msg("Action failed")
    }
}
```

### Alternative: Zap (Uber's logger)

```go
import "go.uber.org/zap"

logger, _ := zap.NewProduction()
defer logger.Sync()

logger.Info("User logged in",
    zap.String("user_id", "123"),
    zap.Int("session_duration", 3600),
)
```

### Sending Logs to Loki

```go
package main

import (
    "github.com/grafana/loki-client-go/loki"
    "github.com/rs/zerolog"
)

func setupLoki() *loki.Client {
    cfg := loki.Config{
        URL: "http://localhost:3100",
    }
    
    client, err := loki.New(cfg)
    if err != nil {
        log.Fatal().Err(err).Msg("Failed to create Loki client")
    }
    
    return client
}
```

---

## Metrics

### Prometheus Metrics

```go
package main

import (
    "net/http"
    "github.com/prometheus/client_golang/prometheus"
    "github.com/prometheus/client_golang/prometheus/promauto"
    "github.com/prometheus/client_golang/prometheus/promhttp"
)

var (
    // Counter: monotonically increasing value
    httpRequestsTotal = promauto.NewCounterVec(
        prometheus.CounterOpts{
            Name: "http_requests_total",
            Help: "Total number of HTTP requests",
        },
        []string{"method", "endpoint", "status"},
    )
    
    // Gauge: value that can go up and down
    activeConnections = promauto.NewGauge(
        prometheus.GaugeOpts{
            Name: "active_connections",
            Help: "Number of active connections",
        },
    )
    
    // Histogram: observations (e.g., request durations)
    httpRequestDuration = promauto.NewHistogramVec(
        prometheus.HistogramOpts{
            Name: "http_request_duration_seconds",
            Help: "HTTP request duration in seconds",
            Buckets: prometheus.DefBuckets,
        },
        []string{"method", "endpoint"},
    )
    
    // Summary: similar to histogram but calculates quantiles
    requestSize = promauto.NewSummaryVec(
        prometheus.SummaryOpts{
            Name: "http_request_size_bytes",
            Help: "HTTP request size in bytes",
        },
        []string{"method", "endpoint"},
    )
)

func metricsMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        timer := prometheus.NewTimer(httpRequestDuration.WithLabelValues(r.Method, r.URL.Path))
        defer timer.ObserveDuration()
        
        activeConnections.Inc()
        defer activeConnections.Dec()
        
        next.ServeHTTP(w, r)
        
        httpRequestsTotal.WithLabelValues(r.Method, r.URL.Path, "200").Inc()
    })
}

func main() {
    // Your application handlers
    http.Handle("/api/users", metricsMiddleware(http.HandlerFunc(usersHandler)))
    
    // Prometheus metrics endpoint
    http.Handle("/metrics", promhttp.Handler())
    
    http.ListenAndServe(":8080", nil)
}
```

### Custom Metrics Example

```go
// Business metrics
var (
    ordersProcessed = promauto.NewCounter(
        prometheus.CounterOpts{
            Name: "orders_processed_total",
            Help: "Total number of orders processed",
        },
    )
    
    orderValue = promauto.NewHistogram(
        prometheus.HistogramOpts{
            Name: "order_value_dollars",
            Help: "Value of orders in dollars",
            Buckets: []float64{10, 50, 100, 500, 1000, 5000},
        },
    )
    
    inventoryLevel = promauto.NewGaugeVec(
        prometheus.GaugeOpts{
            Name: "inventory_level",
            Help: "Current inventory level",
        },
        []string{"product_id"},
    )
)

func processOrder(order Order) {
    ordersProcessed.Inc()
    orderValue.Observe(order.TotalAmount)
    
    for _, item := range order.Items {
        inventoryLevel.WithLabelValues(item.ProductID).Dec()
    }
}
```

---

## Distributed Tracing

### OpenTelemetry Setup

```go
package main

import (
    "context"
    "go.opentelemetry.io/otel"
    "go.opentelemetry.io/otel/exporters/jaeger"
    "go.opentelemetry.io/otel/sdk/resource"
    "go.opentelemetry.io/otel/sdk/trace"
    semconv "go.opentelemetry.io/otel/semconv/v1.4.0"
)

func initTracer() (*trace.TracerProvider, error) {
    // Create Jaeger exporter
    exporter, err := jaeger.New(
        jaeger.WithCollectorEndpoint(jaeger.WithEndpoint("http://localhost:14268/api/traces")),
    )
    if err != nil {
        return nil, err
    }
    
    // Create tracer provider
    tp := trace.NewTracerProvider(
        trace.WithBatcher(exporter),
        trace.WithResource(resource.NewWithAttributes(
            semconv.SchemaURL,
            semconv.ServiceNameKey.String("my-service"),
        )),
    )
    
    otel.SetTracerProvider(tp)
    return tp, nil
}

func main() {
    tp, err := initTracer()
    if err != nil {
        log.Fatal(err)
    }
    defer tp.Shutdown(context.Background())
    
    // Your application code
}
```

### Using Traces

```go
func handleRequest(ctx context.Context, req Request) error {
    tracer := otel.Tracer("my-service")
    
    // Start a span
    ctx, span := tracer.Start(ctx, "handleRequest")
    defer span.End()
    
    // Add attributes
    span.SetAttributes(
        attribute.String("user.id", req.UserID),
        attribute.Int("request.size", len(req.Body)),
    )
    
    // Call downstream service
    result, err := callDatabase(ctx, req.ID)
    if err != nil {
        span.RecordError(err)
        span.SetStatus(codes.Error, err.Error())
        return err
    }
    
    span.SetStatus(codes.Ok, "success")
    return nil
}

func callDatabase(ctx context.Context, id string) (Result, error) {
    tracer := otel.Tracer("my-service")
    
    // Child span
    ctx, span := tracer.Start(ctx, "database.query")
    defer span.End()
    
    span.SetAttributes(
        attribute.String("db.system", "postgresql"),
        attribute.String("db.operation", "SELECT"),
    )
    
    // Database call here
    return db.Query(ctx, id)
}
```

---

## Dashboards & Visualization

### Grafana Dashboard Setup

1. **Install Grafana**:
```bash
docker run -d -p 3000:3000 grafana/grafana:latest
```

2. **Add Prometheus Data Source**:
- Navigate to http://localhost:3000
- Configuration → Data Sources → Add Prometheus
- URL: `http://localhost:9090`

3. **Create Dashboard**:
```json
{
  "dashboard": {
    "title": "Application Metrics",
    "panels": [
      {
        "title": "Request Rate",
        "targets": [{
          "expr": "rate(http_requests_total[5m])"
        }]
      },
      {
        "title": "Error Rate",
        "targets": [{
          "expr": "rate(http_requests_total{status=~\"5..\"}[5m])"
        }]
      },
      {
        "title": "P95 Latency",
        "targets": [{
          "expr": "histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))"
        }]
      }
    ]
  }
}
```

### Key Metrics to Monitor

**Application Health**:
- Request rate
- Error rate
- Request duration (p50, p95, p99)
- Active connections

**System Resources**:
- CPU usage
- Memory usage
- Disk I/O
- Network I/O

**Business Metrics**:
- User signups
- Transactions processed
- Revenue generated
- Feature usage

---

## Complete Example

```go
package main

import (
    "context"
    "net/http"
    "time"
    
    "github.com/rs/zerolog/log"
    "github.com/prometheus/client_golang/prometheus"
    "github.com/prometheus/client_golang/prometheus/promauto"
    "github.com/prometheus/client_golang/prometheus/promhttp"
    "go.opentelemetry.io/otel"
    "go.opentelemetry.io/otel/attribute"
)

var (
    httpDuration = promauto.NewHistogramVec(prometheus.HistogramOpts{
        Name: "http_duration_seconds",
        Help: "Duration of HTTP requests",
    }, []string{"method", "path", "status"})
)

// Combined middleware with logging, metrics, and tracing
func observabilityMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        start := time.Now()
        
        // Start trace
        tracer := otel.Tracer("api-server")
        ctx, span := tracer.Start(r.Context(), r.URL.Path)
        defer span.End()
        
        // Add trace attributes
        span.SetAttributes(
            attribute.String("http.method", r.Method),
            attribute.String("http.url", r.URL.String()),
        )
        
        // Log request
        log.Info().
            Str("method", r.Method).
            Str("path", r.URL.Path).
            Str("remote_addr", r.RemoteAddr).
            Msg("Request started")
        
        // Wrap response writer to capture status
        rw := &responseWriter{ResponseWriter: w, statusCode: http.StatusOK}
        
        // Process request
        next.ServeHTTP(rw, r.WithContext(ctx))
        
        duration := time.Since(start).Seconds()
        
        // Record metrics
        httpDuration.WithLabelValues(
            r.Method,
            r.URL.Path,
            http.StatusText(rw.statusCode),
        ).Observe(duration)
        
        // Log response
        log.Info().
            Str("method", r.Method).
            Str("path", r.URL.Path).
            Int("status", rw.statusCode).
            Float64("duration", duration).
            Msg("Request completed")
    })
}

type responseWriter struct {
    http.ResponseWriter
    statusCode int
}

func (rw *responseWriter) WriteHeader(code int) {
    rw.statusCode = code
    rw.ResponseWriter.WriteHeader(code)
}

func main() {
    // Setup tracing
    tp, _ := initTracer()
    defer tp.Shutdown(context.Background())
    
    // Setup handlers
    mux := http.NewServeMux()
    mux.Handle("/api/users", observabilityMiddleware(http.HandlerFunc(usersHandler)))
    mux.Handle("/metrics", promhttp.Handler())
    
    log.Info().Msg("Server starting on :8080")
    http.ListenAndServe(":8080", mux)
}
```

---

## Best Practices

### Logging
✅ **DO:**
- Use structured logging (JSON in production)
- Log at appropriate levels (DEBUG, INFO, WARN, ERROR)
- Include context (user_id, request_id, trace_id)
- Log errors with stack traces
- Use sampling for high-volume logs

❌ **DON'T:**
- Log sensitive data (passwords, tokens)
- Log at DEBUG level in production
- Use string concatenation for logs
- Log without context

### Metrics
✅ **DO:**
- Use meaningful metric names
- Include units in metric names (`_seconds`, `_bytes`)
- Use labels wisely (low cardinality)
- Set appropriate histogram buckets
- Monitor SLIs (latency, error rate, throughput)

❌ **DON'T:**
- Use high-cardinality labels (user_id, ip_address)
- Create too many metrics
- Forget to document metrics
- Ignore metric collection overhead

### Tracing
✅ **DO:**
- Trace critical paths
- Include meaningful span names
- Add relevant attributes
- Sample traces (100% in dev, 1-5% in prod)
- Use trace context propagation

❌ **DON'T:**
- Trace everything (too expensive)
- Include sensitive data in span attributes
- Create too many spans
- Forget to close spans

---

## Related Projects

Apply observability to these projects:
- [Project 7: REST API](../projects/02-intermediate/project-07-rest-api.md)
- [Project 28: gRPC Microservices](../projects/05-specialized/project-28-grpc-microservices.md)
- [Project 29: Distributed Tracing](../projects/05-specialized/project-29-distributed-tracing.md)

---

[← Back to Getting Started](../getting-started.md) | [↑ Back to Index](../MASTER-INDEX.md)
