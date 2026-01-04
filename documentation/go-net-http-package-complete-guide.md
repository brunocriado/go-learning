# The Complete Guide to Go's `net/http` Package

**Go Version:** 1.19+ (Compatible with 1.25.5)  
**Official Documentation:** https://pkg.go.dev/net/http

---

## Table of Contents

1. [Introduction](#introduction)
2. [Core Concepts](#core-concepts)
3. [HTTP Server Architecture](#http-server-architecture)
4. [HTTP Client Architecture](#http-client-architecture)
5. [Handler Interface Deep Dive](#handler-interface-deep-dive)
6. [Request Structure](#request-structure)
7. [Response Structure](#response-structure)
8. [ServeMux and Routing](#servemux-and-routing)
9. [HTTP Methods](#http-methods)
10. [Status Codes Reference](#status-codes-reference)
11. [Headers Management](#headers-management)
12. [Cookies Handling](#cookies-handling)
13. [Middleware Pattern](#middleware-pattern)
14. [Context and Cancellation](#context-and-cancellation)
15. [TLS and HTTPS](#tls-and-https)
16. [File Operations](#file-operations)
17. [Templates Integration](#templates-integration)
18. [Testing HTTP Code](#testing-http-code)
19. [Performance and Optimization](#performance-and-optimization)
20. [Common Patterns](#common-patterns)
21. [Best Practices](#best-practices)
22. [Troubleshooting](#troubleshooting)

---

## Introduction

The `net/http` package provides HTTP client and server implementations. It's one of the most powerful and complete HTTP packages in any standard library, handling HTTP/1.1 and HTTP/2 out of the box.

**What net/http provides:**
- Full-featured HTTP/1.1 and HTTP/2 server
- HTTP/1.1 and HTTP/2 client
- Request routing via ServeMux
- Automatic keep-alive connection pooling
- TLS/HTTPS support
- Cookie management
- File serving capabilities
- Template rendering integration
- Testing utilities (httptest package)

**What net/http does NOT provide:**
- Complex routing with path parameters (pre Go 1.22)
- Authentication middleware
- Session management
- CORS handling
- Request validation
- ORM or database integration

---

## Core Concepts

### The HTTP Protocol: What's Actually Happening

**HTTP (HyperText Transfer Protocol)** is a **text-based** protocol for communication between clients and servers. Every interaction is a **request-response cycle**.

**Why text-based matters:**
- You can literally type HTTP requests by hand in telnet
- Easy to debug (just read the bytes)
- Human-readable headers and status messages
- Platform-independent (text is universal)

**Example raw HTTP request:**
```
GET /api/users HTTP/1.1
Host: example.com
User-Agent: curl/7.68.0
Accept: */*

```

**Example raw HTTP response:**
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 42

{"name":"Alice","email":"alice@example.com"}
```

**Key insight:** HTTP is stateless - each request is independent. The server doesn't remember previous requests (unless you use cookies/sessions to fake state).

### Client-Server Model: The Foundation

```
Client                          Server
  |                               |
  |-- HTTP Request -------------->|
  |   (Method, URL, Headers,      |
  |    Body, etc.)                |
  |                               |
  |<-- HTTP Response -------------|
      (Status, Headers, Body)
```

**Client responsibilities:**
1. **Initiate** communication
2. **Format** requests according to HTTP spec
3. **Wait** for server response
4. **Parse** response

**Server responsibilities:**
1. **Listen** for incoming connections
2. **Parse** HTTP requests
3. **Route** to appropriate handler
4. **Generate** HTTP responses
5. **Handle** thousands of concurrent connections

**Why this model exists:**
- **Separation of concerns**: Client handles UI, server handles data/logic
- **Scalability**: One server can serve many clients
- **Security**: Server controls access to resources
- **Caching**: Responses can be cached at multiple levels

### TCP/IP: The Foundation Beneath HTTP

**HTTP doesn't exist in isolation** - it runs on top of TCP/IP:

```
┌─────────────────────────────────┐
│  Application Layer (HTTP)       │  ← net/http works here
├─────────────────────────────────┤
│  Transport Layer (TCP)          │  ← net package
├─────────────────────────────────┤
│  Network Layer (IP)             │  ← Handled by OS
├─────────────────────────────────┤
│  Link Layer (Ethernet/WiFi)     │  ← Handled by hardware
└─────────────────────────────────┘
```

**What TCP provides:**
- **Reliable delivery**: Packets arrive in order, or you get an error
- **Error detection**: Checksums ensure data integrity
- **Flow control**: Prevents overwhelming the receiver
- **Connection-oriented**: Three-way handshake establishes connection

**HTTP's job on top of TCP:**
- **Structure** the byte stream into requests/responses
- **Define** methods (GET, POST, etc.)
- **Specify** headers format
- **Handle** status codes

**Why this matters for Go:**
When you call `http.ListenAndServe(":8080", handler)`:
1. Go creates a TCP socket on port 8080
2. OS binds that socket to your network interface
3. Socket goes into "listening" mode
4. For each connection, OS does TCP handshake
5. Go reads bytes from TCP stream
6. `net/http` parses those bytes as HTTP
7. Your handler processes the request

### The Handler Interface: Go's Brilliant Abstraction

The fundamental abstraction in `net/http`:

```go
type Handler interface {
    ServeHTTP(ResponseWriter, *Request)
}
```

**Why this interface is genius:**

1. **Single method**: Can't get simpler than this
2. **Takes everything you need**: Request in, Response out
3. **No return value**: Write directly to ResponseWriter (streaming!)
4. **Composable**: Handlers can wrap other handlers (middleware!)

**Philosophical insight:**
```
Everything that handles HTTP is a Handler.
Routing? Handler that calls other handlers.
Middleware? Handler that wraps another handler.
Static files? Handler that reads files.
```

**Everything** that processes HTTP requests must implement this interface.

### Why ResponseWriter is an Interface, Not a Struct

```go
type ResponseWriter interface {
    Header() Header
    Write([]byte) (int, error)
    WriteHeader(statusCode int)
}
```

**This is not an accident.** It's an interface because:

1. **Flexibility**: Different implementations for different scenarios
   - Regular HTTP response
   - HTTP/2 response
   - Test response (httptest.ResponseRecorder)
   - Middleware wrappers

2. **You can't construct a response incorrectly**:
   - Headers must be written before body (enforced by implementation)
   - Status code must be written before body
   - Can't accidentally send invalid HTTP

3. **Allows decoration**:
   ```go
   type gzipResponseWriter struct {
       http.ResponseWriter
       Writer io.Writer
   }
   
   func (w gzipResponseWriter) Write(b []byte) (int, error) {
       return w.Writer.Write(b) // Compress on the fly!
   }
   ```

**Mental model:**
ResponseWriter is like a **write-only file** that enforces HTTP rules.

### The HandlerFunc Adapter: Type Conversion Magic

```go
type HandlerFunc func(ResponseWriter, *Request)

func (f HandlerFunc) ServeHTTP(w ResponseWriter, r *Request) {
    f(w, r)
}
```

**What's happening here?**

This is a **type conversion trick** that converts a function into a Handler.

**Step by step:**
1. `HandlerFunc` is a **type** (not just a function)
2. It's defined as a function signature: `func(ResponseWriter, *Request)`
3. It has a **method** called `ServeHTTP`
4. That method just calls the function itself

**Example:**
```go
// This is just a function
func hello(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello!")
}

// Convert it to a Handler
var handler http.Handler = http.HandlerFunc(hello)

// Now you can use it where Handler is required
mux.Handle("/hello", handler)
```

**Why this pattern exists:**

**Problem:** You have a function `func(ResponseWriter, *Request)` but need a `Handler` interface.

**Solution 1 (ugly):**
```go
type MyHandler struct {
    fn func(http.ResponseWriter, *http.Request)
}

func (h MyHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
    h.fn(w, r)
}

mux.Handle("/", MyHandler{fn: myFunc}) // Verbose!
```

**Solution 2 (elegant):**
```go
mux.Handle("/", http.HandlerFunc(myFunc)) // Clean!
```

**Even better:**
```go
mux.HandleFunc("/", myFunc) // HandleFunc does the conversion for you!
```

**Mental model:**
`HandlerFunc` is a **adapter** that makes functions satisfy the Handler interface.

**This pattern is used throughout Go:**
- `http.HandlerFunc` - function → Handler
- `sort.StringSlice` - []string → sort.Interface
- `http.FileSystem` - interface for file serving

### Why Handlers Return Nothing: The Streaming Insight

Notice handlers **don't return anything**:
```go
func ServeHTTP(w ResponseWriter, r *Request) {
    // No return value!
}
```

**This is intentional.** Here's why:

**Traditional approach (many languages):**
```python
def handle_request(request):
    return Response(body="Hello", status=200)  # Build entire response in memory
```

**Go's approach:**
```go
func handle(w http.ResponseWriter, r *http.Request) {
    w.WriteHeader(200)
    fmt.Fprintf(w, "Hello")  // Stream directly to client
}
```

**Advantages:**

1. **Memory efficient**: Don't need to build entire response in RAM
2. **Can stream**: Send data as it's generated
3. **Progressive rendering**: Client sees HTML as it arrives
4. **Large files**: Can serve GB files without loading into memory

**Example streaming:**
```go
func streamNumbers(w http.ResponseWriter, r *http.Request) {
    for i := 1; i <= 1000000; i++ {
        fmt.Fprintf(w, "%d\n", i)
        if i%1000 == 0 {
            w.(http.Flusher).Flush() // Send chunk to client
            time.Sleep(10 * time.Millisecond)
        }
    }
}
```

**Trade-off:**
You can't change headers after calling `Write()` - they've already been sent!

```go
w.Write([]byte("Hello"))
w.Header().Set("X-Custom", "value") // TOO LATE! Headers already sent!
```

### The Three Core Types

1. **Handler** - Processes requests
2. **Request** - Incoming HTTP request data
3. **ResponseWriter** - Interface to construct responses

---

## HTTP Server Architecture

### What "ListenAndServe" Really Does

```go
func ListenAndServe(addr string, handler Handler) error
```

**This single line does a lot.** Let's break it down:

**Step 1: Create TCP Socket**
```go
// Internally (simplified):
listener, err := net.Listen("tcp", addr)
// Creates a socket bound to port (e.g., :8080)
```

**What this means:**
- OS allocates a socket (file descriptor)
- Binds it to network interface (0.0.0.0) and port (8080)
- Marks it as "listening" (passive socket)

**Step 2: Accept Loop**
```go
for {
    conn, err := listener.Accept()  // Blocks until connection
    go c.serve(conn)                // Handle in goroutine
}
```

**What's happening:**
- **Blocking call**: `Accept()` waits for incoming connection
- **TCP handshake**: OS does SYN, SYN-ACK, ACK automatically
- **New goroutine**: Each connection gets its own goroutine (lightweight thread)
- **Concurrent handling**: Thousands of requests in parallel

**Step 3: Serve Individual Connection**
```go
func (c *conn) serve(ctx context.Context) {
    for {
        req, err := c.readRequest()  // Parse HTTP from TCP stream
        
        serverHandler{c.server}.ServeHTTP(w, req)  // Call your handler
        
        w.finishRequest()  // Flush response
        
        if !w.shouldReuseConnection() {
            break  // Keep-alive check
        }
    }
}
```

**Key insights:**

1. **One goroutine per connection** (not per request!)
   - HTTP/1.1 keep-alive means multiple requests on same connection
   - Goroutine stays alive until connection closes

2. **Request parsing is incremental**
   - Reads from TCP stream byte-by-byte
   - Stops reading body if handler doesn't consume it

3. **Response is streamed**
   - Written directly to TCP socket
   - No buffering unless explicitly added

**Why goroutines instead of threads?**

Traditional thread-per-connection:
- **Thread overhead**: 1-2 MB stack per thread
- **10,000 connections** = 10-20 GB RAM just for stacks!
- **Context switching**: OS kernel must schedule threads

Go's goroutines:
- **Small stack**: Starts at 2-4 KB, grows as needed
- **10,000 connections** = 20-40 MB RAM
- **User-space scheduling**: Go runtime schedules, not OS

**Practical impact:**
```go
// This server can handle 100,000+ concurrent connections
http.ListenAndServe(":8080", handler)
```

### Minimal Server

```go
package main

import (
    "fmt"
    "net/http"
)

func main() {
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Hello, World!")
    })
    
    http.ListenAndServe(":8080", nil)
}
```

**What's actually happening:**

1. `http.HandleFunc("/", ...)` registers with `DefaultServeMux`
2. `ListenAndServe(":8080", nil)` uses `DefaultServeMux` as handler
3. DefaultServeMux is a **global variable** (generally bad practice!)

**Better version (no globals):**
```go
func main() {
    mux := http.NewServeMux()  // Your own mux
    mux.HandleFunc("/", handler)
    http.ListenAndServe(":8080", mux)
}
```

### How ListenAndServe Works

```go
func ListenAndServe(addr string, handler Handler) error
```

**Process:**
1. Creates a TCP listener on `addr`
2. Accepts incoming connections
3. For each connection:
   - Spawns a new goroutine
   - Reads HTTP request
   - Calls `handler.ServeHTTP(w, r)`
   - Writes response back

**Default Handler:**
- If `handler == nil`, uses `http.DefaultServeMux`
- DefaultServeMux is a global ServeMux instance

### Server with Custom Configuration

```go
server := &http.Server{
    Addr:           ":8080",
    Handler:        myHandler,
    ReadTimeout:    10 * time.Second,
    WriteTimeout:   10 * time.Second,
    MaxHeaderBytes: 1 << 20, // 1 MB
    IdleTimeout:    120 * time.Second,
}

log.Fatal(server.ListenAndServe())
```

**Why configure timeouts?**

**Problem:** Without timeouts, a single slow client can hold a connection forever.

**Example attack:**
```
Client connects → sends partial request → never finishes
Server goroutine waits forever → eventually OOM (out of memory)
```

**Server Fields Explained:**

| Field | Type | Purpose | Default | Why It Matters |
|-------|------|---------|---------|----------------|
| `Addr` | `string` | TCP address to listen on | `:http` (port 80) | Which port to bind |
| `Handler` | `Handler` | Request handler | DefaultServeMux | nil = global mux (avoid!) |
| `ReadTimeout` | `Duration` | Max time to **read** request | None! | Prevents slow-read attacks |
| `WriteTimeout` | `Duration` | Max time to **write** response | None! | Prevents slow clients |
| `IdleTimeout` | `Duration` | Keep-alive timeout | Same as ReadTimeout | How long to wait between requests |
| `MaxHeaderBytes` | `int` | Max bytes for request headers | 1 MB | Prevents memory exhaustion |
| `TLSConfig` | `*tls.Config` | TLS configuration | nil | HTTPS settings |
| `ErrorLog` | `*log.Logger` | Error logger | log.Default() | Where to log errors |

**Timeout behavior:**

```
Connection established
     ↓
[ReadTimeout starts]
     ↓
Reading request... (headers + body)
     ↓
[ReadTimeout ends, WriteTimeout starts]
     ↓
Handler executes
     ↓
Writing response...
     ↓
[WriteTimeout ends]
     ↓
[IdleTimeout starts]
     ↓
Waiting for next request (keep-alive)
     ↓
[IdleTimeout ends or new request arrives]
```

**Critical insight:**
- **ReadTimeout** includes reading headers AND body
- **WriteTimeout** includes handler execution AND writing response
- If handler is slow, client may see timeout even if network is fast!

**Production recommendations:**
```go
server := &http.Server{
    Addr:           ":8080",
    Handler:        myHandler,
    ReadTimeout:    5 * time.Second,   // Quick reads
    WriteTimeout:   10 * time.Second,  // Handler + response
    IdleTimeout:    120 * time.Second, // 2 min keep-alive
    MaxHeaderBytes: 1 << 20,           // 1 MB headers max
}
```

### Multiple Servers: Why You'd Want This

```go
func main() {
    // Server 1: Public API
    publicMux := http.NewServeMux()
    publicMux.HandleFunc("/api/", apiHandler)
    go http.ListenAndServe(":8080", publicMux)

    // Server 2: Admin interface
    adminMux := http.NewServeMux()
    adminMux.HandleFunc("/admin/", adminHandler)
    http.ListenAndServe(":8081", adminMux)
}
```

**Use cases:**

1. **Separation of concerns:**
   - Public API on :8080 (restricted, rate-limited)
   - Admin API on :8081 (localhost only, no rate limit)
   - Metrics on :9090 (Prometheus format)

2. **Different security requirements:**
   ```go
   // Public: HTTPS with strict timeouts
   publicServer := &http.Server{
       Addr:         ":443",
       Handler:      publicHandler,
       ReadTimeout:  5 * time.Second,
       WriteTimeout: 5 * time.Second,
       TLSConfig:    strictTLSConfig,
   }
   
   // Internal: HTTP with relaxed timeouts
   internalServer := &http.Server{
       Addr:         "127.0.0.1:8080",
       Handler:      internalHandler,
       ReadTimeout:  30 * time.Second,
   }
   ```

3. **Firewall rules:**
   - External port (80/443) → public interface
   - Internal port (8080) → localhost only

**Architecture pattern:**
```
Internet → Load Balancer → :443 (HTTPS, public)
                              ↓
                         Your App
                              ↓
Admins → VPN → :8080 (HTTP, internal)
Monitoring → :9090 (metrics, internal)
```

---

## HTTP Client Architecture

### The Client-Server Dance: What Happens When You http.Get()

```go
resp, err := http.Get("https://api.github.com")
```

**Behind the scenes (simplified):**

1. **DNS Lookup**
   - Resolve `api.github.com` → IP address (e.g., 140.82.121.6)
   - Cached by OS (don't lookup every time)

2. **TCP Connection**
   - Three-way handshake: SYN → SYN-ACK → ACK
   - OS establishes connection to IP:443

3. **TLS Handshake** (because https)
   - Client hello (supported ciphers)
   - Server hello (chosen cipher + certificate)
   - Key exchange
   - Verify certificate
   - Now encrypted connection established

4. **Send HTTP Request**
   ```
   GET / HTTP/1.1
   Host: api.github.com
   User-Agent: Go-http-client/1.1
   Accept-Encoding: gzip
   
   ```

5. **Read HTTP Response**
   ```
   HTTP/1.1 200 OK
   Content-Type: application/json
   Content-Length: 1234
   
   {"message": "..."}
   ```

6. **Connection Pooling** (important!)
   - Connection NOT closed immediately
   - Kept alive for reuse (HTTP/1.1 keep-alive)
   - Stored in `http.DefaultTransport` connection pool

**Total time:**
- DNS: ~10-50ms (or 0ms if cached)
- TCP handshake: ~30-100ms (round trip)
- TLS handshake: ~100-200ms (multiple round trips)
- HTTP exchange: ~10-100ms (depends on response size)
- **Total**: 150-450ms for first request
- **Subsequent requests** (same host): ~10-100ms (reuse connection!)

### Simple GET Request

```go
resp, err := http.Get("https://api.github.com")
if err != nil {
    log.Fatal(err)
}
defer resp.Body.Close()

body, err := io.ReadAll(resp.Body)
if err != nil {
    log.Fatal(err)
}

fmt.Println(string(body))
```

**Critical:** Always close `resp.Body` even on errors!

**Why?**
- Response body is a TCP connection
- Not closing = connection leak
- Connection pool fills up
- Eventually can't make new requests!

**Correct error handling:**
```go
resp, err := http.Get(url)
if err != nil {
    return err  // No body to close
}
defer resp.Body.Close()  // ALWAYS defer immediately

// Check status AFTER closing is deferred
if resp.StatusCode != 200 {
    return fmt.Errorf("bad status: %d", resp.StatusCode)
}
```

### The Default Client: What You're Really Using

```go
var DefaultClient = &Client{}
```

When you call `http.Get()`, you're actually calling:
```go
func Get(url string) (*Response, error) {
    return DefaultClient.Get(url)
}
```

**DefaultClient configuration:**
- **No timeout!** Requests can hang forever
- Uses `DefaultTransport` (connection pooling enabled)
- Follows up to 10 redirects automatically
- No cookie jar (doesn't persist cookies)

**DefaultTransport configuration:**
```go
var DefaultTransport = &Transport{
    MaxIdleConns:          100,              // Total idle connections
    MaxIdleConnsPerHost:   2,                // Per host
    MaxConnsPerHost:       0,                // Unlimited active
    IdleConnTimeout:       90 * time.Second, // How long to keep idle
    TLSHandshakeTimeout:   10 * time.Second,
    ExpectContinueTimeout: 1 * time.Second,
}
```

**What this means:**

1. **Connection reuse**: Connections are pooled and reused
   ```go
   // First request: DNS + TCP + TLS + HTTP = slow
   http.Get("https://api.github.com/users")
   
   // Second request (same host): Just HTTP = fast!
   http.Get("https://api.github.com/repos")
   ```

2. **Idle connection limits**:
   - Max 100 idle connections total
   - Max 2 idle per host (GitHub, Google, etc.)
   - Idle connections closed after 90 seconds

3. **No global connection limit** (unlimited active!)
   - Can make 1000s of concurrent requests
   - But only keep 100 idle

**Why these defaults matter:**

**Problem 1: No timeout**
```go
// Can hang forever if server never responds
resp, err := http.Get("https://slow-server.com")
```

**Solution:**
```go
client := &http.Client{Timeout: 10 * time.Second}
resp, err := client.Get("https://slow-server.com")
```

**Problem 2: Idle connection leak**
```go
for i := 0; i < 1000; i++ {
    resp, _ := http.Get("https://api.github.com")
    // Forgot to close resp.Body!
}
// Now you have 1000 idle connections (should be 2!)
```

### Custom Client: Taking Control

```go
client := &http.Client{
    Timeout: 10 * time.Second,
    CheckRedirect: func(req *Request, via []*Request) error {
        // Custom redirect logic
        if len(via) >= 5 {
            return errors.New("too many redirects")
        }
        return nil
    },
}

resp, err := client.Get("https://example.com")
```

**Client Fields:**

| Field | Type | Purpose | Default | Why Override |
|-------|------|---------|---------|--------------|
| `Transport` | `RoundTripper` | HTTP transport mechanism | DefaultTransport | Custom retry logic, logging, metrics |
| `CheckRedirect` | `func` | Redirect policy | Follow up to 10 | Prevent redirect loops, custom logic |
| `Jar` | `CookieJar` | Cookie storage | nil | Session handling, auth |
| `Timeout` | `Duration` | Total timeout | None! | **Always set this!** Prevent hangs |

**Timeout applies to entire request:**
```
[Timeout starts]
    ↓
DNS lookup
    ↓
TCP dial
    ↓
TLS handshake
    ↓
Send request
    ↓
Read response
    ↓
[Timeout ends]
```

**If ANY step takes too long, entire request fails.**

### Making Custom Requests

```go
req, err := http.NewRequest("POST", url, bytes.NewBuffer(jsonData))
if err != nil {
    return err
}

req.Header.Set("Content-Type", "application/json")
req.Header.Set("Authorization", "Bearer token123")

client := &http.Client{Timeout: 10 * time.Second}
resp, err := client.Do(req)
```

### Request with Context

```go
ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
defer cancel()

req, err := http.NewRequestWithContext(ctx, "GET", url, nil)
if err != nil {
    return err
}

resp, err := client.Do(req)
```

---

## Handler Interface Deep Dive

### Handler Interface

```go
type Handler interface {
    ServeHTTP(ResponseWriter, *Request)
}
```

### Implementing Handler (Method 1: Struct)

```go
type MyHandler struct {
    message string
}

func (h *MyHandler) ServeHTTP(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, h.message)
}

// Usage
mux.Handle("/hello", &MyHandler{message: "Hello, World!"})
```

### Implementing Handler (Method 2: HandlerFunc)

```go
func myHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, World!")
}

// Convert function to Handler
handler := http.HandlerFunc(myHandler)
mux.Handle("/hello", handler)

// Or use HandleFunc directly
mux.HandleFunc("/hello", myHandler)
```

### Handler vs HandleFunc

```go
// These are equivalent:
mux.Handle("/path", http.HandlerFunc(myFunc))
mux.HandleFunc("/path", myFunc)
```

**HandleFunc is syntactic sugar** for converting a function to a Handler.

### Methods vs Functions as Handlers

**The Problem**: How do you register handlers that need access to shared state (database, cache, config)?

**Solution 1: Standalone Function (No State)**

```go
// ❌ Cannot access any shared data
func myHandler(w http.ResponseWriter, r *http.Request) {
    w.Write([]byte("Hello"))
}

mux.HandleFunc("/hello", myHandler)
```

**Solution 2: Method on Struct (With State)**

```go
// ✅ Has access to all struct fields and methods
type Server struct {
    db    *sql.DB
    cache *Cache
}

func (s *Server) usersHandler(w http.ResponseWriter, r *http.Request) {
    // Can access s.db, s.cache, call other methods on s
    users := s.db.QueryUsers()  // Access to database
    fmt.Fprintf(w, "%v", users)
}

// Register the method - you MUST have an instance
server := &Server{db: myDB, cache: myCache}
mux.HandleFunc("/users", server.usersHandler)
//                        ^^^^^^^^ method on instance
```

**Key Difference:**
- **Function**: Stateless, no access to shared data
- **Method**: Stateful, has access to struct's fields and other methods via receiver

**Why Methods Matter for Real Applications:**

Most web applications need shared state:
- Database connections
- Configuration
- Caches
- Session stores
- Business logic in other methods

**Example: URL Shortener**

```go
type URLShortener struct {
    urls map[string]*URLData
    mu   sync.RWMutex
}

// Method has access to us.urls and us.mu
func (us *URLShortener) shortenHandler(w http.ResponseWriter, r *http.Request) {
    shortCode := us.Shorten(url)  // ✅ Can call other methods
    // Can access us.urls, us.mu
}

// Registration requires an instance
shortener := NewURLShortener()
mux.HandleFunc("/api/shorten", shortener.shortenHandler)
```

**When to Use Each:**
- **Standalone Functions**: Simple handlers, no shared state (rare in production)
- **Methods on Struct**: Production apps with databases, caching, business logic (common)

### Closure-based Handlers

```go
func makeHandler(message string) http.HandlerFunc {
    return func(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, message)
    }
}

mux.HandleFunc("/hello", makeHandler("Hello"))
mux.HandleFunc("/goodbye", makeHandler("Goodbye"))
```

---

## Request Structure

### Request Type

```go
type Request struct {
    Method           string
    URL              *url.URL
    Proto            string      // "HTTP/1.1"
    Header           Header
    Body             io.ReadCloser
    ContentLength    int64
    Host             string
    Form             url.Values
    PostForm         url.Values
    MultipartForm    *multipart.Form
    Trailer          Header
    RemoteAddr       string
    RequestURI       string
    TLS              *tls.ConnectionState
    // ... and more
}
```

### Reading Request Method

```go
func handler(w http.ResponseWriter, r *http.Request) {
    switch r.Method {
    case http.MethodGet:
        // Handle GET
    case http.MethodPost:
        // Handle POST
    case http.MethodPut:
        // Handle PUT
    case http.MethodDelete:
        // Handle DELETE
    default:
        http.Error(w, "Method not allowed", http.StatusMethodNotAllowed)
    }
}
```

### Reading URL Path

```go
func handler(w http.ResponseWriter, r *http.Request) {
    path := r.URL.Path
    // /users/123 → "/users/123"
    
    // Extract segments manually (pre Go 1.22)
    segments := strings.Split(path, "/")
    // [, users, 123]
}
```

### Reading Query Parameters

```go
func handler(w http.ResponseWriter, r *http.Request) {
    // URL: /search?q=golang&page=2
    
    query := r.URL.Query()
    // type: url.Values (map[string][]string)
    
    q := query.Get("q")        // "golang"
    page := query.Get("page")  // "2"
    
    // Multiple values
    tags := query["tags"]      // []string
    
    // Check existence
    if _, ok := query["debug"]; ok {
        // debug parameter present
    }
}
```

### Reading Headers

```go
func handler(w http.ResponseWriter, r *http.Request) {
    // Single value
    contentType := r.Header.Get("Content-Type")
    
    // All values (header can have multiple)
    accepts := r.Header.Values("Accept")
    
    // Check existence
    if _, ok := r.Header["Authorization"]; ok {
        // Authorization header present
    }
    
    // Canonical form
    // "content-type" → "Content-Type"
    r.Header.Get("content-type") // Works, auto-canonicalized
}
```

### Reading Body

**Plain Text:**
```go
func handler(w http.ResponseWriter, r *http.Request) {
    body, err := io.ReadAll(r.Body)
    if err != nil {
        http.Error(w, "Can't read body", http.StatusBadRequest)
        return
    }
    defer r.Body.Close()
    
    text := string(body)
}
```

**JSON:**
```go
type User struct {
    Name  string `json:"name"`
    Email string `json:"email"`
}

func handler(w http.ResponseWriter, r *http.Request) {
    var user User
    err := json.NewDecoder(r.Body).Decode(&user)
    if err != nil {
        http.Error(w, "Invalid JSON", http.StatusBadRequest)
        return
    }
    defer r.Body.Close()
}
```

**IMPORTANT:** Body can only be read once! It's an `io.ReadCloser`.

### Reading Form Data

**application/x-www-form-urlencoded:**
```go
func handler(w http.ResponseWriter, r *http.Request) {
    err := r.ParseForm()
    if err != nil {
        http.Error(w, "Can't parse form", http.StatusBadRequest)
        return
    }
    
    username := r.FormValue("username")
    password := r.FormValue("password")
}
```

**multipart/form-data (file uploads):**
```go
func handler(w http.ResponseWriter, r *http.Request) {
    err := r.ParseMultipartForm(10 << 20) // 10 MB max
    if err != nil {
        http.Error(w, "Can't parse form", http.StatusBadRequest)
        return
    }
    
    file, header, err := r.FormFile("upload")
    if err != nil {
        http.Error(w, "No file uploaded", http.StatusBadRequest)
        return
    }
    defer file.Close()
    
    filename := header.Filename
    // Save file...
}
```

### Reading Cookies

```go
func handler(w http.ResponseWriter, r *http.Request) {
    // Single cookie
    cookie, err := r.Cookie("session_id")
    if err != nil {
        if err == http.ErrNoCookie {
            // Cookie not found
        }
        return
    }
    sessionID := cookie.Value
    
    // All cookies
    cookies := r.Cookies()
    for _, c := range cookies {
        fmt.Printf("%s = %s\n", c.Name, c.Value)
    }
}
```

### Path Values (Go 1.22+)

```go
mux.HandleFunc("/users/{id}", func(w http.ResponseWriter, r *http.Request) {
    id := r.PathValue("id")
    // /users/123 → id = "123"
})

mux.HandleFunc("/files/{path...}", func(w http.ResponseWriter, r *http.Request) {
    path := r.PathValue("path")
    // /files/docs/readme.md → path = "docs/readme.md"
})
```

---

## Response Structure

### ResponseWriter Interface

```go
type ResponseWriter interface {
    Header() Header
    Write([]byte) (int, error)
    WriteHeader(statusCode int)
}
```

### Writing Response Headers

```go
func handler(w http.ResponseWriter, r *http.Request) {
    // MUST be called before Write() or WriteHeader()
    w.Header().Set("Content-Type", "application/json")
    w.Header().Set("X-Custom-Header", "value")
    
    // Add (appends, doesn't replace)
    w.Header().Add("Set-Cookie", "session=abc")
    w.Header().Add("Set-Cookie", "user=123")
    
    // Delete
    w.Header().Del("X-Unwanted")
}
```

### Writing Status Code

```go
func handler(w http.ResponseWriter, r *http.Request) {
    // Method 1: Explicit
    w.WriteHeader(http.StatusCreated) // 201
    
    // Method 2: Implicit (defaults to 200)
    // First Write() call triggers WriteHeader(200)
    w.Write([]byte("content"))
}
```

**IMPORTANT:** `WriteHeader()` can only be called once!

### Writing Body

```go
func handler(w http.ResponseWriter, r *http.Request) {
    // Method 1: Write bytes
    w.Write([]byte("Hello, World!"))
    
    // Method 2: fmt.Fprintf
    fmt.Fprintf(w, "User ID: %d", userID)
    
    // Method 3: io.Copy
    io.Copy(w, fileReader)
}
```

### Responding with JSON

```go
func respondJSON(w http.ResponseWriter, data interface{}, status int) {
    w.Header().Set("Content-Type", "application/json")
    w.WriteHeader(status)
    
    err := json.NewEncoder(w).Encode(data)
    if err != nil {
        // Can't change status code now!
        log.Printf("JSON encoding error: %v", err)
    }
}

func handler(w http.ResponseWriter, r *http.Request) {
    user := User{Name: "Alice", Email: "alice@example.com"}
    respondJSON(w, user, http.StatusOK)
}
```

### Error Responses

```go
// Method 1: http.Error
http.Error(w, "Not found", http.StatusNotFound)
// Sets status, writes message, sets text/plain header

// Method 2: Custom error response
func respondError(w http.ResponseWriter, message string, code int) {
    w.Header().Set("Content-Type", "application/json")
    w.WriteHeader(code)
    json.NewEncoder(w).Encode(map[string]string{
        "error": message,
    })
}
```

### Redirects

```go
func handler(w http.ResponseWriter, r *http.Request) {
    http.Redirect(w, r, "/new-path", http.StatusMovedPermanently)
    // Sets Location header and status code
}
```

### Setting Cookies

```go
func handler(w http.ResponseWriter, r *http.Request) {
    cookie := &http.Cookie{
        Name:     "session_id",
        Value:    "abc123xyz",
        Path:     "/",
        MaxAge:   3600,    // 1 hour
        HttpOnly: true,    // Not accessible via JavaScript
        Secure:   true,    // Only sent over HTTPS
        SameSite: http.SameSiteStrictMode,
    }
    
    http.SetCookie(w, cookie)
}
```

---

## ServeMux and Routing

### What is ServeMux?

ServeMux is a request **multiplexer** - it routes requests to handlers based on URL patterns.

```go
type ServeMux struct {
    // contains filtered or unexported fields
}
```

### Creating ServeMux

```go
// Default global mux (avoid in production)
http.DefaultServeMux

// Custom mux (recommended)
mux := http.NewServeMux()
```

### Registering Handlers

```go
mux := http.NewServeMux()

// Method 1: HandleFunc (function)
mux.HandleFunc("/path", func(w http.ResponseWriter, r *http.Request) {
    // handler code
})

// Method 2: Handle (Handler interface)
mux.Handle("/path", myHandler)

// Method 3: Handle with HandlerFunc adapter
mux.Handle("/path", http.HandlerFunc(myFunc))
```

### Pattern Matching (Pre Go 1.22)

```go
mux.HandleFunc("/", rootHandler)
// Matches: /, /anything, /foo/bar (everything)

mux.HandleFunc("/users", usersHandler)
// Matches: /users exactly

mux.HandleFunc("/users/", usersHandler)
// Matches: /users/, /users/123, /users/123/profile
```

**Rule:** Patterns ending with `/` match that path and everything under it.

### Pattern Matching (Go 1.22+)

**Method-specific routes:**
```go
mux.HandleFunc("GET /users", listUsers)
mux.HandleFunc("POST /users", createUser)
mux.HandleFunc("PUT /users/{id}", updateUser)
mux.HandleFunc("DELETE /users/{id}", deleteUser)
```

**Path parameters:**
```go
mux.HandleFunc("/users/{id}", func(w http.ResponseWriter, r *http.Request) {
    id := r.PathValue("id")
    fmt.Fprintf(w, "User ID: %s", id)
})
```

**Wildcard parameters:**
```go
mux.HandleFunc("/files/{path...}", func(w http.ResponseWriter, r *http.Request) {
    path := r.PathValue("path")
    // /files/docs/readme.md → path = "docs/readme.md"
})
```

**Exact match (ending with `{$}`):**
```go
mux.HandleFunc("/users/{$}", listAllUsers)
// Matches: /users/ exactly
// Does NOT match: /users/123
```

### Route Priority

**More specific routes take precedence:**

```go
mux.HandleFunc("/users/admin", adminHandler)      // Priority 1 (most specific)
mux.HandleFunc("/users/{id}", userHandler)        // Priority 2
mux.HandleFunc("/users/", allUsersHandler)        // Priority 3 (least specific)

// Request to /users/admin → adminHandler
// Request to /users/123 → userHandler
// Request to /users/ → allUsersHandler
```

**Method-specific takes precedence over general:**
```go
mux.HandleFunc("GET /api/data", getHandler)  // Priority 1
mux.HandleFunc("/api/data", anyHandler)      // Priority 2

// GET /api/data → getHandler
// POST /api/data → anyHandler
```

### Conflicting Patterns

```go
// These conflict (panic at registration):
mux.HandleFunc("/users/{id}", handler1)
mux.HandleFunc("/users/{userId}", handler2)
// Both match the same requests with different parameter names
```

### Host-specific Routes

```go
mux.HandleFunc("example.com/", exampleHandler)
mux.HandleFunc("api.example.com/", apiHandler)

// Request to example.com → exampleHandler
// Request to api.example.com → apiHandler
```

---

## HTTP Methods

### Method Constants

```go
const (
    MethodGet     = "GET"
    MethodHead    = "HEAD"
    MethodPost    = "POST"
    MethodPut     = "PUT"
    MethodPatch   = "PATCH"
    MethodDelete  = "DELETE"
    MethodConnect = "CONNECT"
    MethodOptions = "OPTIONS"
    MethodTrace   = "TRACE"
)
```

### Method Semantics

| Method | Safe | Idempotent | Purpose |
|--------|------|------------|---------|
| GET | ✓ | ✓ | Retrieve resource |
| HEAD | ✓ | ✓ | Get headers only |
| POST | ✗ | ✗ | Create resource |
| PUT | ✗ | ✓ | Replace resource |
| PATCH | ✗ | ✗ | Partial update |
| DELETE | ✗ | ✓ | Remove resource |
| OPTIONS | ✓ | ✓ | Get allowed methods |

**Safe:** Doesn't modify server state  
**Idempotent:** Multiple identical requests = same effect as single request

### Handling Methods (Pre Go 1.22)

```go
func handler(w http.ResponseWriter, r *http.Request) {
    switch r.Method {
    case http.MethodGet:
        handleGet(w, r)
    case http.MethodPost:
        handlePost(w, r)
    case http.MethodPut:
        handlePut(w, r)
    case http.MethodDelete:
        handleDelete(w, r)
    default:
        http.Error(w, "Method not allowed", http.StatusMethodNotAllowed)
    }
}
```

### Handling Methods (Go 1.22+)

```go
mux.HandleFunc("GET /resource", getResource)
mux.HandleFunc("POST /resource", createResource)
mux.HandleFunc("PUT /resource/{id}", updateResource)
mux.HandleFunc("DELETE /resource/{id}", deleteResource)
```

---

## Status Codes Reference

### 1xx Informational

```go
http.StatusContinue           // 100
http.StatusSwitchingProtocols // 101
http.StatusProcessing         // 102
```

### 2xx Success

```go
http.StatusOK                 // 200
http.StatusCreated            // 201
http.StatusAccepted           // 202
http.StatusNoContent          // 204
```

### 3xx Redirection

```go
http.StatusMovedPermanently   // 301
http.StatusFound              // 302
http.StatusSeeOther           // 303
http.StatusNotModified        // 304
http.StatusTemporaryRedirect  // 307
http.StatusPermanentRedirect  // 308
```

### 4xx Client Errors

```go
http.StatusBadRequest                    // 400
http.StatusUnauthorized                  // 401
http.StatusForbidden                     // 403
http.StatusNotFound                      // 404
http.StatusMethodNotAllowed              // 405
http.StatusNotAcceptable                 // 406
http.StatusRequestTimeout                // 408
http.StatusConflict                      // 409
http.StatusGone                          // 410
http.StatusPreconditionFailed            // 412
http.StatusRequestEntityTooLarge         // 413
http.StatusUnsupportedMediaType          // 415
http.StatusUnprocessableEntity           // 422
http.StatusTooManyRequests               // 429
```

### 5xx Server Errors

```go
http.StatusInternalServerError           // 500
http.StatusNotImplemented                // 501
http.StatusBadGateway                    // 502
http.StatusServiceUnavailable            // 503
http.StatusGatewayTimeout                // 504
```

### Getting Status Text

```go
text := http.StatusText(http.StatusNotFound)
// "Not Found"
```

---

## Headers Management

### Header Type

```go
type Header map[string][]string
```

Headers are **case-insensitive** and automatically canonicalized.

### Canonical Form

```go
// These all become "Content-Type"
"content-type"
"CONTENT-TYPE"
"Content-Type"

http.CanonicalHeaderKey("content-type") // → "Content-Type"
```

### Reading Headers

```go
func handler(w http.ResponseWriter, r *http.Request) {
    // Get single value (first if multiple)
    ct := r.Header.Get("Content-Type")
    
    // Get all values
    accepts := r.Header.Values("Accept")
    // []string{"text/html", "application/json"}
    
    // Direct map access
    authHeaders := r.Header["Authorization"]
    
    // Check existence
    if _, ok := r.Header["X-Custom"]; ok {
        // Header exists
    }
}
```

### Setting Headers

```go
func handler(w http.ResponseWriter, r *http.Request) {
    // Set (replaces existing)
    w.Header().Set("Content-Type", "application/json")
    
    // Add (appends, doesn't replace)
    w.Header().Add("Cache-Control", "public")
    w.Header().Add("Cache-Control", "max-age=3600")
    
    // Delete
    w.Header().Del("X-Powered-By")
}
```

### Common Headers

**Request Headers:**
```go
r.Header.Get("Accept")           // Content types client accepts
r.Header.Get("Accept-Encoding")  // Encoding client supports
r.Header.Get("Accept-Language")  // Languages client prefers
r.Header.Get("Authorization")    // Authentication credentials
r.Header.Get("Content-Type")     // Body content type
r.Header.Get("Content-Length")   // Body length
r.Header.Get("Cookie")           // Cookies
r.Header.Get("Host")             // Target host
r.Header.Get("Referer")          // Previous page URL
r.Header.Get("User-Agent")       // Client identifier
```

**Response Headers:**
```go
w.Header().Set("Content-Type", "application/json")
w.Header().Set("Content-Length", "1234")
w.Header().Set("Cache-Control", "no-cache")
w.Header().Set("Expires", "Wed, 21 Oct 2025 07:28:00 GMT")
w.Header().Set("Location", "/new-url")  // For redirects
w.Header().Set("Set-Cookie", "session=abc")
w.Header().Set("X-Content-Type-Options", "nosniff")
w.Header().Set("X-Frame-Options", "DENY")
```

### Header Order

**IMPORTANT:** Header order is **not guaranteed**. Don't rely on it.

---

## Cookies Handling

### Cookie Structure

```go
type Cookie struct {
    Name     string
    Value    string
    Path     string
    Domain   string
    Expires  time.Time
    MaxAge   int
    Secure   bool
    HttpOnly bool
    SameSite SameSite
    Raw      string
    Unparsed []string
}
```

### SameSite Values

```go
const (
    SameSiteDefaultMode SameSite = iota + 1
    SameSiteLaxMode
    SameSiteStrictMode
    SameSiteNoneMode
)
```

| Mode | Behavior |
|------|----------|
| Strict | Cookie only sent to same site |
| Lax | Sent on top-level navigation (default) |
| None | Sent with all requests (requires Secure) |

### Setting Cookies

```go
func handler(w http.ResponseWriter, r *http.Request) {
    cookie := &http.Cookie{
        Name:     "session_token",
        Value:    "abc123xyz",
        Path:     "/",           // Available on all paths
        Domain:   "example.com", // Available on domain
        Expires:  time.Now().Add(24 * time.Hour),
        MaxAge:   86400,         // 24 hours (in seconds)
        Secure:   true,          // HTTPS only
        HttpOnly: true,          // Not accessible via JavaScript
        SameSite: http.SameSiteStrictMode,
    }
    
    http.SetCookie(w, cookie)
}
```

### Reading Cookies

```go
func handler(w http.ResponseWriter, r *http.Request) {
    // Single cookie
    cookie, err := r.Cookie("session_token")
    if err != nil {
        if err == http.ErrNoCookie {
            // Cookie not found
            http.Error(w, "Not authenticated", http.StatusUnauthorized)
            return
        }
        // Other error
        http.Error(w, "Error reading cookie", http.StatusBadRequest)
        return
    }
    
    token := cookie.Value
    
    // All cookies
    cookies := r.Cookies()
    for _, c := range cookies {
        fmt.Printf("%s = %s\n", c.Name, c.Value)
    }
}
```

### Deleting Cookies

```go
func handler(w http.ResponseWriter, r *http.Request) {
    cookie := &http.Cookie{
        Name:   "session_token",
        Value:  "",
        Path:   "/",
        MaxAge: -1,  // Delete immediately
    }
    
    http.SetCookie(w, cookie)
}
```

### Cookie Expiration

**Two ways to set expiration:**

1. **Expires** - Absolute time
```go
cookie.Expires = time.Now().Add(24 * time.Hour)
```

2. **MaxAge** - Relative seconds (preferred)
```go
cookie.MaxAge = 3600  // 1 hour
```

If both set, **MaxAge takes precedence**.

---

## Middleware Pattern

### What is Middleware?

Middleware wraps handlers to add functionality:
- Logging
- Authentication
- CORS
- Compression
- Rate limiting
- Request ID tracking

### Middleware Signature

```go
func middleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        // Before handler
        
        next.ServeHTTP(w, r)
        
        // After handler
    })
}
```

### Logging Middleware

```go
func loggingMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        start := time.Now()
        
        // Call next handler
        next.ServeHTTP(w, r)
        
        // Log after completion
        log.Printf(
            "%s %s %v",
            r.Method,
            r.URL.Path,
            time.Since(start),
        )
    })
}
```

### Authentication Middleware

```go
func authMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        token := r.Header.Get("Authorization")
        
        if !isValidToken(token) {
            http.Error(w, "Unauthorized", http.StatusUnauthorized)
            return  // Stop chain, don't call next
        }
        
        // Token valid, proceed
        next.ServeHTTP(w, r)
    })
}
```

### CORS Middleware

```go
func corsMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        w.Header().Set("Access-Control-Allow-Origin", "*")
        w.Header().Set("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE")
        w.Header().Set("Access-Control-Allow-Headers", "Content-Type, Authorization")
        
        // Handle preflight
        if r.Method == http.MethodOptions {
            w.WriteHeader(http.StatusOK)
            return
        }
        
        next.ServeHTTP(w, r)
    })
}
```

### Response Writer Wrapper

To capture status code in middleware:

```go
type responseWriter struct {
    http.ResponseWriter
    statusCode int
}

func (rw *responseWriter) WriteHeader(code int) {
    rw.statusCode = code
    rw.ResponseWriter.WriteHeader(code)
}

func loggingMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        wrapped := &responseWriter{ResponseWriter: w, statusCode: http.StatusOK}
        
        next.ServeHTTP(wrapped, r)
        
        log.Printf("%s %s %d", r.Method, r.URL.Path, wrapped.statusCode)
    })
}
```

### Chaining Middleware

```go
func chain(handler http.Handler, middlewares ...func(http.Handler) http.Handler) http.Handler {
    for i := len(middlewares) - 1; i >= 0; i-- {
        handler = middlewares[i](handler)
    }
    return handler
}

// Usage
finalHandler := chain(
    myHandler,
    loggingMiddleware,
    authMiddleware,
    corsMiddleware,
)

http.ListenAndServe(":8080", finalHandler)
```

### Per-Route Middleware

```go
mux := http.NewServeMux()

// Public routes (no auth)
mux.Handle("/", homeHandler)
mux.Handle("/login", loginHandler)

// Protected routes (with auth)
mux.Handle("/dashboard", authMiddleware(dashboardHandler))
mux.Handle("/profile", authMiddleware(profileHandler))
```

---

## Context and Cancellation

### Request Context

Every `*http.Request` has an associated `context.Context`:

```go
func handler(w http.ResponseWriter, r *http.Request) {
    ctx := r.Context()
    
    // Context is cancelled when:
    // - Client disconnects
    // - Request completes
    // - Timeout occurs
}
```

### Using Context

```go
func handler(w http.ResponseWriter, r *http.Request) {
    ctx := r.Context()
    
    // Long operation
    select {
    case result := <-doWork(ctx):
        json.NewEncoder(w).Encode(result)
    case <-ctx.Done():
        // Request cancelled
        log.Printf("Request cancelled: %v", ctx.Err())
        return
    }
}
```

### Adding Values to Context

```go
type contextKey string

func middleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        // Add value to context
        ctx := context.WithValue(r.Context(), contextKey("user_id"), "123")
        
        // Create new request with updated context
        r = r.WithContext(ctx)
        
        next.ServeHTTP(w, r)
    })
}

