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

## 📋 Task Checklist

Use this checklist to guide your implementation. Check off tasks as you complete them. **Remember**: These are guidance tasks, not solutions. Research and figure out the implementation details yourself.

### Phase 1: Project Setup & Foundation
- [x] **Task 1.1**: Create project directory and initialize Go module
- [x] **Task 1.2**: Create empty files: `main.go`, `shortener.go`, `handlers.go`
- [x] **Task 1.3**: Create `templates/` directory for HTML files
- [x] **Task 1.4**: Research the `net/http` package - how does Go handle HTTP?
- [x] **Task 1.5**: Research Go maps - syntax, initialization, and operations
- [x] **Task 1.6**: Research `sync.RWMutex` - why do we need thread safety?
- [x] **Task 1.7**: Understand the difference between `Lock()` and `RLock()`

### Phase 2: Core Data Structures (`shortener.go`)
- [x] **Task 2.1**: Define `URLData` struct with all fields (ID, OriginalURL, ShortCode, Clicks, CreatedAt)
- [x] **Task 2.2**: Add JSON tags to each field for API responses
- [x] **Task 2.3**: Define `URLShortener` struct with map and mutex
- [x] **Task 2.4**: Research map initialization - what's the zero value? How to initialize?
- [x] **Task 2.5**: Implement `NewURLShortener()` constructor function
- [x] **Task 2.6**: Test map operations manually - insert, lookup, delete
- [x] **Task 2.7**: Research hash functions - what's MD5? How to use `crypto/md5`?
- [x] **Task 2.8**: Implement `generateShortCode()` - hash URL and convert to short string
- [x] **Task 2.9**: Research Base62 encoding - why use it for short codes?
- [x] **Task 2.10**: Implement `base62Encode()` - convert number to alphanumeric string
- [x] **Task 2.11**: Test short code generation - are codes unique? URL-safe?
- [x] **Task 2.12**: Implement `Shorten()` method with mutex locking
- [x] **Task 2.13**: Handle collision case - what if short code already exists?
- [x] **Task 2.14**: Implement `Resolve()` method with read lock
- [x] **Task 2.15**: What should `Resolve()` return if short code doesn't exist?
- [x] **Task 2.16**: Implement `IncrementClick()` - how to safely update counter?
- [x] **Task 2.17**: Implement `GetStats()` method to return URL data
- [x] **Task 2.18**: Implement `GetAll()` method - how to convert map to slice?
- [x] **Task 2.19**: Test all methods with sample data

### Phase 3: HTTP Request/Response Structures (`handlers.go`)
- [x] **Task 3.1**: Define `ShortenRequest` struct with URL field
- [x] **Task 3.2**: Define `ShortenResponse` struct with ShortCode and ShortURL
- [x] **Task 3.3**: Define `ErrorResponse` struct for error messages
- [x] **Task 3.4**: Research `http.ResponseWriter` - what methods does it have?
- [x] **Task 3.5**: Research `*http.Request` - how to access body, method, headers?
- [x] **Task 3.6**: Implement `respondWithJSON()` helper function
- [x] **Task 3.7**: What headers need to be set for JSON responses?
- [x] **Task 3.8**: Implement `respondWithError()` helper function
- [x] **Task 3.9**: Test JSON encoding manually with sample data

### Phase 4: HTTP Handlers Implementation (`handlers.go`)
- [x] **Task 4.1**: Implement `shortenHandler()` - parse POST request body
- [x] **Task 4.2**: How to decode JSON from `r.Body`? Research `json.NewDecoder`
- [x] **Task 4.3**: Validate the incoming URL - is it empty? Valid format?
- [x] **Task 4.4**: Research URL validation - `strings.HasPrefix()` or regex?
- [x] **Task 4.5**: Call `Shorten()` and construct response with full short URL
- [x] **Task 4.6**: How to build the full short URL? Combine host + path + shortCode
- [x] **Task 4.7**: Handle errors in `shortenHandler` - what status codes to return?
- [x] **Task 4.8**: Implement `redirectHandler()` - extract short code from URL path
- [x] **Task 4.9**: Research `http.Redirect()` - what status code for permanent redirect?
- [x] **Task 4.10**: What to do if short code doesn't exist in `redirectHandler`?
- [x] **Task 4.11**: Call `IncrementClick()` before redirecting
- [x] **Task 4.12**: Implement `statsHandler()` - return URLData as JSON
- [x] **Task 4.13**: Implement `listHandler()` - return all URLs as JSON array
- [x] **Task 4.14**: Implement `homeHandler()` - serve HTML file
- [x] **Task 4.15**: Research `http.ServeFile()` vs `html/template` package
- [x] **Task 4.16**: Handle HTTP method validation - reject wrong methods gracefully

### Phase 5: HTML Frontend (`templates/index.html`)
- [x] **Task 5.1**: Create basic HTML structure with form
- [x] **Task 5.2**: Add input field for URL with proper type and validation
- [x] **Task 5.3**: Add submit button
- [x] **Task 5.4**: Add div to display results
- [x] **Task 5.5**: Research JavaScript `fetch()` API for making HTTP requests
- [x] **Task 5.6**: Implement form submission with `preventDefault()`
- [x] **Task 5.7**: Send POST request to `/api/shorten` with JSON body
- [x] **Task 5.8**: Parse JSON response and display short URL
- [x] **Task 5.9**: Handle and display errors from API
- [x] **Task 5.10**: Add "Copy to Clipboard" button functionality
- [x] **Task 5.11**: Research `navigator.clipboard.writeText()` API
- [x] **Task 5.12**: Add basic CSS styling for better UX
- [x] **Task 5.13**: Make URL input clickable (link) in result display

