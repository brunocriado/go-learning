# Project 8: WebSocket Real-Time Chat

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a real-time chat application using WebSocket connections. Learn bidirectional communication, connection management, message broadcasting, and building scalable real-time systems.

**Difficulty:** Intermediate  
**Estimated Time:** 15-20 hours  
**Category:** Network Programming, Real-Time Systems

## Prerequisites

Before starting, you should have:
- Completed [Project 7: REST API with Authentication](project-07-rest-api.md)
- Understanding of HTTP upgrade mechanism
- Familiarity with concurrency (goroutines, channels)

**Required Packages:**
```bash
go get github.com/gorilla/websocket
```

## What You'll Learn

- WebSocket protocol and upgrade mechanism
- Managing concurrent connections
- Message broadcasting patterns
- Connection lifecycle management
- Heartbeat/ping-pong for connection health
- Handling connection drops
- Chat room management
- User presence tracking

## Core Features

### 1. WebSocket Server
- HTTP to WebSocket upgrade
- Connection registry
- Message routing
- Graceful disconnection
- Error handling

### 2. Chat Functionality
- One-on-one messaging
- Group chat rooms
- Broadcast messages
- User join/leave notifications
- Typing indicators
- Message history

### 3. Connection Management
- Connection pooling
- Heartbeat mechanism
- Automatic reconnection
- Connection limits
- Idle timeout

### 4. User Features
- User authentication
- Online status
- User list
- Private messages
- Room creation

## Implementation Guide

### Basic WebSocket Server

```go
package main

import (
    "github.com/gorilla/websocket"
    "log"
    "net/http"
    "sync"
)

var upgrader = websocket.Upgrader{
    ReadBufferSize:  1024,
    WriteBufferSize: 1024,
    CheckOrigin: func(r *http.Request) bool {
        return true // Configure properly in production
    },
}

type Client struct {
    hub  *Hub
    conn *websocket.Conn
    send chan []byte
    username string
    room string
}

type Hub struct {
    clients    map[*Client]bool
    broadcast  chan []byte
    register   chan *Client
    unregister chan *Client
    mu         sync.RWMutex
}

func newHub() *Hub {
    return &Hub{
        broadcast:  make(chan []byte),
        register:   make(chan *Client),
        unregister: make(chan *Client),
        clients:    make(map[*Client]bool),
    }
}

func (h *Hub) run() {
    for {
        select {
        case client := <-h.register:
            h.mu.Lock()
            h.clients[client] = true
            h.mu.Unlock()
            
        case client := <-h.unregister:
            h.mu.Lock()
            if _, ok := h.clients[client]; ok {
                delete(h.clients, client)
                close(client.send)
            }
            h.mu.Unlock()
            
        case message := <-h.broadcast:
            h.mu.RLock()
            for client := range h.clients {
                select {
                case client.send <- message:
                default:
                    close(client.send)
                    delete(h.clients, client)
                }
            }
            h.mu.RUnlock()
        }
    }
}

func (c *Client) readPump() {
    defer func() {
        c.hub.unregister <- c
        c.conn.Close()
    }()
    
    for {
        _, message, err := c.conn.ReadMessage()
        if err != nil {
            break
        }
        c.hub.broadcast <- message
    }
}

func (c *Client) writePump() {
    defer c.conn.Close()
    
    for message := range c.send {
        w, err := c.conn.NextWriter(websocket.TextMessage)
        if err != nil {
            return
        }
        w.Write(message)
        w.Close()
    }
}

func serveWs(hub *Hub, w http.ResponseWriter, r *http.Request) {
    conn, err := upgrader.Upgrade(w, r, nil)
    if err != nil {
        log.Println(err)
        return
    }
    
    client := &Client{hub: hub, conn: conn, send: make(chan []byte, 256)}
    client.hub.register <- client
    
    go client.writePump()
    go client.readPump()
}

func main() {
    hub := newHub()
    go hub.run()
    
    http.HandleFunc("/ws", func(w http.ResponseWriter, r *http.Request) {
        serveWs(hub, w, r)
    })
    
    log.Fatal(http.ListenAndServe(":8080", nil))
}
```

## Project Structure

```
websocket-chat/
├── main.go
├── hub.go              # Connection hub/manager
├── client.go           # WebSocket client
├── message.go          # Message types
├── room.go             # Chat room management
├── auth.go             # User authentication
├── static/
│   ├── index.html
│   ├── chat.js
│   └── style.css
└── README.md
```

## Testing Strategy

### Unit Tests
- Message routing logic
- Room management
- User authentication

### Integration Tests
- WebSocket connection handling
- Message broadcasting
- Connection lifecycle

### Load Tests
- 1000+ concurrent connections
- Message throughput
- Memory usage under load

## Challenges & Solutions

### Challenge 1: Connection Management
**Problem:** How to track active connections efficiently?  
**Solution:** Use a map with mutex protection, register/unregister channels

### Challenge 2: Message Ordering
**Problem:** Guarantee message ordering per user  
**Solution:** Use buffered channels per client, single writer goroutine

### Challenge 3: Graceful Shutdown
**Problem:** Close all connections cleanly  
**Solution:** Signal pattern with context, drain send channels before closing

## Next Steps

After completing this project:
1. Add Redis for horizontal scaling
2. Implement message persistence
3. Add file sharing
4. Create video chat with WebRTC
5. Move to [Project 9: File Sync Tool](project-09-file-sync.md)

## Resources

- [Gorilla WebSocket Documentation](https://github.com/gorilla/websocket)
- [WebSocket RFC 6455](https://tools.ietf.org/html/rfc6455)
- [Real-Time Web Apps](https://www.oreilly.com/library/view/high-performance-browser/9781449344757/)

---

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)