func handler(w http.ResponseWriter, r *http.Request) {
    // Read value from context
    userID := r.Context().Value(contextKey("user_id")).(string)
}
```

### Request Timeout

```go
func handler(w http.ResponseWriter, r *http.Request) {
    ctx, cancel := context.WithTimeout(r.Context(), 5*time.Second)
    defer cancel()
    
    // Use ctx for operations
    req, _ := http.NewRequestWithContext(ctx, "GET", url, nil)
    resp, err := http.DefaultClient.Do(req)
    if err != nil {
        if ctx.Err() == context.DeadlineExceeded {
            http.Error(w, "Request timeout", http.StatusGatewayTimeout)
            return
        }
    }
}
```

---

## TLS and HTTPS

### HTTPS Server

```go
func main() {
    mux := http.NewServeMux()
    mux.HandleFunc("/", handler)
    
    log.Fatal(http.ListenAndServeTLS(
        ":443",
        "server.crt",  // Certificate file
        "server.key",  // Private key file
        mux,
    ))
}
```

### Custom TLS Config

```go
tlsConfig := &tls.Config{
    MinVersion: tls.VersionTLS12,
    CipherSuites: []uint16{
        tls.TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384,
        tls.TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256,
    },
}

server := &http.Server{
    Addr:      ":443",
    Handler:   mux,
    TLSConfig: tlsConfig,
}

