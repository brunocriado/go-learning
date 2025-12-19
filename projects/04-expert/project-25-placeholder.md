# Project 25: Distributed Cache & Rate Limiter

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a distributed caching system with eviction policies and production-ready rate limiter with multiple algorithms.

**Difficulty:** Expert  
**Estimated Time:** 4-5 weeks  
**Prerequisites:** Redis project, understanding of caching concepts, concurrent programming

## What You'll Learn

- LRU, LFU, FIFO eviction policies
- Distributed cache consistency
- Cache stampede prevention
- Rate limiting algorithms
- Token bucket implementation
- Sliding window counters
- Distributed rate limiting

## Core Features

1. **Cache Implementation:**
   - In-memory cache with eviction
   - LRU (Least Recently Used)
   - LFU (Least Frequently Used)
   - TTL-based expiration
   - Size-based eviction
   - Thread-safe operations

2. **Distributed Cache:**
   - Consistent hashing
   - Sharding strategy
   - Replication
   - Cache coherence
   - Redis cluster integration

3. **Rate Limiter:**
   - Token bucket algorithm
   - Leaky bucket algorithm
   - Fixed window counter
   - Sliding window counter
   - Distributed rate limiting (Redis)

4. **Cache Patterns:**
   - Cache-aside
   - Read-through
   - Write-through
   - Write-behind
   - Refresh-ahead

## LRU Cache Implementation

```go
type LRUCache struct {
    capacity int
    cache    map[string]*list.Element
    list     *list.List
    mu       sync.RWMutex
}

type entry struct {
    key   string
    value interface{}
}

func (c *LRUCache) Get(key string) (interface{}, bool) {
    c.mu.Lock()
    defer c.mu.Unlock()
    
    if elem, ok := c.cache[key]; ok {
        c.list.MoveToFront(elem)
        return elem.Value.(*entry).value, true
    }
    return nil, false
}

func (c *LRUCache) Put(key string, value interface{}) {
    c.mu.Lock()
    defer c.mu.Unlock()
    
    if elem, ok := c.cache[key]; ok {
        c.list.MoveToFront(elem)
        elem.Value.(*entry).value = value
        return
    }
    
    if c.list.Len() >= c.capacity {
        // Evict LRU
        oldest := c.list.Back()
        c.list.Remove(oldest)
        delete(c.cache, oldest.Value.(*entry).key)
    }
    
    elem := c.list.PushFront(&entry{key, value})
    c.cache[key] = elem
}
```

## Token Bucket Rate Limiter

```go
type TokenBucket struct {
    capacity   int
    tokens     int
    refillRate time.Duration
    lastRefill time.Time
    mu         sync.Mutex
}

func (tb *TokenBucket) Allow() bool {
    tb.mu.Lock()
    defer tb.mu.Unlock()
    
    // Refill tokens
    now := time.Now()
    elapsed := now.Sub(tb.lastRefill)
    tokensToAdd := int(elapsed / tb.refillRate)
    
    if tokensToAdd > 0 {
        tb.tokens = min(tb.capacity, tb.tokens + tokensToAdd)
        tb.lastRefill = now
    }
    
    if tb.tokens > 0 {
        tb.tokens--
        return true
    }
    return false
}
```

## Sliding Window Rate Limiter (Redis)

```go
func (rl *RateLimiter) AllowRedis(key string, limit int, window time.Duration) bool {
    now := time.Now().UnixNano()
    windowStart := now - window.Nanoseconds()
    
    pipe := rl.redis.Pipeline()
    
    // Remove old entries
    pipe.ZRemRangeByScore(ctx, key, "0", fmt.Sprint(windowStart))
    
    // Count entries in window
    pipe.ZCard(ctx, key)
    
    // Add current request
    pipe.ZAdd(ctx, key, &redis.Z{Score: float64(now), Member: now})
    
    // Set expiry
    pipe.Expire(ctx, key, window)
    
    results, _ := pipe.Exec(ctx)
    count := results[1].(*redis.IntCmd).Val()
    
    return count < int64(limit)
}
```

## Project Structure

```
distributed-cache/
├── cache/
│   ├── lru.go            # LRU cache
│   ├── lfu.go            # LFU cache
│   ├── ttl.go            # TTL cache
│   └── distributed.go    # Distributed cache
├── ratelimit/
│   ├── token_bucket.go
│   ├── leaky_bucket.go
│   ├── fixed_window.go
│   ├── sliding_window.go
│   └── distributed.go    # Redis-based
├── consistent/
│   └── hash.go           # Consistent hashing
└── examples/
    └── api/              # API with rate limiting
```

## Cache Strategies

**Cache-Aside:**
- Application manages cache
- Read: Check cache → if miss, load from DB → update cache
- Write: Update DB → invalidate cache

**Write-Through:**
- Write to cache and DB together
- Ensures consistency
- Higher write latency

**Write-Behind:**
- Write to cache immediately
- Async write to DB
- Better performance
- Risk of data loss

## Full Details

Complete implementation in `golang-learning-projects.md` (search "Project 25"):
- All eviction policies with code
- Consistent hashing implementation
- All rate limiting algorithms
- Distributed cache setup
- Redis integration
- Performance benchmarks

---

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)
