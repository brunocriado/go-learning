# Project 29: Distributed Tracing & APM

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Implement comprehensive distributed tracing across microservices using OpenTelemetry, integrated with Jaeger, Zipkin, or Tempo.

**Difficulty:** Expert  
**Estimated Time:** 3-4 weeks  
**Prerequisites:** Observability section completed, microservices experience, distributed systems understanding

## What You'll Learn

- OpenTelemetry SDK setup
- Automatic instrumentation
- Manual span creation
- Trace context propagation
- Baggage for cross-service data
- Sampling strategies
- Trace analysis
- Performance bottleneck detection

## Core Features

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

## OpenTelemetry Setup

```go
import (
    "go.opentelemetry.io/otel"
    "go.opentelemetry.io/otel/exporters/jaeger"
    "go.opentelemetry.io/otel/sdk/resource"
    "go.opentelemetry.io/otel/sdk/trace"
    semconv "go.opentelemetry.io/otel/semconv/v1.17.0"
)

func initTracer() (*trace.TracerProvider, error) {
    // Create Jaeger exporter
    exp, err := jaeger.New(jaeger.WithCollectorEndpoint(
        jaeger.WithEndpoint("http://localhost:14268/api/traces"),
    ))
    if err != nil {
        return nil, err
    }
    
    // Create tracer provider
    tp := trace.NewTracerProvider(
        trace.WithBatcher(exp),
        trace.WithResource(resource.NewWithAttributes(
            semconv.SchemaURL,
            semconv.ServiceNameKey.String("my-service"),
            semconv.ServiceVersionKey.String("1.0.0"),
        )),
    )
    
    // Set global tracer provider
    otel.SetTracerProvider(tp)
    
    return tp, nil
}

func main() {
    tp, _ := initTracer()
    defer tp.Shutdown(context.Background())
    
    // Your application
}
```

## HTTP Instrumentation

```go
import "go.opentelemetry.io/contrib/instrumentation/net/http/otelhttp"

func main() {
    // Wrap HTTP handler
    handler := otelhttp.NewHandler(http.HandlerFunc(handleRequest), "api")
    http.Handle("/api", handler)
    
    http.ListenAndServe(":8080", nil)
}

func handleRequest(w http.ResponseWriter, r *http.Request) {
    // Span automatically created by otelhttp
    ctx := r.Context()
    span := trace.SpanFromContext(ctx)
    
    // Add custom attributes
    span.SetAttributes(
        attribute.String("user.id", getUserID(r)),
        attribute.Int("http.status_code", 200),
    )
    
    // Call other services (context propagated automatically)
    makeExternalCall(ctx)
}
```

## Custom Spans

```go
func processOrder(ctx context.Context, order Order) error {
    tracer := otel.Tracer("order-service")
    
    ctx, span := tracer.Start(ctx, "process_order")
    defer span.End()
    
    // Add attributes
    span.SetAttributes(
        attribute.String("order.id", order.ID),
        attribute.Float64("order.total", order.Total),
    )
    
    // Nested span
    ctx, dbSpan := tracer.Start(ctx, "save_to_database")
    err := saveToDatabase(ctx, order)
    if err != nil {
        dbSpan.RecordError(err)
        dbSpan.SetStatus(codes.Error, "database save failed")
    }
    dbSpan.End()
    
    return err
}
```

## Database Tracing

```go
import "go.opentelemetry.io/contrib/instrumentation/database/sql/otelsql"

func main() {
    // Wrap database driver
    db, err := otelsql.Open("postgres", dsn,
        otelsql.WithAttributes(
            semconv.DBSystemPostgreSQL,
        ),
    )
    if err != nil {
        log.Fatal(err)
    }
    defer db.Close()
    
    // All queries automatically traced
    rows, _ := db.QueryContext(ctx, "SELECT * FROM users")
}
```

## Context Propagation (HTTP Client)

```go
func makeExternalCall(ctx context.Context) (*http.Response, error) {
    req, _ := http.NewRequestWithContext(ctx, "GET", "http://api.example.com/data", nil)
    
    // Use otelhttp client (automatically injects trace headers)
    client := http.Client{
        Transport: otelhttp.NewTransport(http.DefaultTransport),
    }
    
    return client.Do(req)
}
```

## Sampling Configuration

```go
// Probabilistic: Sample 10% of traces
tp := trace.NewTracerProvider(
    trace.WithSampler(trace.TraceIDRatioBased(0.1)),
    // ...
)

// Always sample errors
tp := trace.NewTracerProvider(
    trace.WithSampler(trace.ParentBased(
        trace.AlwaysSample(), // root
        trace.WithRemoteParentSampled(trace.AlwaysSample()),
    )),
    // ...
)
```

## Project Structure

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

## Jaeger UI Analysis

**What to look for:**
- End-to-end request latency
- Service call graph
- Slowest operations
- Error traces
- Critical path (longest spans)

**Queries:**
- Find traces with errors: `error=true`
- Find slow traces: `http.status_code=200 duration>1s`
- Find specific operation: `operation="GET /api/users"`

## Full Details

Complete implementation in `golang-learning-projects.md` (search "Project 29"):
- Complete OpenTelemetry setup
- All instrumentation patterns
- Context propagation strategies
- Sampling configurations
- Integration with Jaeger/Zipkin/Tempo
- Trace analysis techniques

---

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)