log.Fatal(server.ListenAndServeTLS("server.crt", "server.key"))
```

### HTTP to HTTPS Redirect

```go
func main() {
    // HTTPS server
    go func() {
        mux := http.NewServeMux()
        mux.HandleFunc("/", handler)
        log.Fatal(http.ListenAndServeTLS(":443", "server.crt", "server.key", mux))
    }()
    
    // HTTP redirect server
    log.Fatal(http.ListenAndServe(":80", http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        http.Redirect(w, r, "https://"+r.Host+r.URL.String(), http.StatusMovedPermanently)
    })))
}
```

### Client with Custom TLS

```go
tr := &http.Transport{
    TLSClientConfig: &tls.Config{
        InsecureSkipVerify: false,  // Don't skip verification!
        MinVersion:         tls.VersionTLS12,
    },
}

client := &http.Client{
    Transport: tr,
    Timeout:   30 * time.Second,
}
```

---

## File Operations

### Serving Static Files

```go
func main() {
    // Serve entire directory
    fs := http.FileServer(http.Dir("./static"))
    http.Handle("/static/", http.StripPrefix("/static/", fs))
    
    http.ListenAndServe(":8080", nil)
}

// URL: http://localhost:8080/static/style.css
// Serves: ./static/style.css
```

### Serving Single File

```go
func downloadHandler(w http.ResponseWriter, r *http.Request) {
    http.ServeFile(w, r, "./files/document.pdf")
}
```

### File Upload

```go
func uploadHandler(w http.ResponseWriter, r *http.Request) {
    // Parse multipart form (10 MB max)
    err := r.ParseMultipartForm(10 << 20)
    if err != nil {
        http.Error(w, "File too large", http.StatusBadRequest)
        return
    }
    
    // Get file from form
    file, handler, err := r.FormFile("upload")
    if err != nil {
        http.Error(w, "No file uploaded", http.StatusBadRequest)
        return
    }
    defer file.Close()
    
    // Create destination
    dst, err := os.Create("./uploads/" + handler.Filename)
    if err != nil {
        http.Error(w, "Can't save file", http.StatusInternalServerError)
        return
    }
    defer dst.Close()
    
    // Copy file
    _, err = io.Copy(dst, file)
    if err != nil {
        http.Error(w, "Upload failed", http.StatusInternalServerError)
        return
    }
    
    fmt.Fprintf(w, "File uploaded: %s", handler.Filename)
}
```

### Download with Custom Headers

```go
func downloadHandler(w http.ResponseWriter, r *http.Request) {
    filename := "report.pdf"
    filepath := "./files/" + filename
    
    // Force download (not inline display)
    w.Header().Set("Content-Disposition", "attachment; filename="+filename)
    w.Header().Set("Content-Type", "application/pdf")
    
    http.ServeFile(w, r, filepath)
}
```

### Embedding Files (Go 1.16+)

```go
//go:embed static/*
var staticFiles embed.FS

