# Project 20: Distributed Cache System

[← Back to Advanced Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a Redis-like distributed cache with replication, sharding, and persistence. Learn distributed data structures, consistent hashing, and cache coherence.

**Difficulty:** Advanced  
**Estimated Time:** 60-90 hours  
**Prerequisites:** Understanding of Redis, networking, concurrency

## What You'll Learn

- In-memory data structures (string, list, hash, set, sorted set)
- RESP protocol (Redis Serialization Protocol)
- Consistent hashing for sharding
- Replication (master-slave)
- Persistence (RDB snapshots, AOF logs)
- Pub/sub messaging
- Cluster mode
- Eviction policies (LRU, LFU)

## Core Features

1. **Data Types:**
   - String: GET, SET, INCR, DECR
   - List: LPUSH, RPUSH, LPOP, RPOP, LRANGE
   - Hash: HSET, HGET, HDEL, HGETALL
   - Set: SADD, SREM, SMEMBERS, SINTER
   - Sorted Set: ZADD, ZRANGE, ZRANK

2. **Persistence:**
   - RDB: Periodic snapshots
   - AOF: Append-only log
   - Hybrid: RDB + AOF

3. **Replication:**
   - Master-slave replication
   - Full sync + incremental
   - Read replicas

4. **Clustering:**
   - Consistent hashing
   - 16384 hash slots
   - Automatic resharding
   - Gossip protocol

## Implementation Guide

```go
type Cache struct {
    data   map[string]interface{}
    mu     sync.RWMutex
    ttl    map[string]time.Time
}

func (c *Cache) Set(key string, value interface{}, ttl time.Duration) {
    c.mu.Lock()
    defer c.mu.Unlock()
    
    c.data[key] = value
    if ttl > 0 {
        c.ttl[key] = time.Now().Add(ttl)
    }
}

func (c *Cache) Get(key string) (interface{}, bool) {
    c.mu.RLock()
    defer c.mu.RUnlock()
    
    // Check expiration
    if expiry, ok := c.ttl[key]; ok {
        if time.Now().After(expiry) {
            delete(c.data, key)
            delete(c.ttl, key)
            return nil, false
        }
    }
    
    val, ok := c.data[key]
    return val, ok
}
```

## Project Structure

```
distributed-cache/
├── main.go
├── cache/
│   ├── cache.go          # Core cache
│   ├── string.go         # String operations
│   ├── list.go           # List operations
│   ├── hash.go           # Hash operations
│   └── set.go            # Set operations
├── protocol/
│   └── resp.go           # RESP protocol
├── persistence/
│   ├── rdb.go            # Snapshots
│   └── aof.go            # Append-only log
├── cluster/
│   ├── shard.go          # Consistent hashing
│   ├── node.go           # Cluster node
│   └── gossip.go         # Gossip protocol
└── replication/
    ├── master.go
    └── slave.go
```

## Full Details

Complete implementation in `golang-learning-projects.md` (search "Project 20" or around line 7500-8500):
- RESP protocol implementation
- All data structure operations
- Replication setup
- Cluster configuration
- Client library

---

[← Back to Advanced Projects](README.md) | [↑ Back to Index](../../projects-index.md)
