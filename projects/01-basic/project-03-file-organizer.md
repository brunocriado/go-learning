# Project 3: File Organizer

[← Back to Basic Projects](README.md) | [↑ Back to Index](../../projects-index.md)

---

## Prerequisites & Requirements

**Before Starting:**
- **Completed**: Projects 1 & 2, or equivalent experience
- Solid understanding of:
  - Goroutines and channels
  - File system concepts (files, directories, paths)
  - Concurrent programming basics
- Comfortable with command-line operations
- Basic regex knowledge helpful (not required)

**Knowledge Prerequisites:**
- **Must Know**:
  - All concepts from Projects 1 & 2
  - Goroutines: `go func() { ... }()`
  - Channels: `make(chan type)`, `<-channel`
  - Select statements: `select { case <-ch1: ... }`
  - File operations: create, move, delete
  - Paths: absolute vs relative
- **Will Learn**:
  - File system watching with fsnotify
  - Complex concurrent patterns
  - Signal handling
  - Configuration files
  - Advanced file operations

**External Dependencies:**
- **Required**:
  - `github.com/fsnotify/fsnotify` - File system watching
- **Optional**:
  - `gopkg.in/yaml.v3` - YAML config files
  - `github.com/spf13/cobra` - Better CLI

**Estimated Time:** 12-20 hours

---

## Overview

Build a tool that watches a directory (like Downloads) and automatically organizes files into subdirectories based on file type, date, or custom rules. This teaches file system operations, path manipulation, and goroutines.

### What You'll Learn

- **filepath Package**: Cross-platform path operations
- **os Package**: File system operations (move, copy, stat)
- **File Watching**: Monitor directory for changes (using fsnotify)
- **Goroutines**: Lightweight threads for concurrent operations
- **Channels**: Communication between goroutines
- **Select Statement**: Multiplex channel operations
- **Regular Expressions**: Pattern matching for file rules
- **Configuration**: Load rules from config file (YAML/JSON)

### Core Features

1. Watch a directory for new files
2. Organize files by extension (images/, documents/, videos/, etc.)
3. Organize by date (2024/12/, 2025/01/, etc.)
4. Custom rules based on filename patterns
5. Dry-run mode to preview changes
6. Undo recent operations
7. Configuration file for custom rules

---

## Project Structure

```
file-organizer/
├── main.go           # Entry point and CLI
├── watcher.go        # File system watching
├── organizer.go      # Organization logic
├── rules.go          # Rule definitions and matching
├── config.go         # Configuration loading
├── config.yaml       # User configuration
└── go.mod
```

---

## Implementation Guide

### Step 1: Initialize and Install Dependencies

```bash
mkdir file-organizer
cd file-organizer
go mod init github.com/yourusername/file-organizer

# Install file watching library
go get github.com/fsnotify/fsnotify
```

### Step 2: Define Rules (`rules.go`)

**What you need to create:**
- `Rule` struct with fields:
  - Name (e.g., "Images")
  - Extensions (slice of strings like [".jpg", ".png"])
  - Pattern (optional regex for filename matching)
  - Destination (target folder name)
- `RuleSet` struct with Rules slice
- `DefaultRules()` function that returns common categories
- Methods on `RuleSet`:
  - `MatchRule(filename)` - Find first matching rule
  - `AddCustomRule(rule)` - Add user-defined rule

**Hints:**
- Use `filepath.Ext(filename)` to get extension
- Compare extensions case-insensitively with `strings.ToLower()`
- Return empty string and false if no match found

### Step 3: File Operations (`organizer.go`)

**What you need to create:**
- `Operation` struct for undo tracking (SourcePath, DestPath, Timestamp)
- `Organizer` struct with:
  - WatchDir, Rules, DryRun, History
- Methods:
  - `OrganizeFile(filePath)` - Main logic
  - `resolveConflict(path)` - Handle filename conflicts
  - `OrganizeAll()` - Process all files
  - `Undo(count)` - Reverse last N operations

**Learning Notes:**
- `os.Stat()`: Get file information
- `os.MkdirAll()`: Create directory and parents
- `os.Rename()`: Move/rename files
- `os.ReadDir()`: List directory contents

### Step 4: File Watching (`watcher.go`)

**What you need to create:**
- `Watcher` struct with organizer, fsnotify watcher, done channel
- Methods:
  - `Start()` - Add directory to watcher, launch event loop
  - `eventLoop()` - Runs in goroutine, listens for file events
  - `Stop()` - Clean shutdown

**Learning Notes:**
- Use `select` to multiplex channels
- On CREATE or WRITE events: organize the file
- Add debouncing (wait 500ms before processing)

### Step 5: Main Application (`main.go`)

Define command-line flags:
- `-dir`: Directory to watch
- `-dry-run`: Preview mode
- `-organize`: Run once and exit
- `-watch`: Watch continuously
- `-undo`: Undo last N operations

---

## Build and Use

```bash
# Build
go build -o file-organizer

# Organize Downloads folder once
./file-organizer -dir ~/Downloads -organize

# Preview changes (dry-run)
./file-organizer -dir ~/Downloads -organize -dry-run

# Watch directory continuously
./file-organizer -dir ~/Downloads -watch

# Undo last 3 operations
./file-organizer -dir ~/Downloads -undo 3
```

---

## Enhancement Ideas

1. **Date-based Organization**: Group by year/month
2. **Size Filters**: Handle large files differently
3. **Duplicate Detection**: Find and merge duplicate files (by hash)
4. **Cloud Sync**: Upload organized files to cloud storage
5. **GUI**: Build a desktop interface
6. **Smart Rules**: ML-based file categorization
7. **Compression**: Auto-compress old files

---

## Common Gotchas

**Problem**: Watcher triggers for own moves  
**Solution**: Track recently moved files and ignore them

**Problem**: Permission errors  
**Solution**: Check permissions before operations

**Problem**: Infinite loops with symbolic links  
**Solution**: Check for symlinks and handle appropriately

---

[← Back to Basic Projects](README.md) | [↑ Back to Index](../../projects-index.md)