func main() {
    fs := http.FileServer(http.FS(staticFiles))
    http.Handle("/static/", fs)
    http.ListenAndServe(":8080", nil)
}
```

---

## Templates Integration

### HTML Template

```go
import "html/template"

func handler(w http.ResponseWriter, r *http.Request) {
    tmpl := template.Must(template.ParseFiles("templates/page.html"))
    
    data := struct {
        Title string
        User  string
    }{
        Title: "Home",
        User:  "Alice",
    }
    
    err := tmpl.Execute(w, data)
    if err != nil {
        http.Error(w, err.Error(), http.StatusInternalServerError)
    }
}
```

**templates/page.html:**
```html
<!DOCTYPE html>
<html>
<head><title>{{.Title}}</title></head>
<body>
    <h1>Welcome, {{.User}}!</h1>
</body>
</html>
```

### Reusable Templates

```go
var templates *template.Template

func init() {
    templates = template.Must(template.ParseGlob("templates/*.html"))
}

func handler(w http.ResponseWriter, r *http.Request) {
    err := templates.ExecuteTemplate(w, "page.html", data)
    if err != nil {
        http.Error(w, err.Error(), http.StatusInternalServerError)
    }
}
```

---

## Testing HTTP Code

### Testing Handlers

```go
import (
    "net/http"
    "net/http/httptest"
    "testing"
)

