# Project 27: Context & Cancellation Patterns

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Comprehensive demonstration of Go's context package patterns for timeout handling, cancellation propagation, and graceful shutdown.

**Difficulty:** Expert  
**Estimated Time:** 2-3 weeks  
**Prerequisites:** 10+ completed projects, understanding of goroutines, HTTP servers

## What You'll Learn

- Context creation and propagation
- Timeout contexts
- Cancellation contexts
- Context values (when to use)
- Context in HTTP handlers
- Context in database queries
- Graceful goroutine shutdown
- Context best practices

## Core Features

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

## Timeout Context Pattern

```go
func FetchWithTimeout(url string) ([]byte, error) {
    // Create context with 5s timeout
    ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
    defer cancel()
    
    req, _ := http.NewRequestWithContext(ctx, "GET", url, nil)
    resp, err := http.DefaultClient.Do(req)
    if err != nil {
        return nil, err
    }
    defer resp.Body.Close()
    
    return io.ReadAll(resp.Body)
}
```

## Cancellation Context

```go
func Worker(ctx context.Context, jobs <-chan Job) {
    for {
        select {
        case <-ctx.Done():
            // Context cancelled, cleanup and return
            log.Println("Worker shutting down:", ctx.Err())
            return
        case job := <-jobs:
            // Process job
            if err := processJob(ctx, job); err != nil {
                log.Printf("Job failed: %v", err)
            }
        }
    }
}

func main() {
    ctx, cancel := context.WithCancel(context.Background())
    defer cancel()
    
    jobs := make(chan Job)
    
    // Start workers
    for i := 0; i < 5; i++ {
        go Worker(ctx, jobs)
    }
    
    // On shutdown signal, cancel context
    sigChan := make(chan os.Signal, 1)
    signal.Notify(sigChan, os.Interrupt)
    <-sigChan
    
    cancel() // Stop all workers
}
```

## Context Values (Use Sparingly)

```go
type contextKey string

const requestIDKey contextKey = "requestID"

func WithRequestID(ctx context.Context, id string) context.Context {
    return context.WithValue(ctx, requestIDKey, id)
}

func GetRequestID(ctx context.Context) string {
    if id, ok := ctx.Value(requestIDKey).(string); ok {
        return id
    }
    return ""
}

// Use in middleware
func RequestIDMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        id := generateRequestID()
        ctx := WithRequestID(r.Context(), id)
        next.ServeHTTP(w, r.WithContext(ctx))
    })
}
```

## HTTP Handler with Context

```go
func HandleSearch(w http.ResponseWriter, r *http.Request) {
    // Get context from request (has timeout from server)
    ctx := r.Context()
    
    query := r.URL.Query().Get("q")
    
    // Pass context to downstream calls
    results, err := searchService.Search(ctx, query)
    if err != nil {
        if err == context.DeadlineExceeded {
            http.Error(w, "Request timeout", http.StatusRequestTimeout)
            return
        }
        http.Error(w, err.Error(), http.StatusInternalServerError)
        return
    }
    
    json.NewEncoder(w).Encode(results)
}
```

## Database Query with Context

```go
func GetUser(ctx context.Context, db *sql.DB, userID int) (*User, error) {
    ctx, cancel := context.WithTimeout(ctx, 5*time.Second)
    defer cancel()
    
    var user User
    err := db.QueryRowContext(ctx, 
        "SELECT id, name, email FROM users WHERE id = ?", userID,
    ).Scan(&user.ID, &user.Name, &user.Email)
    
    if err != nil {
        return nil, err
    }
    return &user, nil
}
```

## Graceful Server Shutdown

```go
func main() {
    server := &http.Server{
        Addr:    ":8080",
        Handler: router,
    }
    
    // Start server in goroutine
    go func() {
        if err := server.ListenAndServe(); err != nil && err != http.ErrServerClosed {
            log.Fatalf("Server error: %v", err)
        }
    }()
    
    // Wait for interrupt signal
    sigChan := make(chan os.Signal, 1)
    signal.Notify(sigChan, os.Interrupt, syscall.SIGTERM)
    <-sigChan
    
    log.Println("Shutting down gracefully...")
    
    // Create shutdown context with timeout
    ctx, cancel := context.WithTimeout(context.Background(), 30*time.Second)
    defer cancel()
    
    // Shutdown server (waits for active connections)
    if err := server.Shutdown(ctx); err != nil {
        log.Printf("Shutdown error: %v", err)
    }
    
    log.Println("Server stopped")
}
```

## Project Structure

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

## Best Practices

**DO:**
- Pass context as first parameter: `func DoWork(ctx context.Context, ...)`
- Use context for cancellation and timeouts
- Propagate context through call chain
- Check `ctx.Done()` in long-running operations
- Use `context.WithTimeout` for operations with time limits

**DON'T:**
- Store context in structs (pass as parameter)
- Use context.Value for required parameters
- Create context without cancel in goroutines
- Ignore context.Err() when context is done

## Full Details

Complete implementation in `golang-learning-projects.md` (search "Project 27"):
- All context patterns with detailed examples
- HTTP integration patterns
- Database query patterns
- Worker pool patterns
- Graceful shutdown strategies
- Common pitfalls and solutions

---

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)
