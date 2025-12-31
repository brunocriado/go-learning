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

### Client-Server Model

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

### The Handler Interface

The fundamental abstraction in `net/http`:

```go
type Handler interface {
    ServeHTTP(ResponseWriter, *Request)
}
```

**Everything** that processes HTTP requests must implement this interface.

### The HandlerFunc Adapter

```go
type HandlerFunc func(ResponseWriter, *Request)

func (f HandlerFunc) ServeHTTP(w ResponseWriter, r *Request) {
    f(w, r)
}
```

This allows ordinary functions to act as Handlers.

### The Three Core Types

1. **Handler** - Processes requests
2. **Request** - Incoming HTTP request data
3. **ResponseWriter** - Interface to construct responses

---

## HTTP Server Architecture

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

**Server Fields:**

| Field | Type | Purpose |
|-------|------|---------|
| `Addr` | `string` | TCP address to listen on |
| `Handler` | `Handler` | Request handler (nil = DefaultServeMux) |
| `ReadTimeout` | `Duration` | Maximum time to read request |
| `WriteTimeout` | `Duration` | Maximum time to write response |
| `IdleTimeout` | `Duration` | Keep-alive timeout |
| `MaxHeaderBytes` | `int` | Max bytes for request headers |
| `TLSConfig` | `*tls.Config` | TLS configuration |
| `ErrorLog` | `*log.Logger` | Error logger |

### Multiple Servers

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

---

## HTTP Client Architecture

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

### The Default Client

```go
var DefaultClient = &Client{}
```

Functions `http.Get`, `http.Post`, etc., use `DefaultClient`.

**DefaultClient limitations:**
- No timeout (requests can hang forever)
- Uses DefaultTransport with connection pooling
- Follows redirects (max 10)

### Custom Client

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

| Field | Type | Purpose |
|-------|------|---------|
| `Transport` | `RoundTripper` | HTTP transport mechanism |
| `CheckRedirect` | `func` | Redirect policy |
| `Jar` | `CookieJar` | Cookie storage |
| `Timeout` | `Duration` | Total timeout (dial + request + response) |

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