func TestHandler(t *testing.T) {
    // Create request
    req := httptest.NewRequest("GET", "/hello", nil)
    
    // Create response recorder
    w := httptest.NewRecorder()
    
    // Call handler
    helloHandler(w, req)
    
    // Check status
    if w.Code != http.StatusOK {
        t.Errorf("Expected 200, got %d", w.Code)
    }
    
    // Check body
    expected := "Hello, World!"
    if w.Body.String() != expected {
        t.Errorf("Expected %s, got %s", expected, w.Body.String())
    }
    
    // Check headers
    contentType := w.Header().Get("Content-Type")
    if contentType != "text/plain" {
        t.Errorf("Expected text/plain, got %s", contentType)
    }
}
```

### Testing HTTP Client

```go
func TestClient(t *testing.T) {
    // Create test server
    server := httptest.NewServer(http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        w.WriteHeader(http.StatusOK)
        w.Write([]byte("test response"))
    }))
    defer server.Close()
    
    // Make request to test server
    resp, err := http.Get(server.URL)
    if err != nil {
        t.Fatal(err)
    }
    defer resp.Body.Close()
    
    // Verify response
    body, _ := io.ReadAll(resp.Body)
    if string(body) != "test response" {
        t.Errorf("Unexpected body: %s", body)
    }
}
```

### Testing JSON APIs

```go
func TestJSONAPI(t *testing.T) {
    // Create request with JSON body
    jsonData := []byte(`{"name":"Alice","email":"alice@example.com"}`)
    req := httptest.NewRequest("POST", "/users", bytes.NewBuffer(jsonData))
    req.Header.Set("Content-Type", "application/json")
    
    w := httptest.NewRecorder()
    
    createUserHandler(w, req)
    
    // Check status
    if w.Code != http.StatusCreated {
        t.Errorf("Expected 201, got %d", w.Code)
    }
    
    // Decode response
    var response map[string]interface{}
    json.NewDecoder(w.Body).Decode(&response)
    
    if response["name"] != "Alice" {
        t.Errorf("Unexpected name: %v", response["name"])
    }
}
```

---

## Performance and Optimization

### Connection Pooling

The default `http.Transport` automatically pools connections:

```go
// Default transport settings
DefaultTransport = &Transport{
    MaxIdleConns:          100,
    MaxIdleConnsPerHost:   2,
    IdleConnTimeout:       90 * time.Second,
}
```

### Custom Transport

```go
tr := &http.Transport{
    MaxIdleConns:        100,
    MaxIdleConnsPerHost: 10,
    IdleConnTimeout:     30 * time.Second,
    DisableKeepAlives:   false,  // Keep connections alive
}

