# Project 9: Distributed File Sync Tool

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a Dropbox-like file synchronization tool. Learn file watching, conflict resolution, efficient file transfer, and distributed state management.

**Difficulty:** Intermediate  
**Estimated Time:** 45-70 hours  
**Category:** Systems Programming, Distributed Systems

## Prerequisites

- Completed [Project 3: Automated File Organizer](../01-basic/project-03-file-organizer.md)
- Understanding of file systems
- Network programming basics

**Required Packages:**
```bash
go get github.com/fsnotify/fsnotify
go get github.com/zeebo/blake3
```

## What You'll Learn

- File system monitoring with fsnotify
- Efficient file transfer (rsync algorithm, chunking)
- Conflict resolution strategies
- File versioning and snapshots
- Hash-based deduplication
- Network protocols for file sync
- Handling large files

## Core Features

### 1. File Watching
- Monitor directory changes
- Detect file create/modify/delete
- Recursive watching
- Ignore patterns (.gitignore style)
- Efficient event batching

### 2. File Transfer
- Chunked transfer for large files
- Delta sync (only changed parts)
- Compression
- Resume capability
- Bandwidth throttling

### 3. Conflict Resolution
- Last-write-wins
- Three-way merge for text files
- Conflict copies (file_conflict_2024.txt)
- Manual resolution UI
- Version history

### 4. Synchronization
- Bidirectional sync
- Selective sync
- Pause/resume
- Offline changes queue
- Background sync

## Implementation Guide

### File Watcher

```go
package main

import (
    "github.com/fsnotify/fsnotify"
    "log"
    "path/filepath"
)

type FileWatcher struct {
    watcher   *fsnotify.Watcher
    rootPath  string
    onChange  chan FileChange
}

type FileChange struct {
    Path      string
    Operation string // create, modify, delete
    Timestamp time.Time
}

func NewFileWatcher(path string) (*FileWatcher, error) {
    watcher, err := fsnotify.NewWatcher()
    if err != nil {
        return nil, err
    }
    
    fw := &FileWatcher{
        watcher:  watcher,
        rootPath: path,
        onChange: make(chan FileChange, 100),
    }
    
    return fw, nil
}

func (fw *FileWatcher) Start() error {
    // Add root and subdirectories
    err := filepath.Walk(fw.rootPath, func(path string, info os.FileInfo, err error) error {
        if info.IsDir() {
            return fw.watcher.Add(path)
        }
        return nil
    })
    
    if err != nil {
        return err
    }
    
    go fw.handleEvents()
    return nil
}

func (fw *FileWatcher) handleEvents() {
    for {
        select {
        case event := <-fw.watcher.Events:
            fw.onChange <- FileChange{
                Path:      event.Name,
                Operation: event.Op.String(),
                Timestamp: time.Now(),
            }
            
        case err := <-fw.watcher.Errors:
            log.Println("Watcher error:", err)
        }
    }
}
```

### File Hasher

```go
import "github.com/zeebo/blake3"

func HashFile(path string) (string, error) {
    file, err := os.Open(path)
    if err != nil {
        return "", err
    }
    defer file.Close()
    
    hasher := blake3.New()
    if _, err := io.Copy(hasher, file); err != nil {
        return "", err
    }
    
    return hex.EncodeToString(hasher.Sum(nil)), nil
}
```

## Project Structure

```
file-sync/
├── main.go
├── watcher/
│   └── watcher.go
├── sync/
│   ├── engine.go
│   ├── conflict.go
│   └── delta.go
├── network/
│   ├── client.go
│   └── server.go
├── storage/
│   ├── metadata.go
│   └── versions.go
└── README.md
```

## Challenges & Solutions

### Challenge 1: Circular Syncs
**Problem:** Changes trigger more changes  
**Solution:** Ignore self-triggered events, use event IDs

### Challenge 2: Large Files
**Problem:** Memory issues with huge files  
**Solution:** Chunked reading, streaming transfer

### Challenge 3: Network Failures
**Problem:** Incomplete transfers  
**Solution:** Resume capability, checksums per chunk

## Next Steps

- Add end-to-end encryption
- Implement LAN sync (no server)
- Create mobile app
- Move to [Project 10: Web Scraper](project-10-web-scraper.md)

## Resources

- [fsnotify Documentation](https://github.com/fsnotify/fsnotify)
- [rsync Algorithm](https://rsync.samba.org/tech_report/)
- [Dropbox Engineering Blog](https://dropbox.tech/)

---

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)
