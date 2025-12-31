# Go `sync` Package: Complete Guide

A comprehensive reference for Go's `sync` package - mastering synchronization primitives, mutexes, and concurrent programming patterns.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Understanding Goroutines](#understanding-goroutines)
3. [Concurrency Fundamentals](#concurrency-fundamentals)
4. [Race Conditions & Data Races](#race-conditions--data-races)
5. [Go Memory Model](#go-memory-model)
6. [Managing Shared State](#managing-shared-state)
7. [Mutex - Mutual Exclusion Lock](#mutex---mutual-exclusion-lock)
8. [RWMutex - Reader/Writer Mutex](#rwmutex---readerwriter-mutex)
9. [WaitGroup - Goroutine Synchronization](#waitgroup---goroutine-synchronization)
10. [Once - One-Time Initialization](#once---one-time-initialization)
11. [Pool - Object Reuse](#pool---object-reuse)
12. [Map - Concurrent Map](#map---concurrent-map)
13. [Cond - Condition Variables](#cond---condition-variables)
14. [Common Patterns & Best Practices](#common-patterns--best-practices)
15. [Performance Considerations](#performance-considerations)
16. [Real-World Examples](#real-world-examples)

---

## Introduction

The `sync` package provides **basic synchronization primitives** for managing concurrent access to shared memory in Go programs. Understanding these primitives is essential for writing safe, correct concurrent code.

### Official Documentation

- **sync Package Documentation**: https://pkg.go.dev/sync
- **Go Memory Model**: https://go.dev/ref/mem
- **Effective Go - Concurrency**: https://go.dev/doc/effective_go#concurrency
- **Go Blog - Share Memory by Communicating**: https://go.dev/blog/codelab-share
- **Data Race Detector**: https://go.dev/doc/articles/race_detector

### What is the sync Package?

The `sync` package provides low-level synchronization primitives that protect shared memory from concurrent access issues. While Go's philosophy emphasizes "*Don't communicate by sharing memory; share memory by communicating*" (using channels), there are scenarios where direct memory synchronization is more appropriate or performant.

**Key Principle**: Values containing types from the `sync` package should **NEVER be copied** after first use. Copying a mutex, for example, copies its internal state, leading to undefined behavior.

### When to Use sync vs Channels

This is one of the most important decisions in Go concurrent programming:

**Use `sync` primitives when:**
- **Protecting shared state**: Counters, caches, maps that multiple goroutines access
- **Performance-critical paths**: Lower overhead than channels for simple locking
- **Read-heavy workloads**: `RWMutex` allows concurrent reads
- **Ensuring one-time initialization**: `sync.Once` guarantees single execution
- **Managing resource pools**: Object reuse with `sync.Pool`
- **Simple coordination**: Waiting for goroutines with `WaitGroup`

**Use channels when:**
- **Transferring ownership**: Moving data between goroutines
- **Distributing work**: Worker pools, fan-out/fan-in patterns
- **Communicating events**: Signaling state changes, cancellation
- **Pipeline processing**: Chaining operations
- **Orchestration**: Complex goroutine coordination
- **CSP-style programming**: Communicating Sequential Processes patterns

**Rule of Thumb**: Use channels for communication, use mutexes for protecting state.

---

## Understanding Goroutines

Before diving into synchronization primitives, you must understand **goroutines** - the foundation of Go's concurrency model.

### What is a Goroutine?

A **goroutine** is a lightweight thread managed by the Go runtime. It's not an OS thread - it's a function executing concurrently with other goroutines in the same address space.

**Key characteristics**:
- **Lightweight**: Start with ~2KB stack (grows/shrinks dynamically)
- **Cheap**: Can run thousands/millions simultaneously
- **Managed**: Go runtime schedules them on OS threads
- **Shared memory**: All goroutines share the same address space

### Creating Goroutines

```go
// Sequential execution
func main() {
    doWork()    // Runs in main goroutine
    moreWork()  // Waits for doWork() to finish
}

// Concurrent execution
func main() {
    go doWork()    // Runs in NEW goroutine
    moreWork()     // Runs immediately in main goroutine
    // Problem: main might exit before doWork() finishes!
}
```

### Goroutine Lifecycle

```go
func main() {
    fmt.Println("Main starts")           // Main goroutine
    
    go func() {                          // New goroutine created
        fmt.Println("Goroutine executes") // Runs concurrently
    }()                                   // Goroutine started
    
    fmt.Println("Main continues")        // Doesn't wait!
    time.Sleep(time.Second)              // Hack: wait for goroutine
    fmt.Println("Main exits")            // All goroutines terminated
}
```

**States in goroutine lifecycle**:
1. **Created**: `go` keyword spawns goroutine
2. **Runnable**: Waiting to be scheduled on CPU
3. **Running**: Executing on OS thread
4. **Waiting**: Blocked on I/O, channel, mutex, etc.
5. **Dead**: Function returned, goroutine exits

### The Goroutine Scheduler

Go uses an **M:N scheduler** (M goroutines on N OS threads):

```
Goroutines:  G1  G2  G3  G4  G5  G6  G7  G8  ...  (thousands)
                ↓   ↓   ↓   ↓   ↓   ↓   ↓   ↓
Scheduler:      [  Go Runtime Scheduler  ]
                ↓   ↓   ↓   ↓
OS Threads:     M1  M2  M3  M4  ...  (GOMAXPROCS, typically # CPUs)
                ↓   ↓   ↓   ↓
CPU Cores:      P1  P2  P3  P4
```

**Key concepts**:
- **G (Goroutine)**: The function being executed
- **M (Machine)**: OS thread
- **P (Processor)**: Scheduling context (max = GOMAXPROCS)

### Common Goroutine Pitfalls

#### Pitfall 1: Loop Variable Capture

```go
// ❌ WRONG: All goroutines see final value
for i := 0; i < 5; i++ {
    go func() {
        fmt.Println(i) // All print 5!
    }()
}

// ✅ CORRECT: Pass value as parameter
for i := 0; i < 5; i++ {
    go func(id int) {
        fmt.Println(id) // Prints 0, 1, 2, 3, 4
    }(i)
}

// ✅ ALSO CORRECT: Create loop-scoped variable
for i := 0; i < 5; i++ {
    i := i  // Shadow loop variable
    go func() {
        fmt.Println(i) // Each goroutine has own copy
    }()
}
```

#### Pitfall 2: Goroutine Leaks

```go
// ❌ WRONG: Goroutine never exits (leak!)
func leakyFunction() {
    ch := make(chan int)
    go func() {
        val := <-ch  // Blocks forever if nothing sends
        fmt.Println(val)
    }()
    // Function returns, channel never receives, goroutine leaks
}

// ✅ CORRECT: Use context for cancellation
func nonLeakyFunction(ctx context.Context) {
    ch := make(chan int)
    go func() {
        select {
        case val := <-ch:
            fmt.Println(val)
        case <-ctx.Done():
            return  // Goroutine can exit
        }
    }()
}
```

#### Pitfall 3: No Guarantee of Execution

```go
// ❌ WRONG: main might exit before goroutine runs
func main() {
    go fmt.Println("Hello from goroutine")
    // main exits immediately, goroutine might not run
}

// ✅ CORRECT: Wait for goroutine
func main() {
    var wg sync.WaitGroup
    wg.Add(1)
    go func() {
        defer wg.Done()
        fmt.Println("Hello from goroutine")
    }()
    wg.Wait() // Waits for goroutine to finish
}
```

---

## Concurrency Fundamentals

### Concurrency vs Parallelism

These terms are often confused but represent different concepts:

**Concurrency**: Dealing with multiple things at once (structure)
- Multiple tasks make progress in overlapping time periods
- About **composition** of independently executing processes
- Can happen on single CPU core (time-slicing)

**Parallelism**: Doing multiple things at once (execution)
- Multiple tasks execute simultaneously
- About **simultaneous execution** on multiple CPU cores
- Requires multiple processors

```go
// Concurrent (may or may not be parallel)
go task1()  // Goroutine 1
go task2()  // Goroutine 2
// Runtime decides if they run in parallel

// Example timeline on single core (concurrent, not parallel):
// Time:  0ms   10ms  20ms  30ms  40ms  50ms
// CPU:   T1    T2    T1    T2    T1    T2   (interleaved)

// Example timeline on dual core (concurrent AND parallel):
// Time:  0ms        25ms        50ms
// Core1: Task1      Task1       Task1   (running)
// Core2: Task2      Task2       Task2   (simultaneously)
```

**Rob Pike's explanation**: "*Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once.*"

### Shared Memory Model

Go goroutines share the same memory space:

```go
var counter int  // Shared variable

func main() {
    go func() {
        counter++  // Goroutine 1 accesses counter
    }()
    
    go func() {
        counter++  // Goroutine 2 accesses counter
    }()
    
    // DANGER: Both goroutines access shared memory!
}
```

**Memory layout**:
```
        Heap (shared by all goroutines)
     ┌─────────────────────────────────┐
     │  counter: 0                     │
     │  objects, slices, maps, etc.    │
     └─────────────────────────────────┘
             ↑               ↑
             │               │
     ┌───────┴─────┐   ┌─────┴───────┐
     │ Goroutine 1 │   │ Goroutine 2 │
     │   Stack     │   │   Stack     │
     │ (local vars)│   │ (local vars)│
     └─────────────┘   └─────────────┘
```

### Why Go Maps Aren't Thread-Safe by Default

**Design Decision**: Go maps are intentionally not thread-safe for performance and simplicity.

**Reasons**:

1. **Performance**: Thread-safe maps require locking on every operation, adding overhead even in single-threaded scenarios
   ```go
   // If maps were thread-safe, EVERY access would need locking
   m["key"] = value  // Would internally: lock → write → unlock
   val := m["key"]   // Would internally: lock → read → unlock
   // Expensive even when only one goroutine uses the map!
   ```

2. **Not all programs need concurrency**: Many programs use maps in single-threaded contexts
   ```go
   func processData(input string) map[string]int {
       result := make(map[string]int)  // Only used in this function
       // ... process ...
       return result  // No concurrency needed
   }
   ```

3. **One size doesn't fit all**: Different use cases need different synchronization strategies
   - Read-heavy workloads → `RWMutex` is better
   - Write-heavy workloads → `Mutex` is better
   - Specific patterns → `sync.Map` might be better
   - Single owner pattern → Channels are better

4. **Fail-fast detection**: Concurrent map access causes immediate panic (detectable), better than silent corruption
   ```go
   // Concurrent access to map
   fatal error: concurrent map read and map write
   // Crashes immediately instead of corrupting data silently
   ```

**What happens with concurrent map access**:
```go
var m = make(map[string]int)

// Goroutine 1: Writing
go func() {
    m["key"] = 1  // Modifies internal data structure
}()

// Goroutine 2: Reading
go func() {
    val := m["key"]  // Reads internal data structure
}()

// PANIC! Runtime detects concurrent access
// fatal error: concurrent map read and map write
```

**The internal reason**: Maps use a hash table with buckets. Concurrent writes can:
- Corrupt bucket pointers
- Create invalid memory references
- Cause the map to grow/rehash while being read
- Result in lost data or crashes

**Solution**: Protect maps with synchronization when needed:
```go
type SafeMap struct {
    mu sync.RWMutex
    m  map[string]int
}

func (sm *SafeMap) Get(key string) (int, bool) {
    sm.mu.RLock()
    defer sm.mu.RUnlock()
    val, ok := sm.m[key]
    return val, ok
}

func (sm *SafeMap) Set(key string, val int) {
    sm.mu.Lock()
    defer sm.mu.Unlock()
    sm.m[key] = val
}
```

### Critical Sections

A **critical section** is code that accesses shared resources and must not be executed by multiple goroutines simultaneously.

```go
var balance int = 1000  // Shared bank account

// Critical section: read-modify-write
func withdraw(amount int) {
    // START CRITICAL SECTION
    current := balance      // Read
    if current >= amount {  // Check
        balance -= amount   // Modify
    }
    // END CRITICAL SECTION
}

// Problem: Two goroutines can interleave:
// Time  Goroutine 1        Goroutine 2        balance
// ───────────────────────────────────────────────────
// t0                                          1000
// t1    Read: 1000
// t2                       Read: 1000
// t3    Check: OK
// t4                       Check: OK
// t5    Write: 500
// t6                       Write: 500         500 (should be 0!)
```

**Solution**: Protect critical section with mutex (see Mutex section).

---

## Race Conditions & Data Races

### What is a Race Condition?

A **race condition** occurs when program behavior depends on the relative timing of events (like thread scheduling). The outcome is non-deterministic.

```go
var result int

go func() {
    result = compute1()  // Might execute first or second
}()

go func() {
    result = compute2()  // Might execute first or second
}()

time.Sleep(time.Second)
fmt.Println(result)  // Unpredictable: compute1 or compute2 result?
```

### What is a Data Race?

A **data race** is a specific type of race condition where:
1. Two or more goroutines access the same variable
2. At least one access is a write
3. Accesses are not synchronized

**Data races cause undefined behavior** - your program may crash, produce wrong results, or appear to work.

```go
var counter int  // Shared variable

// Data race: concurrent read and write
go func() {
    counter++  // Read, increment, write (3 operations!)
}()

go func() {
    counter++  // Read, increment, write (not atomic!)
}()

// Result: counter might be 1 instead of 2!
```

### Why counter++ is Not Safe

```go
counter++  // Looks atomic, but it's actually 3 operations:

// Assembly-level view:
// 1. Load counter from memory to register
// 2. Increment register
// 3. Store register back to memory

// Interleaving example:
// Goroutine 1          Goroutine 2          counter (memory)
// ────────────────────────────────────────────────────────
//                                            0
// Load: reg1 = 0
//                      Load: reg2 = 0
// Inc:  reg1 = 1
//                      Inc:  reg2 = 1
// Store: counter = 1
//                      Store: counter = 1    1 (Lost update!)
```

### Detecting Data Races

Go provides a **race detector**:

```bash
# Run with race detection
go run -race main.go
go test -race ./...
go build -race

# Example output:
==================
WARNING: DATA RACE
Write at 0x00c000014088 by goroutine 7:
  main.increment()
      /path/to/main.go:15 +0x3e

Previous read at 0x00c000014088 by goroutine 6:
  main.increment()
      /path/to/main.go:15 +0x3e
==================
```

**Important**: Race detector finds races that occur during execution. Always test concurrent code with `-race`.

---

## Go Memory Model

The **Go Memory Model** specifies when reads of a variable in one goroutine are guaranteed to observe values written to the same variable in another goroutine.

### Happens-Before Relationship

Go defines a **happens-before** partial order:
- If event A happens-before event B, then A's effects are visible to B
- If A doesn't happen-before B, and B doesn't happen-before A, they are **concurrent**

**Without synchronization, you have NO guarantees about ordering!**

```go
var a, b int

// Goroutine 1
func g1() {
    a = 1       // A1
    b = 2       // A2
}

// Goroutine 2
func g2() {
    print(b)    // B1
    print(a)    // B2
}

go g1()
go g2()

// Possible outputs: 00, 02, 20, 22
// Even 20 is possible! (b=2 visible before a=1)
// Compiler/CPU can reorder operations!
```

### Synchronization Guarantees

Go provides happens-before guarantees through:

1. **Channel operations**
   ```go
   var c = make(chan int)
   var a int
   
   go func() {
       a = 1
       c <- 0  // Send happens-before receive
   }()
   
   <-c         // Receive
   print(a)    // Guaranteed to see a = 1
   ```

2. **Mutex locks**
   ```go
   var mu sync.Mutex
   var a int
   
   go func() {
       mu.Lock()
       a = 1
       mu.Unlock()  // Unlock happens-before next Lock
   }()
   
   mu.Lock()        // Lock
   print(a)         // Guaranteed to see a = 1
   mu.Unlock()
   ```

3. **sync.Once**
   ```go
   var once sync.Once
   var a int
   
   once.Do(func() {
       a = 1  // Completion happens-before Do() returns
   })
   
   print(a)  // Guaranteed to see a = 1
   ```

### Common Misconceptions

```go
// ❌ WRONG: No synchronization = no guarantees
var ready bool
var data int

go func() {
    data = 42
    ready = true  // Not synchronized!
}()

for !ready {  // Might never see ready = true!
    // Compiler might optimize to: if !ready { for {} }
}
print(data)   // Might see 0, 42, or garbage!

// ✅ CORRECT: Use channel for synchronization
var done = make(chan bool)
var data int

go func() {
    data = 42
    done <- true  // Synchronized send
}()

<-done        // Synchronized receive
print(data)   // Guaranteed to see 42
```

---

## Managing Shared State

### State in Concurrent Programs

**State** is data that changes over time. In concurrent programs, managing shared state is the primary challenge.

**Types of state**:
1. **Local state**: Variables in goroutine stack (safe, no sharing)
2. **Shared state**: Variables accessed by multiple goroutines (needs protection)
3. **Immutable state**: Never changes after creation (safe to share)

### Approaches to Shared State

#### Approach 1: Don't Share (Recommended)

```go
// ✅ BEST: Each goroutine owns its data
func processFiles(files []string) []Result {
    results := make(chan Result)
    
    for _, file := range files {
        file := file  // Copy for goroutine
        go func() {
            result := process(file)  // Local state only
            results <- result        // Transfer ownership via channel
        }()
    }
    
    // Collect results
    var collected []Result
    for range files {
        collected = append(collected, <-results)
    }
    return collected
}
```

#### Approach 2: Share Immutable State

```go
// ✅ GOOD: Immutable data is safe to share
type Config struct {
    Host string
    Port int
    // No setters, fields never change
}

var globalConfig = &Config{Host: "localhost", Port: 8080}

// All goroutines can safely read globalConfig
func worker() {
    addr := globalConfig.Host + ":" + strconv.Itoa(globalConfig.Port)
    // ...
}
```

#### Approach 3: Protect with Mutex (When Necessary)

```go
// When you must share mutable state:
type Cache struct {
    mu    sync.RWMutex           // Protects items
    items map[string]CachedItem  // Shared mutable state
}

func (c *Cache) Get(key string) (CachedItem, bool) {
    c.mu.RLock()                 // Acquire read lock
    defer c.mu.RUnlock()         // Release when done
    item, ok := c.items[key]     // Safe: protected by lock
    return item, ok
}

func (c *Cache) Set(key string, item CachedItem) {
    c.mu.Lock()                  // Acquire write lock
    defer c.mu.Unlock()          // Release when done
    c.items[key] = item          // Safe: exclusive access
}
```

### Design Patterns for State Management

#### Pattern 1: Single Owner (Actor Pattern)

```go
// One goroutine owns state, others communicate via channels
type Database struct {
    data    map[string]string
    queries chan Query
}

type Query struct {
    key    string
    result chan string
}

func (db *Database) Run() {
    for query := range db.queries {         // Owner goroutine
        result := db.data[query.key]        // Only this goroutine accesses data
        query.result <- result
    }
}

func (db *Database) Get(key string) string {
    result := make(chan string)
    db.queries <- Query{key: key, result: result}
    return <-result  // Wait for owner to respond
}
```

#### Pattern 2: Mutex-Protected State

```go
// Multiple goroutines access state through mutex
type Counter struct {
    mu    sync.Mutex  // Guards value
    value int         // Shared mutable state
}

func (c *Counter) Inc() {
    c.mu.Lock()       // Critical section starts
    c.value++         // Modify shared state
    c.mu.Unlock()     // Critical section ends
}
```

#### Pattern 3: Copy-on-Write

```go
// Share pointer, replace on write (requires atomic.Value)
type ConfigManager struct {
    config atomic.Value  // Stores *Config
}

func (cm *ConfigManager) Get() *Config {
    return cm.config.Load().(*Config)  // Safe: atomic load
}

func (cm *ConfigManager) Update(newConfig *Config) {
    cm.config.Store(newConfig)  // Safe: atomic store, old version still readable
}
```

### Choosing the Right Approach

| Scenario | Approach | Reason |
|----------|----------|--------|
| Read-only data | Share directly | Immutable = safe |
| One writer, many readers | `sync.RWMutex` | Concurrent reads |
| Frequent updates | Channels (single owner) | Avoid lock contention |
| Simple counter | `sync.Mutex` or `atomic` | Simple, clear |
| Complex coordination | Channels | Better expressiveness |
| Cache/lookup table | `sync.RWMutex` or `sync.Map` | Optimized for reads |

---

## Mutex - Mutual Exclusion Lock

A `Mutex` is a **mutual exclusion lock** that ensures only one goroutine can access a critical section at a time.

### Mutex vs RWMutex: Key Differences

Before diving into details, understand when to use each:

| Aspect | Mutex | RWMutex |
|--------|-------|---------|
| **Locking** | One type: exclusive | Two types: read (shared) or write (exclusive) |
| **Concurrent reads** | ❌ Not allowed | ✅ Multiple readers allowed |
| **Concurrent writes** | ❌ Not allowed | ❌ Not allowed |
| **Read + write** | ❌ Not allowed | ❌ Not allowed |
| **Use case** | Balanced read/write or simple protection | Read-heavy workloads (90%+ reads) |
| **Performance** | Faster for simple/short operations | Faster when many concurrent reads |
| **Complexity** | Simple (Lock/Unlock) | More complex (RLock/RUnlock + Lock/Unlock) |
| **Overhead** | Lower | Higher (maintains reader count) |

**Quick Decision Guide**:
```go
// Use Mutex when:
// - Reads and writes are roughly equal
// - Critical section is very short
// - Simplicity matters
type Counter struct {
    mu    sync.Mutex
    count int
}

// Use RWMutex when:
// - Reads >> Writes (10:1 ratio or higher)
// - Read operations are expensive/slow
// - Many goroutines reading simultaneously
type Cache struct {
    mu    sync.RWMutex
    items map[string]Value
}
```

### When to Use Read Lock vs Write Lock

**Read Lock (`RLock`)** - Use when you only **observe** data without changing it:

```go
func (c *Cache) Get(key string) (Value, bool) {
    c.mu.RLock()              // Multiple goroutines can hold RLock simultaneously
    defer c.mu.RUnlock()
    val, ok := c.items[key]   // Just reading - no modification
    return val, ok
}

func (c *Cache) Count() int {
    c.mu.RLock()              // Reading data
    defer c.mu.RUnlock()
    return len(c.items)       // Just counting - no modification
}

func (c *Cache) Has(key string) bool {
    c.mu.RLock()              // Checking existence
    defer c.mu.RUnlock()
    _, ok := c.items[key]     // Just checking - no modification
    return ok
}
```

**Write Lock (`Lock`)** - Use when you **modify** data in any way:

```go
func (c *Cache) Set(key string, val Value) {
    c.mu.Lock()               // Exclusive access - no other readers/writers
    defer c.mu.Unlock()
    c.items[key] = val        // Modifying the map
}

func (c *Cache) Delete(key string) {
    c.mu.Lock()               // Deleting modifies the map
    defer c.mu.Unlock()
    delete(c.items, key)      // Modification
}

func (c *Cache) Clear() {
    c.mu.Lock()               // Modifying by clearing
    defer c.mu.Unlock()
    c.items = make(map[string]Value)  // Creating new map
}
```

**Tricky Cases** - Operations that read AND write need **write lock**:

```go
// ❌ WRONG: This increments but uses read lock
func (c *Cache) IncrementBad(key string) {
    c.mu.RLock()              // Read lock - WRONG!
    defer c.mu.RUnlock()
    c.items[key]++            // This MODIFIES - needs write lock!
}

// ✅ CORRECT: Read-modify-write needs write lock
func (c *Cache) Increment(key string) {
    c.mu.Lock()               // Write lock - CORRECT
    defer c.mu.Unlock()
    c.items[key]++            // Safe modification
}

// ❌ WRONG: Conditional update with read lock
func (c *Cache) UpdateIfExistsBad(key string, val Value) {
    c.mu.RLock()              // Read lock - WRONG!
    defer c.mu.RUnlock()
    if _, ok := c.items[key]; ok {
        c.items[key] = val    // Modification needs write lock!
    }
}

// ✅ CORRECT: Conditional update with write lock
func (c *Cache) UpdateIfExists(key string, val Value) {
    c.mu.Lock()               // Write lock - CORRECT
    defer c.mu.Unlock()
    if _, ok := c.items[key]; ok {
        c.items[key] = val    // Safe modification
    }
}
```

**Rule of Thumb**:
- **Reading only** → RLock (if using RWMutex)
- **Writing (adding, updating, deleting)** → Lock
- **Reading then writing** → Lock (the whole operation)
- **Unsure?** → Use Lock (safer)

### URL Shortener: Read vs Write Operations

For your Project 2 URL Shortener, identify which operations are reads vs writes:

**Read Operations** (use `RLock`):
```go
// Getting the original URL - just reading the map
func (s *URLShortener) Get(shortCode string) (string, bool) {
    s.mu.RLock()              // ✅ Read lock
    defer s.mu.RUnlock()
    url, ok := s.urls[shortCode]
    return url, ok
}

// Checking if a short code exists - just checking
func (s *URLShortener) Exists(shortCode string) bool {
    s.mu.RLock()              // ✅ Read lock
    defer s.mu.RUnlock()
    _, ok := s.urls[shortCode]
    return ok
}

// Getting total count - just reading length
func (s *URLShortener) Count() int {
    s.mu.RLock()              // ✅ Read lock
    defer s.mu.RUnlock()
    return len(s.urls)
}

// Listing all URLs - just reading
func (s *URLShortener) List() []URLMapping {
    s.mu.RLock()              // ✅ Read lock
    defer s.mu.RUnlock()
    result := make([]URLMapping, 0, len(s.urls))
    for short, long := range s.urls {
        result = append(result, URLMapping{Short: short, Long: long})
    }
    return result
}
```

**Write Operations** (use `Lock`):
```go
// Adding a new URL - modifies the map
func (s *URLShortener) Add(shortCode, longURL string) {
    s.mu.Lock()               // ✅ Write lock
    defer s.mu.Unlock()
    s.urls[shortCode] = longURL
}

// Deleting a URL - modifies the map
func (s *URLShortener) Delete(shortCode string) {
    s.mu.Lock()               // ✅ Write lock
    defer s.mu.Unlock()
    delete(s.urls, shortCode)
}

// Updating a URL - modifies the map
func (s *URLShortener) Update(shortCode, newURL string) {
    s.mu.Lock()               // ✅ Write lock
    defer s.mu.Unlock()
    s.urls[shortCode] = newURL
}
```

**Read-Then-Write Operations** (use `Lock` for entire operation):
```go
// Incrementing visit count - reads then writes
func (s *URLShortener) IncrementVisits(shortCode string) {
    s.mu.Lock()               // ✅ Write lock (not RLock!)
    defer s.mu.Unlock()
    // Even though we read first, we're modifying
    s.visits[shortCode]++
}

// Get and delete (consume) - reads then writes
func (s *URLShortener) GetAndDelete(shortCode string) (string, bool) {
    s.mu.Lock()               // ✅ Write lock
    defer s.mu.Unlock()
    url, ok := s.urls[shortCode]
    if ok {
        delete(s.urls, shortCode)  // Modifying
    }
    return url, ok
}

// Generate unique short code - checks then adds
func (s *URLShortener) GenerateAndAdd(longURL string) string {
    s.mu.Lock()               // ✅ Write lock
    defer s.mu.Unlock()
    
    // Generate random code
    shortCode := generateCode()
    
    // Check if exists, regenerate if needed
    for _, exists := s.urls[shortCode]; exists; {
        shortCode = generateCode()
    }
    
    // Add to map
    s.urls[shortCode] = longURL
    return shortCode
}
```

**Performance Impact in URL Shortener**:

Typical usage pattern for a URL shortener:
- 1 URL created (write)
- 1000+ people click the link (reads)
- **Ratio: 1000:1 reads to writes** → Perfect for RWMutex!

```go
// HTTP Handler flow
func (h *Handler) RedirectHandler(w http.ResponseWriter, r *http.Request) {
    shortCode := extractCode(r.URL.Path)
    
    // This happens 1000+ times (READ)
    longURL, ok := h.shortener.Get(shortCode)  // Uses RLock
    
    if !ok {
        http.NotFound(w, r)
        return
    }
    
    http.Redirect(w, r, longURL, http.StatusFound)
}

func (h *Handler) ShortenHandler(w http.ResponseWriter, r *http.Request) {
    longURL := extractURL(r)
    
    // This happens once (WRITE)
    shortCode := h.shortener.GenerateAndAdd(longURL)  // Uses Lock
    
    json.NewEncoder(w).Encode(map[string]string{
        "short": shortCode,
    })
}
```

**Summary for URL Shortener**:
- `Get()`, `Exists()`, `List()` → **RLock** (reading only)
- `Add()`, `Delete()`, `Update()` → **Lock** (modifying)
- `IncrementVisits()`, `GetAndDelete()` → **Lock** (read + modify)
- Expected traffic: 99% reads, 1% writes → **RWMutex is perfect!**

### Basic Usage

```go
package main

import (
    "fmt"
    "sync"
)

type Counter struct {
    mu    sync.Mutex
    value int
}

func (c *Counter) Increment() {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.value++
}

func (c *Counter) Value() int {
    c.mu.Lock()
    defer c.mu.Unlock()
    return c.value
}

func main() {
    var wg sync.WaitGroup
    counter := &Counter{}

    // Launch 1000 goroutines
    for i := 0; i < 1000; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            counter.Increment()
        }()
    }

    wg.Wait()
    fmt.Println("Final count:", counter.Value()) // Always 1000
}
```

### Methods

#### `Lock()`
Locks the mutex. If already locked, the calling goroutine **blocks** until available.

```go
mu.Lock()
// Critical section - only one goroutine here
mu.Unlock()
```

#### `Unlock()`
Unlocks the mutex. **Runtime error** if not locked on entry.

```go
mu.Lock()
defer mu.Unlock() // Always use defer to ensure unlock
```

#### `TryLock()` (Go 1.18+)
Attempts to lock and returns whether it succeeded. **Non-blocking**.

```go
if mu.TryLock() {
    defer mu.Unlock()
    // Got the lock
} else {
    // Lock not available, do something else
}
```

### Best Practices

**DO:**
```go
// ✅ Always use defer to unlock
func (c *Counter) Increment() {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.value++
}

// ✅ Keep critical sections small
mu.Lock()
counter++
mu.Unlock()

// ✅ Embed mutex in the struct it protects
type SafeMap struct {
    mu   sync.Mutex
    data map[string]int
}
```

**DON'T:**
```go
// ❌ Never copy a mutex
func badCopy(c Counter) { // Copies the mutex!
    c.Increment()
}

// ❌ Don't lock twice in same goroutine (deadlock)
mu.Lock()
mu.Lock() // Deadlock!

// ❌ Don't unlock from different goroutine (usually wrong)
go func() {
    mu.Unlock() // Dangerous!
}()
```

### Common Pitfall: Copying Mutexes

```go
// ❌ WRONG: Mutex gets copied
type User struct {
    mu   sync.Mutex
    name string
}

func updateUser(u User) { // Pass by value copies mutex!
    u.mu.Lock()
    defer u.mu.Unlock()
    u.name = "Updated"
}

// ✅ CORRECT: Pass by pointer
func updateUser(u *User) {
    u.mu.Lock()
    defer u.mu.Unlock()
    u.name = "Updated"
}
```

---

## RWMutex - Reader/Writer Mutex

`RWMutex` allows **multiple readers** OR **one writer**, but not both simultaneously. Optimized for read-heavy workloads.

### Basic Usage

```go
package main

import (
    "fmt"
    "sync"
    "time"
)

type Cache struct {
    mu    sync.RWMutex
    items map[string]string
}

func NewCache() *Cache {
    return &Cache{
        items: make(map[string]string),
    }
}

// Read operations use RLock (multiple readers allowed)
func (c *Cache) Get(key string) (string, bool) {
    c.mu.RLock()
    defer c.mu.RUnlock()
    val, ok := c.items[key]
    return val, ok
}

// Write operations use Lock (exclusive access)
func (c *Cache) Set(key, value string) {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.items[key] = value
}

func main() {
    cache := NewCache()
    
    // Multiple readers can read concurrently
    for i := 0; i < 10; i++ {
        go func(id int) {
            for j := 0; j < 100; j++ {
                cache.Get("key")
            }
        }(i)
    }
    
    // Writer gets exclusive access
    go func() {
        for i := 0; i < 10; i++ {
            cache.Set(fmt.Sprintf("key%d", i), fmt.Sprintf("value%d", i))
            time.Sleep(10 * time.Millisecond)
        }
    }()
    
    time.Sleep(2 * time.Second)
}
```

### Methods

#### Read Lock Methods

**`RLock()`**: Locks for reading. Multiple goroutines can hold read locks simultaneously.

```go
cache.mu.RLock()
value := cache.items[key]
cache.mu.RUnlock()
```

**`RUnlock()`**: Unlocks a read lock. Runtime error if not read-locked.

**`TryRLock()` (Go 1.18+)**: Attempts to acquire read lock without blocking.

```go
if cache.mu.TryRLock() {
    defer cache.mu.RUnlock()
    // Read operation
}
```

#### Write Lock Methods

**`Lock()`**: Locks for writing. Exclusive - no readers or writers allowed.

**`Unlock()`**: Unlocks write lock.

**`TryLock()` (Go 1.18+)**: Attempts to acquire write lock without blocking.

#### Other Methods

**`RLocker()`**: Returns a `Locker` interface for read locking.

```go
readLock := cache.mu.RLocker()
readLock.Lock()   // Calls RLock
readLock.Unlock() // Calls RUnlock
```

### When to Use RWMutex

**Use `RWMutex` when:**
- Reads significantly outnumber writes (10:1 or higher)
- Read operations are expensive
- Critical sections are long enough to justify overhead

**Use regular `Mutex` when:**
- Reads and writes are balanced
- Critical sections are very short
- Simplicity matters more than performance

### Performance Example

```go
package main

import (
    "fmt"
    "sync"
    "testing"
    "time"
)

type DataWithMutex struct {
    mu   sync.Mutex
    data map[int]int
}

type DataWithRWMutex struct {
    mu   sync.RWMutex
    data map[int]int
}

func BenchmarkMutexReads(b *testing.B) {
    d := &DataWithMutex{data: make(map[int]int)}
    d.data[1] = 100
    
    b.RunParallel(func(pb *testing.PB) {
        for pb.Next() {
            d.mu.Lock()
            _ = d.data[1]
            d.mu.Unlock()
        }
    })
}

func BenchmarkRWMutexReads(b *testing.B) {
    d := &DataWithRWMutex{data: make(map[int]int)}
    d.data[1] = 100
    
    b.RunParallel(func(pb *testing.PB) {
        for pb.Next() {
            d.mu.RLock()
            _ = d.data[1]
            d.mu.RUnlock()
        }
    })
}

// RWMutex is ~5-10x faster for read-heavy workloads!
```

### Important: No Lock Upgrades

```go
// ❌ WRONG: Cannot upgrade read lock to write lock
cache.mu.RLock()
if needsUpdate {
    cache.mu.Lock() // DEADLOCK! Can't upgrade
    cache.items[key] = newValue
    cache.mu.Unlock()
}
cache.mu.RUnlock()

// ✅ CORRECT: Release read lock first
cache.mu.RLock()
value := cache.items[key]
needsUpdate := checkCondition(value)
cache.mu.RUnlock()

if needsUpdate {
    cache.mu.Lock()
    cache.items[key] = newValue
    cache.mu.Unlock()
}
```

---

## WaitGroup - Goroutine Synchronization

`WaitGroup` waits for a collection of goroutines to finish. Think of it as a **counter for pending operations**.

### Basic Usage

```go
package main

import (
    "fmt"
    "sync"
    "time"
)

func worker(id int, wg *sync.WaitGroup) {
    defer wg.Done() // Decrement counter when done
    
    fmt.Printf("Worker %d starting\n", id)
    time.Sleep(time.Second)
    fmt.Printf("Worker %d done\n", id)
}

func main() {
    var wg sync.WaitGroup
    
    for i := 1; i <= 5; i++ {
        wg.Add(1) // Increment counter
        go worker(i, &wg)
    }
    
    wg.Wait() // Block until counter reaches 0
    fmt.Println("All workers done")
}
```

### Methods

#### `Add(delta int)`
Adds `delta` (can be negative) to the WaitGroup counter. If counter becomes zero, all goroutines blocked on `Wait()` are released.

```go
wg.Add(1)  // Increment by 1
wg.Add(5)  // Increment by 5
wg.Add(-1) // Decrement by 1 (same as Done)
```

**Important**: `Add()` must be called **before** starting the goroutine, not inside it.

```go
// ✅ CORRECT: Add before goroutine
for i := 0; i < 10; i++ {
    wg.Add(1)
    go func(id int) {
        defer wg.Done()
        work(id)
    }(i)
}

// ❌ WRONG: Race condition!
for i := 0; i < 10; i++ {
    go func(id int) {
        wg.Add(1) // May call Wait() before Add()!
        defer wg.Done()
        work(id)
    }(i)
}
```

#### `Done()`
Decrements the counter by one. Equivalent to `Add(-1)`.

```go
func worker(wg *sync.WaitGroup) {
    defer wg.Done() // Always use defer!
    // Do work...
}
```

#### `Wait()`
Blocks until the counter is zero.

```go
wg.Wait() // Blocks until all Done() calls complete
```

#### `Go(f func())` (Go 1.25+)
Convenience method that calls `f` in a new goroutine and automatically manages Add/Done.

```go
var wg sync.WaitGroup

// Old way
wg.Add(1)
go func() {
    defer wg.Done()
    doWork()
}()

// New way (Go 1.25+)
wg.Go(doWork)
```

### Real-World Example: Parallel Processing

```go
package main

import (
    "fmt"
    "sync"
)

func processFiles(files []string) []Result {
    results := make([]Result, len(files))
    var wg sync.WaitGroup
    
    for i, file := range files {
        wg.Add(1)
        go func(index int, filename string) {
            defer wg.Done()
            results[index] = processFile(filename)
        }(i, file)
    }
    
    wg.Wait()
    return results
}

type Result struct {
    File string
    Data []byte
    Err  error
}

func processFile(filename string) Result {
    // Process file...
    return Result{File: filename}
}
```

### Error Handling with WaitGroup

```go
package main

import (
    "fmt"
    "sync"
)

func processWithErrors(items []string) error {
    var wg sync.WaitGroup
    errChan := make(chan error, len(items))
    
    for _, item := range items {
        wg.Add(1)
        go func(s string) {
            defer wg.Done()
            if err := process(s); err != nil {
                errChan <- err
            }
        }(item)
    }
    
    wg.Wait()
    close(errChan)
    
    // Collect errors
    for err := range errChan {
        if err != nil {
            return err // Return first error
        }
    }
    
    return nil
}

func process(s string) error {
    // Process item...
    return nil
}
```

---

## Once - One-Time Initialization

`Once` ensures a function is executed **exactly once**, even when called from multiple goroutines concurrently.

### Basic Usage

```go
package main

import (
    "fmt"
    "sync"
)

var (
    instance *Singleton
    once     sync.Once
)

type Singleton struct {
    data string
}

func GetInstance() *Singleton {
    once.Do(func() {
        fmt.Println("Creating singleton instance")
        instance = &Singleton{data: "initialized"}
    })
    return instance
}

func main() {
    var wg sync.WaitGroup
    
    for i := 0; i < 10; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            s := GetInstance()
            fmt.Println(s.data)
        }()
    }
    
    wg.Wait()
    // "Creating singleton instance" printed only once!
}
```

### Methods

#### `Do(f func())`
Calls `f` only on the **first** call. Subsequent calls block until the first call completes, then return immediately without calling `f`.

```go
var once sync.Once

once.Do(initialize) // Runs initialize()
once.Do(initialize) // Does nothing
once.Do(initialize) // Does nothing
```

### Common Use Cases

#### 1. Singleton Pattern

```go
package config

import "sync"

var (
    cfg  *Config
    once sync.Once
)

type Config struct {
    DatabaseURL string
    APIKey      string
}

func Get() *Config {
    once.Do(func() {
        cfg = &Config{
            DatabaseURL: loadFromEnv("DB_URL"),
            APIKey:      loadFromEnv("API_KEY"),
        }
    })
    return cfg
}
```

#### 2. Lazy Initialization

```go
type Service struct {
    clientOnce sync.Once
    client     *http.Client
}

func (s *Service) getClient() *http.Client {
    s.clientOnce.Do(func() {
        s.client = &http.Client{
            Timeout: 10 * time.Second,
        }
    })
    return s.client
}
```

#### 3. Test Setup

```go
var (
    testDB   *sql.DB
    setupDB  sync.Once
)

func getTestDB(t *testing.T) *sql.DB {
    setupDB.Do(func() {
        var err error
        testDB, err = sql.Open("postgres", "test://...")
        if err != nil {
            t.Fatal(err)
        }
    })
    return testDB
}
```

### Go 1.21+ Helper Functions

#### `OnceFunc(f func()) func()`
Returns a function that invokes `f` only once.

```go
initialize := sync.OnceFunc(func() {
    fmt.Println("Initializing...")
})

initialize() // Prints "Initializing..."
initialize() // Does nothing
initialize() // Does nothing
```

#### `OnceValue[T any](f func() T) func() T`
Returns a function that invokes `f` only once and caches the result.

```go
getConfig := sync.OnceValue(func() *Config {
    return &Config{/* ... */}
})

cfg1 := getConfig() // Calls function
cfg2 := getConfig() // Returns cached value
// cfg1 == cfg2 (same pointer)
```

#### `OnceValues[T1, T2 any](f func() (T1, T2)) func() (T1, T2)`
Like `OnceValue` but for functions returning two values.

```go
getDBConnection := sync.OnceValues(func() (*sql.DB, error) {
    return sql.Open("postgres", connString)
})

db, err := getDBConnection() // Calls function
db, err = getDBConnection()  // Returns cached values
```

### Panic Handling

If `f` panics, `Once` considers it to have returned - future calls will **not** retry.

```go
var once sync.Once

once.Do(func() {
    panic("initialization failed")
})

// Future calls won't retry - they just return!
once.Do(func() {
    fmt.Println("This never runs")
})
```

---

## Pool - Object Reuse

`Pool` is a **temporary object pool** for caching allocated but unused items, reducing GC pressure.

### Basic Usage

```go
package main

import (
    "bytes"
    "fmt"
    "sync"
)

var bufferPool = sync.Pool{
    New: func() interface{} {
        return new(bytes.Buffer)
    },
}

func processData(data string) string {
    // Get buffer from pool
    buf := bufferPool.Get().(*bytes.Buffer)
    defer bufferPool.Put(buf)
    
    // Reset before use
    buf.Reset()
    
    // Use buffer
    buf.WriteString(data)
    buf.WriteString(" processed")
    
    return buf.String()
}

func main() {
    for i := 0; i < 5; i++ {
        result := processData(fmt.Sprintf("item-%d", i))
        fmt.Println(result)
    }
}
```

### Methods

#### `Get() any`
Selects an arbitrary item from pool, removes it, and returns it. If pool is empty and `New` is set, calls `New()`.

```go
buf := bufferPool.Get().(*bytes.Buffer)
```

#### `Put(x any)`
Adds item back to the pool. Item may be discarded at any time.

```go
bufferPool.Put(buf)
```

### Important Characteristics

**⚠️ Items can be removed automatically at any time without notification.**

```go
// Don't rely on Pool for long-term storage!
pool.Put(expensiveObject)
// GC might remove it before next Get()
```

**⚠️ Pool is NOT a cache.** Use a map with TTL for caching.

```go
// ❌ WRONG: Don't use Pool for caching
var cache sync.Pool // Items can disappear!

// ✅ CORRECT: Use a real cache
var cache map[string]Value
var cacheMu sync.RWMutex
```

### Real-World Example: HTTP Server

```go
package main

import (
    "encoding/json"
    "net/http"
    "sync"
)

type Response struct {
    Status string `json:"status"`
    Data   []byte `json:"data"`
}

var responsePool = sync.Pool{
    New: func() interface{} {
        return &Response{}
    },
}

func handler(w http.ResponseWriter, r *http.Request) {
    // Get response object from pool
    resp := responsePool.Get().(*Response)
    defer responsePool.Put(resp)
    
    // Reset fields
    resp.Status = "ok"
    resp.Data = processRequest(r)
    
    json.NewEncoder(w).Encode(resp)
}

func processRequest(r *http.Request) []byte {
    return []byte("processed")
}
```

### When to Use Pool

**Use `sync.Pool` when:**
- Creating temporary objects in hot paths
- Objects are expensive to allocate
- High allocation rate causing GC pressure
- Objects can be safely reused

**Don't use `sync.Pool` when:**
- Objects need to persist
- You need a cache (use a map)
- Allocation cost is low
- Object reuse is unsafe (has state)

### Benchmarking Pool Benefits

```go
package main

import (
    "bytes"
    "sync"
    "testing"
)

var bufferPool = sync.Pool{
    New: func() interface{} {
        return new(bytes.Buffer)
    },
}

func BenchmarkWithoutPool(b *testing.B) {
    for i := 0; i < b.N; i++ {
        buf := new(bytes.Buffer)
        buf.WriteString("test data")
        _ = buf.String()
    }
}

func BenchmarkWithPool(b *testing.B) {
    for i := 0; i < b.N; i++ {
        buf := bufferPool.Get().(*bytes.Buffer)
        buf.Reset()
        buf.WriteString("test data")
        _ = buf.String()
        bufferPool.Put(buf)
    }
}

// Pool version is typically 30-50% faster!
```

---

## Map - Concurrent Map

`sync.Map` is a concurrent map optimized for two use cases:
1. Entry written once but read many times
2. Multiple goroutines read/write disjoint key sets

### Basic Usage

```go
package main

import (
    "fmt"
    "sync"
)

func main() {
    var m sync.Map
    
    // Store values
    m.Store("key1", "value1")
    m.Store("key2", 42)
    
    // Load values
    if val, ok := m.Load("key1"); ok {
        fmt.Println(val) // "value1"
    }
    
    // Load or store
    actual, loaded := m.LoadOrStore("key3", "value3")
    fmt.Println(actual, loaded) // "value3" false
    
    // Delete
    m.Delete("key1")
    
    // Range over entries
    m.Range(func(key, value interface{}) bool {
        fmt.Printf("%v: %v\n", key, value)
        return true // Continue iteration
    })
}
```

### Methods

#### `Load(key any) (value any, ok bool)`
Returns value for key if present.

```go
val, ok := m.Load("key")
if ok {
    user := val.(*User)
}
```

#### `Store(key, value any)`
Sets value for key.

```go
m.Store("user:123", &User{ID: 123})
```

#### `LoadOrStore(key, value any) (actual any, loaded bool)`
Returns existing value if present, otherwise stores and returns given value.

```go
actual, loaded := m.LoadOrStore("key", "new value")
if loaded {
    // Key existed, actual is the old value
} else {
    // Key was new, actual is "new value"
}
```

#### `LoadAndDelete(key any) (value any, loaded bool)`
Deletes key and returns previous value.

```go
val, existed := m.LoadAndDelete("key")
```

#### `Delete(key any)`
Deletes value for key.

```go
m.Delete("key")
```

#### `Range(f func(key, value any) bool)`
Calls `f` for each key-value pair. Stops if `f` returns false.

```go
m.Range(func(key, value any) bool {
    fmt.Printf("%v: %v\n", key, value)
    return true // Continue
})
```

#### `Swap(key, value any) (previous any, loaded bool)` (Go 1.20+)
Swaps value for key and returns previous value.

```go
prev, existed := m.Swap("key", "new value")
```

#### `CompareAndSwap(key, old, new any) bool` (Go 1.20+)
Swaps value only if current value equals `old`.

```go
swapped := m.CompareAndSwap("key", "old", "new")
if swapped {
    // Swap succeeded
}
```

#### `CompareAndDelete(key, old any) bool` (Go 1.20+)
Deletes key only if current value equals `old`.

```go
deleted := m.CompareAndDelete("key", "expected")
```

#### `Clear()` (Go 1.23+)
Deletes all entries.

```go
m.Clear()
```

### When NOT to Use sync.Map

**❌ Don't use `sync.Map` when:**
- You need type safety (use `map[K]V` with `sync.RWMutex`)
- Keys/values are strongly typed
- Simple use case (regular map + mutex is clearer)

```go
// ❌ WRONG: sync.Map loses type safety
var users sync.Map
users.Store("123", &User{}) // any type
val, _ := users.Load("123")
user := val.(*User) // Type assertion required, can panic

// ✅ BETTER: Regular map with RWMutex
type UserCache struct {
    mu    sync.RWMutex
    users map[string]*User
}

func (c *UserCache) Get(id string) *User {
    c.mu.RLock()
    defer c.mu.RUnlock()
    return c.users[id]
}
```

### Real-World Example: Request Cache

```go
package main

import (
    "context"
    "fmt"
    "sync"
    "time"
)

type RequestCache struct {
    cache sync.Map // key: string, value: *CachedResponse
}

type CachedResponse struct {
    Data      []byte
    ExpiresAt time.Time
}

func (rc *RequestCache) Get(ctx context.Context, key string) ([]byte, bool) {
    val, ok := rc.cache.Load(key)
    if !ok {
        return nil, false
    }
    
    cached := val.(*CachedResponse)
    if time.Now().After(cached.ExpiresAt) {
        rc.cache.Delete(key)
        return nil, false
    }
    
    return cached.Data, true
}

func (rc *RequestCache) Set(key string, data []byte, ttl time.Duration) {
    rc.cache.Store(key, &CachedResponse{
        Data:      data,
        ExpiresAt: time.Now().Add(ttl),
    })
}

func main() {
    cache := &RequestCache{}
    
    // Set cache
    cache.Set("api:/users", []byte("user data"), 5*time.Minute)
    
    // Get from cache
    if data, ok := cache.Get(context.Background(), "api:/users"); ok {
        fmt.Println("Cache hit:", string(data))
    }
}
```

---

## Cond - Condition Variables

`Cond` implements a **condition variable** for goroutines waiting for or announcing events. Rarely used in Go - **prefer channels**.

### Basic Structure

```go
type Cond struct {
    L Locker // Usually *Mutex or *RWMutex
    // ...
}
```

### Methods

#### `NewCond(l Locker) *Cond`
Creates a new condition variable.

```go
var mu sync.Mutex
cond := sync.NewCond(&mu)
```

#### `Wait()`
Atomically unlocks `c.L` and suspends execution. When awakened, locks `c.L` before returning.

```go
c.L.Lock()
for !condition() {
    c.Wait()
}
// ... use condition ...
c.L.Unlock()
```

#### `Signal()`
Wakes one waiting goroutine.

```go
c.Signal()
```

#### `Broadcast()`
Wakes all waiting goroutines.

```go
c.Broadcast()
```

### Example: Producer-Consumer

```go
package main

import (
    "fmt"
    "sync"
    "time"
)

type Queue struct {
    mu    sync.Mutex
    cond  *sync.Cond
    items []int
}

func NewQueue() *Queue {
    q := &Queue{
        items: make([]int, 0),
    }
    q.cond = sync.NewCond(&q.mu)
    return q
}

func (q *Queue) Enqueue(item int) {
    q.mu.Lock()
    defer q.mu.Unlock()
    
    q.items = append(q.items, item)
    q.cond.Signal() // Wake one waiting consumer
}

func (q *Queue) Dequeue() int {
    q.mu.Lock()
    defer q.mu.Unlock()
    
    // Wait until items available
    for len(q.items) == 0 {
        q.cond.Wait()
    }
    
    item := q.items[0]
    q.items = q.items[1:]
    return item
}

func main() {
    q := NewQueue()
    
    // Consumer
    go func() {
        for i := 0; i < 5; i++ {
            item := q.Dequeue()
            fmt.Println("Consumed:", item)
        }
    }()
    
    // Producer
    for i := 0; i < 5; i++ {
        time.Sleep(100 * time.Millisecond)
        q.Enqueue(i)
        fmt.Println("Produced:", i)
    }
    
    time.Sleep(time.Second)
}
```

### Why Channels Are Usually Better

```go
// ❌ Complex with Cond
type Queue struct {
    mu    sync.Mutex
    cond  *sync.Cond
    items []int
}

// ✅ Simple with channel
type Queue struct {
    items chan int
}

func NewQueue() *Queue {
    return &Queue{items: make(chan int, 100)}
}

func (q *Queue) Enqueue(item int) {
    q.items <- item
}

func (q *Queue) Dequeue() int {
    return <-q.items
}
```

**Use `Cond` only when:**
- You need broadcast semantics with complex conditions
- Replacing legacy code that uses condition variables
- Channels don't fit the use case

---

## Common Patterns & Best Practices

### Pattern 1: Protecting Shared State

```go
type SafeCounter struct {
    mu    sync.Mutex
    count int
}

func (c *SafeCounter) Inc() {
    c.mu.Lock()
    c.count++
    c.mu.Unlock()
}

func (c *SafeCounter) Value() int {
    c.mu.Lock()
    defer c.mu.Unlock()
    return c.count
}
```

### Pattern 2: Read-Heavy Cache

```go
type Cache struct {
    mu    sync.RWMutex
    items map[string]interface{}
}

func (c *Cache) Get(key string) (interface{}, bool) {
    c.mu.RLock()
    defer c.mu.RUnlock()
    val, ok := c.items[key]
    return val, ok
}

func (c *Cache) Set(key string, val interface{}) {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.items[key] = val
}
```

### Pattern 3: Fan-Out/Fan-In

```go
func fanOutFanIn(input []int) []Result {
    var wg sync.WaitGroup
    results := make([]Result, len(input))
    
    for i, val := range input {
        wg.Add(1)
        go func(index, value int) {
            defer wg.Done()
            results[index] = process(value)
        }(i, val)
    }
    
    wg.Wait()
    return results
}
```

### Pattern 4: Lazy Initialization

```go
type Service struct {
    configOnce sync.Once
    config     *Config
}

func (s *Service) GetConfig() *Config {
    s.configOnce.Do(func() {
        s.config = loadConfig()
    })
    return s.config
}
```

### Pattern 5: Worker Pool

```go
func workerPool(jobs <-chan Job, numWorkers int) <-chan Result {
    var wg sync.WaitGroup
    results := make(chan Result)
    
    for i := 0; i < numWorkers; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            for job := range jobs {
                results <- process(job)
            }
        }()
    }
    
    go func() {
        wg.Wait()
        close(results)
    }()
    
    return results
}
```

---

## Performance Considerations

### Mutex Contention

**Problem**: High contention on a single mutex kills performance.

```go
// ❌ BAD: Single mutex for entire cache
type Cache struct {
    mu    sync.Mutex
    items map[string]Value
}

// ✅ BETTER: Sharded locks
type ShardedCache struct {
    shards [64]struct {
        mu    sync.RWMutex
        items map[string]Value
    }
}

func (c *ShardedCache) shard(key string) *struct {
    mu    sync.RWMutex
    items map[string]Value
} {
    hash := fnv32(key)
    return &c.shards[hash%64]
}

func (c *ShardedCache) Get(key string) (Value, bool) {
    shard := c.shard(key)
    shard.mu.RLock()
    defer shard.mu.RUnlock()
    val, ok := shard.items[key]
    return val, ok
}
```

### Lock-Free Alternatives

For simple counters, use `atomic` instead of mutexes:

```go
import "sync/atomic"

// ❌ Slower with Mutex
type Counter struct {
    mu    sync.Mutex
    count int64
}

func (c *Counter) Inc() {
    c.mu.Lock()
    c.count++
    c.mu.Unlock()
}

// ✅ Faster with atomic
type Counter struct {
    count atomic.Int64
}

func (c *Counter) Inc() {
    c.count.Add(1)
}
```

### Critical Section Size

**Keep critical sections small**:

```go
// ❌ BAD: Large critical section
mu.Lock()
data := fetchData()    // Slow!
result := process(data) // Slow!
mu.Unlock()

// ✅ GOOD: Minimal critical section
data := fetchData()
result := process(data)
mu.Lock()
storeResult(result) // Only this needs lock
mu.Unlock()
```

---

## Real-World Examples

### Example 1: Thread-Safe LRU Cache

```go
package main

import (
    "container/list"
    "sync"
)

type LRUCache struct {
    mu       sync.Mutex
    capacity int
    cache    map[string]*list.Element
    lru      *list.List
}

type entry struct {
    key   string
    value interface{}
}

func NewLRUCache(capacity int) *LRUCache {
    return &LRUCache{
        capacity: capacity,
        cache:    make(map[string]*list.Element),
        lru:      list.New(),
    }
}

func (c *LRUCache) Get(key string) (interface{}, bool) {
    c.mu.Lock()
    defer c.mu.Unlock()
    
    if elem, ok := c.cache[key]; ok {
        c.lru.MoveToFront(elem)
        return elem.Value.(*entry).value, true
    }
    return nil, false
}

func (c *LRUCache) Put(key string, value interface{}) {
    c.mu.Lock()
    defer c.mu.Unlock()
    
    if elem, ok := c.cache[key]; ok {
        c.lru.MoveToFront(elem)
        elem.Value.(*entry).value = value
        return
    }
    
    elem := c.lru.PushFront(&entry{key, value})
    c.cache[key] = elem
    
    if c.lru.Len() > c.capacity {
        oldest := c.lru.Back()
        if oldest != nil {
            c.lru.Remove(oldest)
            delete(c.cache, oldest.Value.(*entry).key)
        }
    }
}
```

### Example 2: Rate Limiter

```go
package main

import (
    "sync"
    "time"
)

type RateLimiter struct {
    mu        sync.Mutex
    rate      int
    tokens    int
    lastRefill time.Time
}

func NewRateLimiter(rate int) *RateLimiter {
    return &RateLimiter{
        rate:      rate,
        tokens:    rate,
        lastRefill: time.Now(),
    }
}

func (rl *RateLimiter) Allow() bool {
    rl.mu.Lock()
    defer rl.mu.Unlock()
    
    now := time.Now()
    elapsed := now.Sub(rl.lastRefill)
    
    // Refill tokens
    tokensToAdd := int(elapsed.Seconds()) * rl.rate
    if tokensToAdd > 0 {
        rl.tokens = min(rl.tokens+tokensToAdd, rl.rate)
        rl.lastRefill = now
    }
    
    if rl.tokens > 0 {
        rl.tokens--
        return true
    }
    
    return false
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
```

### Example 3: Connection Pool

```go
package main

import (
    "errors"
    "sync"
)

type ConnectionPool struct {
    mu      sync.Mutex
    conns   []Connection
    factory func() (Connection, error)
    maxSize int
}

type Connection interface {
    Close() error
}

func NewConnectionPool(factory func() (Connection, error), maxSize int) *ConnectionPool {
    return &ConnectionPool{
        conns:   make([]Connection, 0, maxSize),
        factory: factory,
        maxSize: maxSize,
    }
}

func (p *ConnectionPool) Get() (Connection, error) {
    p.mu.Lock()
    defer p.mu.Unlock()
    
    if len(p.conns) > 0 {
        conn := p.conns[len(p.conns)-1]
        p.conns = p.conns[:len(p.conns)-1]
        return conn, nil
    }
    
    return p.factory()
}

func (p *ConnectionPool) Put(conn Connection) error {
    p.mu.Lock()
    defer p.mu.Unlock()
    
    if len(p.conns) >= p.maxSize {
        return conn.Close()
    }
    
    p.conns = append(p.conns, conn)
    return nil
}

func (p *ConnectionPool) Close() error {
    p.mu.Lock()
    defer p.mu.Unlock()
    
    for _, conn := range p.conns {
        conn.Close()
    }
    p.conns = nil
    return nil
}
```

---

## Related Projects

Apply sync primitives in these projects:
- [Project 2: URL Shortener](../projects/01-basic/project-02-url-shortener.md) - RWMutex for protecting in-memory URL map
- [Project 7: REST API](../projects/02-intermediate/project-07-rest-api.md) - Thread-safe caching
- [Project 10: Web Scraper](../projects/02-intermediate/project-10-web-scraper.md) - WaitGroup for concurrent scraping
- [Project 17: NoSQL API](../projects/02-intermediate/project-17-nosql-api.md) - Connection pooling
- [Project 24: Message Queue](../projects/04-expert/project-24-placeholder.md) - Synchronization for queue operations
- [Project 25: Distributed Cache](../projects/04-expert/project-25-placeholder.md) - RWMutex for cache access

---

## Summary

| Type | Use Case | Key Feature |
|------|----------|-------------|
| **Mutex** | Exclusive access to shared state | Simple lock/unlock |
| **RWMutex** | Read-heavy workloads | Multiple readers OR one writer |
| **WaitGroup** | Wait for goroutines to finish | Counter-based synchronization |
| **Once** | One-time initialization | Guarantees single execution |
| **Pool** | Object reuse | Reduces GC pressure |
| **Map** | Concurrent map operations | Lock-free for some operations |
| **Cond** | Complex wait conditions | Prefer channels instead |

**Golden Rules**:
1. ✅ Never copy sync types after first use
2. ✅ Always use `defer` with `Unlock()`
3. ✅ Keep critical sections small
4. ✅ Prefer channels for communication
5. ✅ Use sync primitives for shared state protection

---

[← Back to Documentation](README.md) | [↑ Back to Index](../MASTER-INDEX.md)