client := &http.Client{
    Transport: tr,
    Timeout:   30 * time.Second,
}
```

### Disabling Keep-Alive

```go
tr := &http.Transport{
    DisableKeepAlives: true,
}
```

Use when making one-off requests to many different hosts.

### Response Body Handling

**Always read and close:**
```go
resp, err := client.Get(url)
if err != nil {
    return err
}

// IMPORTANT: Read body even if you don't need it
io.Copy(io.Discard, resp.Body)
resp.Body.Close()
```

If you don't read the body, the connection can't be reused.

### Streaming Large Responses

```go
resp, err := client.Get(url)
if err != nil {
    return err
}
defer resp.Body.Close()

// Stream to file
file, _ := os.Create("download.bin")
defer file.Close()

io.Copy(file, resp.Body)
```

### Server-Side Performance

**Set timeouts:**
```go
server := &http.Server{
    ReadTimeout:  10 * time.Second,
    WriteTimeout: 10 * time.Second,
    IdleTimeout:  120 * time.Second,
}
```

**Limit header size:**
```go
server := &http.Server{
    MaxHeaderBytes: 1 << 20, // 1 MB
}
```

---

## Common Patterns

### REST API Structure

```go
type User struct {
    ID    int    `json:"id"`
    Name  string `json:"name"`
    Email string `json:"email"`
}

