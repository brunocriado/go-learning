# Project 5: Log File Analyzer & Tail

[← Back to Basic Projects](README.md) | [↑ Back to Index](../../projects-index.md)

---

## Prerequisites & Requirements

**Before Starting:**
- **Completed**: Basic projects
- **Equivalent Experience**: File I/O, string parsing

**Knowledge Prerequisites:**
- **Must Know**:
  - File reading (`os.Open`, `bufio.Scanner`)
  - Regular expressions (`regexp`)
  - String manipulation
  - Maps and slices
- **Will Learn**:
  - File tailing (`tail -f` implementation)
  - Log parsing and analysis
  - Pattern matching with regex
  - Statistics calculation
  - File watching without fsnotify

**New Go Concepts:**
1. **File Seeking**: `file.Seek()` for reading from end
2. **io.SeekEnd**: Positioning file pointer
3. **bufio.Scanner**: Efficient line reading
4. **regexp.Compile**: Pattern matching
5. **time.ParseInLayout**: Parse log timestamps

**What to Install:**
```bash
mkdir log-analyzer
cd log-analyzer
go mod init github.com/yourusername/log-analyzer

# No external dependencies needed for basic version
# Optional: regex2 for advanced regex
go get github.com/dlclark/regexp2
```

**Estimated Time:** 12-18 hours

---

## Overview

Build a log file analyzer and real-time tail utility that parses logs, extracts statistics, and follows files like `tail -f`.

### What You'll Learn

- **File Seeking**: Read from end of file
- **Log Parsing**: Extract structured data from logs
- **Regular Expressions**: Pattern matching
- **Statistics**: Count, aggregate, summarize
- **File Watching**: Detect new content without fsnotify
- **Real-time Processing**: Stream processing

### Core Features

1. Parse common log formats (Apache, nginx, JSON)
2. Extract fields (IP, timestamp, status, URL)
3. Calculate statistics (requests/sec, error rate, top IPs)
4. Filter by patterns, date range, status codes
5. Tail mode (`-f` flag) for real-time monitoring
6. Highlight errors/warnings
7. Export analysis to JSON/CSV

---

## Project Structure

```
log-analyzer/
├── main.go           # 150-200 lines
├── parser/
│   └── parser.go     # 200-300 lines
├── analyzer/
│   └── stats.go      # 150-250 lines
├── tail/
│   └── tail.go       # 150-200 lines
└── filter/
    └── filter.go     # 100-150 lines
```

---

## Implementation Guide

### Step 1: Basic File Reading

**What to create:**
```go
func ReadLogFile(path string) ([]string, error) {
    // Read entire file line by line
    // Return slice of lines
}
```

### Step 2: Log Parsing

**Key Concepts:**
- **Apache Combined Log**: `127.0.0.1 - - [01/Jan/2024:00:00:00 +0000] "GET /path HTTP/1.1" 200 1234`
- **Regex patterns** for extraction
- **Timestamp parsing**

**What to create:**
```go
type LogEntry struct {
    IP        string
    Timestamp time.Time
    Method    string
    Path      string
    Status    int
    Size      int
    UserAgent string
}

func ParseApacheLog(line string) (*LogEntry, error) {
    // Use regex to extract fields
}
```

### Step 3: Statistics

**What to calculate:**
- Total requests
- Requests per status code
- Top N IPs
- Top N URLs
- Error rate percentage
- Average response size
- Requests per hour/day

### Step 4: Tail Implementation

**Key Concepts:**
- Start reading from end of file
- Periodically check for new content
- Only read new lines

**What to create:**
```go
func TailFile(path string, follow bool) {
    file, _ := os.Open(path)
    // Seek to end
    file.Seek(0, io.SeekEnd)
    
    for {
        // Read new lines
        // If no new lines, sleep
        time.Sleep(100 * time.Millisecond)
    }
}
```

---

## Challenge Yourself

1. **Multiple Formats**: Support nginx, JSON, syslog formats
2. **GeoIP**: Lookup IP locations
3. **Alerts**: Alert on error rate thresholds
4. **Web Dashboard**: Real-time web UI
5. **Multiple Files**: Tail multiple files simultaneously
6. **Log Rotation**: Handle rotated log files
7. **Compression**: Read gzipped logs
8. **Search**: Full-text search across logs

---

## Common Gotchas

**Problem**: Memory issues with large files  
**Fix**: Read in chunks, don't load entire file into memory

**Problem**: Tail doesn't see new lines  
**Fix**: Ensure you're checking file size, handle log rotation

**Problem**: Regex performance  
**Fix**: Compile regex once, reuse; or use string operations if possible

---

[← Back to Basic Projects](README.md) | [↑ Back to Index](../../projects-index.md)