### Phase 6: Server Setup & Routing (`main.go`)
- [x] **Task 6.1**: Research `http.ServeMux` - what is a router?
- [x] **Task 6.2**: Create `URLShortener` instance in main()
- [x] **Task 6.3**: Create `http.ServeMux` for routing
- [x] **Task 6.4**: Register route: `/` -> homeHandler
- [x] **Task 6.5**: Register route: `/api/shorten` -> shortenHandler
- [x] **Task 6.6**: Register route: `/api/list` -> listHandler
- [x] **Task 6.7**: Register route: `/s/` -> redirectHandler (prefix match)
- [x] **Task 6.8**: Register route: `/stats/` -> statsHandler
- [x] **Task 6.9**: Research how `HandleFunc()` works - method vs function
- [x] **Task 6.10**: How to pass methods as handler functions?
- [x] **Task 6.11**: Implement `loggingMiddleware()` wrapper function
- [x] **Task 6.12**: Research middleware pattern - how to wrap handlers?
- [x] **Task 6.13**: Log each request: method, path, duration
- [x] **Task 6.14**: Research `time.Since()` for measuring request duration
- [x] **Task 6.15**: Start server with `http.ListenAndServe()`
- [x] **Task 6.16**: What happens if server fails to start? Handle error

### Phase 7: Testing & Debugging
- [ ] **Task 7.1**: Build the project - fix any compilation errors
- [ ] **Task 7.2**: Start the server - does it listen on port 8080?
- [ ] **Task 7.3**: Test accessing `http://localhost:8080` in browser
- [ ] **Task 7.4**: Does the HTML form load correctly?
- [ ] **Task 7.5**: Test shortening a URL through the web interface
- [ ] **Task 7.6**: Does the short URL display correctly?
- [ ] **Task 7.7**: Click the short URL - does it redirect?
- [ ] **Task 7.8**: Test with curl: POST to `/api/shorten`
- [ ] **Task 7.9**: Verify JSON response format matches expected structure
- [ ] **Task 7.10**: Test redirect with curl: `curl -L http://localhost:8080/s/...`
- [ ] **Task 7.11**: Test stats endpoint - do clicks increment?
- [ ] **Task 7.12**: Test list endpoint - does it show all URLs?
- [ ] **Task 7.13**: Test edge cases: empty URL, invalid URL, malformed JSON
- [ ] **Task 7.14**: Test non-existent short code - does it return 404?
- [ ] **Task 7.15**: Test wrong HTTP methods - are they rejected?
- [ ] **Task 7.16**: Check server logs - are requests being logged?
- [ ] **Task 7.17**: Test concurrent requests - use multiple browser tabs
- [ ] **Task 7.18**: Verify thread safety - no race conditions with `go run -race .`

### Phase 8: Refinement & Polish
- [ ] **Task 8.1**: Add input validation error messages in HTML
- [ ] **Task 8.2**: Improve CSS styling for better visual appeal
- [ ] **Task 8.3**: Add loading spinner during API calls
- [ ] **Task 8.4**: Add success/error notifications (toast messages)
- [ ] **Task 8.5**: Make short codes more visually distinct (better encoding)
- [ ] **Task 8.6**: Add URL validation on backend (check format, not just empty)
- [ ] **Task 8.7**: Return meaningful HTTP status codes for all error cases
- [ ] **Task 8.8**: Add CORS headers if testing from different origins
- [ ] **Task 8.9**: Test with very long URLs - do they work?
- [ ] **Task 8.10**: Add comments explaining complex logic

### Bonus Challenges (Optional)
- [ ] **Bonus 1**: Implement custom short codes (user-specified)
- [ ] **Bonus 2**: Add expiration time for URLs
- [ ] **Bonus 3**: Persist data to JSON file (save/load on startup/shutdown)
- [ ] **Bonus 4**: Generate QR codes for short URLs
- [ ] **Bonus 5**: Add analytics dashboard showing top URLs
- [ ] **Bonus 6**: Implement URL validation by checking if URL is reachable
- [ ] **Bonus 7**: Add rate limiting to prevent abuse
- [ ] **Bonus 8**: Use a database (SQLite or PostgreSQL) instead of in-memory map
- [ ] **Bonus 9**: Add user authentication for private URLs
- [ ] **Bonus 10**: Deploy to cloud (Heroku, Railway, Fly.io)

---

## 🤔 Debugging Questions to Ask Yourself

**HTTP & Web Concepts:**
- What's the difference between GET and POST requests?
- Why use JSON instead of plain text for API responses?
- What HTTP status code should you return for "not found"?
- How does an HTTP redirect work under the hood?

**Concurrency & Thread Safety:**
- Why isn't a Go map thread-safe by default?
- When should you use `RLock()` vs `Lock()`?
- What happens if you forget to unlock a mutex?
- How does `defer` help with mutex unlocking?

**Maps & Data Structures:**
- What's the zero value of a map? Can you use it?
- How do you check if a key exists in a map?
- Can map keys be any type, or only certain types?
- What's the difference between `map[string]int` and `map[string]*int`?

**URL Shortening Logic:**
- Why hash URLs instead of just using a counter?
- What makes a good short code (length, characters)?
- How do you handle collisions in short codes?
- Why use Base62 instead of Base64 for short codes?

**Error Handling:**
- What errors can occur when decoding JSON?
- How should you respond to invalid input?
- What if the same URL is shortened twice?
- Should incrementing clicks fail if the short code doesn't exist?

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