var users = make(map[int]User)

// Helper functions
func respondJSON(w http.ResponseWriter, data interface{}, status int) {
    w.Header().Set("Content-Type", "application/json")
    w.WriteHeader(status)
    json.NewEncoder(w).Encode(data)
}

func respondError(w http.ResponseWriter, message string, status int) {
    respondJSON(w, map[string]string{"error": message}, status)
}

// Handlers
func listUsers(w http.ResponseWriter, r *http.Request) {
    userList := make([]User, 0, len(users))
    for _, user := range users {
        userList = append(userList, user)
    }
    respondJSON(w, userList, http.StatusOK)
}

func getUser(w http.ResponseWriter, r *http.Request) {
    id, _ := strconv.Atoi(r.PathValue("id"))
    user, exists := users[id]
    if !exists {
        respondError(w, "User not found", http.StatusNotFound)
        return
    }
    respondJSON(w, user, http.StatusOK)
}

func createUser(w http.ResponseWriter, r *http.Request) {
    var user User
    if err := json.NewDecoder(r.Body).Decode(&user); err != nil {
        respondError(w, "Invalid JSON", http.StatusBadRequest)
        return
    }
    
    user.ID = len(users) + 1
    users[user.ID] = user
    
    respondJSON(w, user, http.StatusCreated)
}

