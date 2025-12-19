# Project 2: URL Shortener Service

[← Back to Basic Projects](README.md) | [↑ Back to Index](../../projects-index.md)

---

## Prerequisites & Requirements

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

---

## Overview

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

---

## Project Structure

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

---

## Implementation Guide

### Step 1: Initialize Project

```bash
mkdir url-shortener
cd url-shortener
go mod init github.com/yourusername/url-shortener
```

### Step 2: Core Data Structures (`shortener.go`)

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

### Step 3: HTTP Handlers (`handlers.go`)

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

### Step 4: HTML Template (`templates/index.html`)

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
- Clean, modern UI with CSS
- Input field for URL
- Button to shorten
- Display area for result
- Copy to clipboard button

### Step 5: Main Server (`main.go`)

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

### Step 6: Run the Server

```bash
# Create templates directory
mkdir templates

# Copy the HTML template to templates/index.html

# Run the server
go run .

# Test with curl
curl -X POST http://localhost:8080/api/shorten \
  -H "Content-Type: application/json" \
  -d '{"url":"https://www.golang.org/doc/"}'

# Or open http://localhost:8080 in your browser
```

---

## Testing the API

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

---

## Enhancement Ideas

1. **Custom Short Codes**: Allow users to specify their own short codes
2. **Expiration**: Auto-delete URLs after certain time
3. **QR Codes**: Generate QR codes for short URLs
4. **Analytics**: Track referrers, user agents, geographic data
5. **Authentication**: User accounts and private URLs
6. **Database**: Use PostgreSQL or Redis instead of in-memory map
7. **Rate Limiting**: Prevent abuse with request throttling
8. **URL Validation**: Check if URLs are reachable before shortening

---

## Common Gotchas & Solutions

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

## Next Steps

After completing this project, you'll be ready for:
- **Project 3**: File Organizer (more complex concurrency)
- **Project 7**: REST API with Database (production-grade web service)
- **Project 8**: WebSocket Chat (real-time communication)

---

[← Back to Basic Projects](README.md) | [↑ Back to Index](../../projects-index.md)