func main() {
    mux := http.NewServeMux()
    mux.HandleFunc("GET /users", listUsers)
    mux.HandleFunc("GET /users/{id}", getUser)
    mux.HandleFunc("POST /users", createUser)
    
    http.ListenAndServe(":8080", mux)
}
```

### Graceful Shutdown

```go
func main() {
    mux := http.NewServeMux()
    mux.HandleFunc("/", handler)
    
    server := &http.Server{
        Addr:    ":8080",
        Handler: mux,
    }
    
    // Start server in goroutine
    go func() {
        if err := server.ListenAndServe(); err != nil && err != http.ErrServerClosed {
            log.Fatalf("Server error: %v", err)
        }
    }()
    
    // Wait for interrupt signal
    quit := make(chan os.Signal, 1)
    signal.Notify(quit, os.Interrupt, syscall.SIGTERM)
    <-quit
    
    log.Println("Shutting down server...")
    
    // Graceful shutdown with timeout
    ctx, cancel := context.WithTimeout(context.Background(), 30*time.Second)
    defer cancel()
    
    if err := server.Shutdown(ctx); err != nil {
        log.Fatal("Server forced to shutdown:", err)
    }
    
    log.Println("Server exited")
}
```

### Request ID Tracking

```go
func requestIDMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        requestID := uuid.New().String()
        
        // Add to response header
        w.Header().Set("X-Request-ID", requestID)
        
        // Add to context
        ctx := context.WithValue(r.Context(), "request_id", requestID)
        
        next.ServeHTTP(w, r.WithContext(ctx))
    })
}
```

### Rate Limiting

```go
import "golang.org/x/time/rate"

var limiter = rate.NewLimiter(1, 3) // 1 req/sec, burst of 3

func rateLimitMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        if !limiter.Allow() {
            http.Error(w, "Rate limit exceeded", http.StatusTooManyRequests)
            return
        }
        next.ServeHTTP(w, r)
    })
}
```

---

## Best Practices

### ✅ DO

1. **Use custom ServeMux**
   ```go
   mux := http.NewServeMux()
   // NOT: http.DefaultServeMux
   ```

2. **Set timeouts**
   ```go
   server := &http.Server{
       ReadTimeout:  10 * time.Second,
       WriteTimeout: 10 * time.Second,
   }
   
   client := &http.Client{
       Timeout: 30 * time.Second,
   }
   ```

3. **Always close response bodies**
   ```go
   resp, err := client.Get(url)
   if err != nil {
       return err
   }
   defer resp.Body.Close()
   ```

4. **Set headers before writing**
   ```go
   w.Header().Set("Content-Type", "application/json")
   w.WriteHeader(http.StatusOK)
   w.Write(data)
   ```

5. **Use context for cancellation**
   ```go
   ctx := r.Context()
   select {
   case <-ctx.Done():
       return
   case result := <-work():
       // process
   }
   ```

6. **Validate input**
   ```go
   if r.Method != http.MethodPost {
       http.Error(w, "Method not allowed", http.StatusMethodNotAllowed)
       return
   }
   ```

7. **Use proper status codes**
   ```go
   w.WriteHeader(http.StatusCreated)     // 201 for created
   w.WriteHeader(http.StatusNoContent)   // 204 for deleted
   w.WriteHeader(http.StatusNotFound)    // 404 for not found
   ```

### ❌ DON'T

1. **Don't use DefaultServeMux in production**
   ```go
   // Bad
   http.ListenAndServe(":8080", nil)
   ```

2. **Don't forget to close bodies**
   ```go
   // Bad
   resp, _ := http.Get(url)
   // Missing: defer resp.Body.Close()
   ```

3. **Don't set headers after writing**
   ```go
   // Bad
   w.Write([]byte("content"))
   w.Header().Set("Content-Type", "text/plain") // Too late!
   ```

4. **Don't read body multiple times**
   ```go
   // Bad
   body1, _ := io.ReadAll(r.Body)
   body2, _ := io.ReadAll(r.Body) // Empty! Body already read
   ```

5. **Don't ignore errors**
   ```go
   // Bad
   http.Get(url) // Ignoring error and response
   ```

6. **Don't panic in handlers**
   ```go
   // Bad
   func handler(w http.ResponseWriter, r *http.Request) {
       panic("something went wrong")
   }
   
   // Good
   func handler(w http.ResponseWriter, r *http.Request) {
       if err := doSomething(); err != nil {
           http.Error(w, err.Error(), http.StatusInternalServerError)
           return
       }
   }
   ```

---

## Troubleshooting

### "Connection reset by peer"

**Cause:** Not reading response body before closing connection.

**Solution:**
```go
resp, err := client.Get(url)
if err != nil {
    return err
}
defer func() {
    io.Copy(io.Discard, resp.Body)
    resp.Body.Close()
}()
```

### "Too many open files"

**Cause:** Not closing response bodies.

**Solution:** Always `defer resp.Body.Close()`

### "Address already in use"

**Cause:** Port already bound by another process.

**Solution:**
```bash
# Find process using port
lsof -i :8080

# Kill process
kill -9 <PID>
```

### Headers not being set

**Cause:** Setting headers after `Write()` or `WriteHeader()`.

**Solution:** Set headers first:
```go
w.Header().Set("Content-Type", "application/json") // First
w.WriteHeader(http.StatusOK)                       // Second
w.Write(data)                                       // Third
```

### Request body is empty

**Cause:** Body already read elsewhere (e.g., in middleware).

**Solution:** Store body in context or use `io.TeeReader`:
```go
var buf bytes.Buffer
tee := io.TeeReader(r.Body, &buf)
io.ReadAll(tee)
r.Body = io.NopCloser(&buf) // Restore for next handler
```

### Timeouts not working

**Cause:** Using `DefaultClient` without timeout.

**Solution:**
```go
client := &http.Client{
    Timeout: 30 * time.Second,
}
```

### Concurrent map writes panic

**Cause:** Modifying shared data structure without synchronization.

**Solution:** Use `sync.RWMutex`:
```go
type SafeMap struct {
    mu   sync.RWMutex
    data map[string]string
}

func (m *SafeMap) Set(key, value string) {
    m.mu.Lock()
    defer m.mu.Unlock()
    m.data[key] = value
}

func (m *SafeMap) Get(key string) string {
    m.mu.RLock()
    defer m.mu.RUnlock()
    return m.data[key]
}
```

---

## Quick Reference

### Server

```go
// Simple
http.ListenAndServe(":8080", handler)

// With config
server := &http.Server{
    Addr:         ":8080",
    Handler:      mux,
    ReadTimeout:  10 * time.Second,
    WriteTimeout: 10 * time.Second,
}
server.ListenAndServe()
```

### Client

```go
// Simple GET
resp, err := http.Get(url)
defer resp.Body.Close()

// Custom request
req, _ := http.NewRequest("POST", url, body)
req.Header.Set("Content-Type", "application/json")
client := &http.Client{Timeout: 10 * time.Second}
resp, err := client.Do(req)
```

### Handlers

```go
// Function
mux.HandleFunc("/path", func(w http.ResponseWriter, r *http.Request) {})

// Method-specific (Go 1.22+)
mux.HandleFunc("GET /users", listUsers)
mux.HandleFunc("POST /users", createUser)

// Path variables (Go 1.22+)
mux.HandleFunc("/users/{id}", func(w http.ResponseWriter, r *http.Request) {
    id := r.PathValue("id")
})
```

### Request

```go
r.Method                        // HTTP method
r.URL.Path                      // URL path
r.URL.Query().Get("key")       // Query parameter
r.FormValue("key")             // Form value
r.Header.Get("Key")            // Header
r.Cookie("name")               // Cookie
r.PathValue("id")              // Path variable (Go 1.22+)
json.NewDecoder(r.Body).Decode(&v)  // JSON body
```

### Response

```go
w.Header().Set("Key", "value") // Set header
w.WriteHeader(status)          // Status code
w.Write([]byte("text"))       // Write bytes
fmt.Fprintf(w, "text")        // Write string
json.NewEncoder(w).Encode(v)  // JSON response
http.Error(w, "msg", status)  // Error response
http.Redirect(w, r, url, code) // Redirect
```

---

## Further Reading

**Official Documentation:**
- https://pkg.go.dev/net/http
- https://go.dev/doc/articles/wiki/
- https://go.dev/blog/http-tracing

**Related Packages:**
- `net/http/httptest` - HTTP testing utilities
- `net/http/httptrace` - HTTP tracing
- `net/http/httputil` - HTTP utility functions
- `net/http/cookiejar` - Cookie jar implementation
- `html/template` - HTML template engine
- `encoding/json` - JSON encoding/decoding
- `context` - Request context

**Standards:**
- RFC 7230: HTTP/1.1 Message Syntax and Routing
- RFC 7231: HTTP/1.1 Semantics and Content
- RFC 7540: HTTP/2

---

**Last Updated:** December 30, 2025  
**Go Version:** 1.19+ (Compatible with 1.25.5)
