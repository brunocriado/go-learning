# Go Goroutines & Concurrency: Complete Guide

A comprehensive guide to goroutines, channels, and concurrent programming in Go.

---

## Table of Contents

1. [Introduction to Concurrency](#introduction-to-concurrency)
2. [What Are Goroutines?](#what-are-goroutines)
3. [The Go Scheduler](#the-go-scheduler)
4. [Creating Goroutines](#creating-goroutines)
5. [Channels](#channels)
6. [Channel Operations](#channel-operations)
7. [Buffered vs Unbuffered Channels](#buffered-vs-unbuffered-channels)
8. [Channel Directions](#channel-directions)
9. [Select Statement](#select-statement)
10. [Synchronization Primitives](#synchronization-primitives)
11. [Common Patterns](#common-patterns)
12. [Best Practices](#best-practices)
13. [Common Pitfalls](#common-pitfalls)
14. [Advanced Topics](#advanced-topics)

---

## Introduction to Concurrency

### Concurrency vs Parallelism

**Concurrency**: Dealing with multiple things at once (structure)  
**Parallelism**: Doing multiple things at once (execution)

**Analogy:**
- **Concurrency**: You're writing an essay while occasionally checking your phone. You're managing two tasks, but only doing one at a time.
- **Parallelism**: You're writing with one hand while eating with the other. You're literally doing two things simultaneously.

**Why the Distinction Matters:**

Concurrent programs can run on a single CPU core by interleaving execution. Parallel programs require multiple CPU cores to truly execute simultaneously.

```go
// Concurrent but not parallel (single core)
// Tasks A and B interleave: A1 -> B1 -> A2 -> B2 -> A3 -> B3

// Parallel (multiple cores)
// Core 1: A1 -> A2 -> A3
// Core 2: B1 -> B2 -> B3 (happening at the same time)
```

**Go's Approach:**

Go makes concurrency easy to express (goroutines, channels) and the runtime handles parallelism automatically based on available CPU cores.

---

## What Are Goroutines?

### Definition

A **goroutine** is a lightweight thread managed by the Go runtime. It's not an OS thread—it's a function executing concurrently with other goroutines in the same address space.

### Key Characteristics

1. **Lightweight**: Start with ~2KB stack (vs 1-2MB for OS threads)
2. **Cheap**: Can create millions of goroutines
3. **Multiplexed**: Many goroutines run on few OS threads
4. **Growable**: Stack grows/shrinks dynamically
5. **Managed**: Scheduled by Go runtime, not OS

### How Goroutines Differ from Threads

| Feature | OS Thread | Goroutine |
|---------|-----------|-----------|
| Stack size | 1-2 MB (fixed) | 2 KB initial (growable) |
| Creation cost | Expensive (~1ms) | Cheap (~2-3µs) |
| Context switch | Expensive (~1-2µs) | Cheap (~0.2µs) |
| Managed by | Operating System | Go Runtime |
| Max instances | ~1,000-10,000 | Millions |

### Under the Hood

**Memory Layout:**
```
┌─────────────────────────────────────┐
│         Program Memory              │
├─────────────────────────────────────┤
│  Goroutine 1 Stack (2KB - 1GB)     │
│  Goroutine 2 Stack (2KB - 1GB)     │
│  Goroutine 3 Stack (2KB - 1GB)     │
│  ...                                │
├─────────────────────────────────────┤
│  Shared Heap (garbage collected)   │
└─────────────────────────────────────┘
```

**Why So Lightweight?**

1. **Dynamic stacks**: Start small, grow as needed
2. **Segmented stacks**: Can be non-contiguous in memory
3. **User-space scheduling**: No kernel involvement
4. **Cooperative scheduling**: Goroutines yield at function calls

---

## The Go Scheduler

### The M:N Scheduler

Go uses an **M:N scheduler**: M goroutines are multiplexed onto N OS threads.

**Components:**

- **G** (Goroutine): The actual goroutine
- **M** (Machine): OS thread
- **P** (Processor): Scheduling context (usually matches CPU cores)

**Diagram:**
```
┌──────────────────────────────────────────┐
│         Go Runtime Scheduler             │
├──────────────────────────────────────────┤
│  P0           P1           P2            │  (Processors)
│  │            │            │             │
│  M0           M1           M2            │  (OS Threads)
│  │            │            │             │
│  G1 -> G2    G3 -> G4    G5 -> G6       │  (Goroutines)
│  │            │            │             │
│  Run Queue   Run Queue   Run Queue      │
└──────────────────────────────────────────┘
```

**How It Works:**

1. **P** (Processor) has a run queue of **G**s (goroutines)
2. **M** (OS thread) binds to a **P** and executes **G**s
3. When a **G** blocks (I/O, syscall), **M** detaches and parks
4. **P** finds or creates another **M** to keep running **G**s
5. When **G** unblocks, it's rescheduled

**Default Number of Ps:**

```go
import "runtime"

// Get number of logical CPUs
numCPU := runtime.NumCPU()

// Set max number of OS threads that can execute simultaneously
runtime.GOMAXPROCS(numCPU) // Default since Go 1.5
```

### Scheduling Decisions

**When does a goroutine yield?**

1. **Function calls**: Checks for preemption
2. **Channel operations**: Send/receive may block
3. **Blocking syscalls**: I/O, sleep, lock contention
4. **Garbage collection**: Stop-the-world pauses
5. **Explicit yield**: `runtime.Gosched()`

**Cooperative vs Preemptive:**

- **Pre Go 1.14**: Cooperative (goroutines must yield)
- **Go 1.14+**: Preemptive (scheduler can interrupt long-running goroutines)

---

## Creating Goroutines

### Basic Syntax

```go
go functionName(args)
```

**The `go` keyword** launches a function as a goroutine.

### Examples

**Example 1: Simple Goroutine**

```go
package main

import (
    "fmt"
    "time"
)

func sayHello() {
    fmt.Println("Hello from goroutine!")
}

func main() {
    // Launch goroutine
    go sayHello()
    
    // Without this sleep, main exits before goroutine runs
    time.Sleep(100 * time.Millisecond)
    
    fmt.Println("Main function ending")
}
```

**Why the sleep?**

The main function is also a goroutine. When `main()` returns, **all goroutines are killed**, even if they haven't finished.

**Example 2: Anonymous Function Goroutine**

```go
func main() {
    // Launch anonymous function as goroutine
    go func() {
        fmt.Println("Anonymous goroutine")
    }()
    
    time.Sleep(100 * time.Millisecond)
}
```

**Example 3: Goroutine with Arguments**

```go
func printNumber(n int) {
    fmt.Println("Number:", n)
}

func main() {
    // Launch 5 goroutines
    for i := 0; i < 5; i++ {
        go printNumber(i)
    }
    
    time.Sleep(100 * time.Millisecond)
}

// Output (order is non-deterministic):
// Number: 3
// Number: 0
// Number: 4
// Number: 1
// Number: 2
```

**⚠️ Common Mistake: Loop Variable Capture**

```go
// ❌ WRONG: All goroutines see the same 'i' (value 5)
for i := 0; i < 5; i++ {
    go func() {
        fmt.Println(i) // Captures variable, not value
    }()
}

// ✅ CORRECT: Pass value as argument
for i := 0; i < 5; i++ {
    go func(n int) {
        fmt.Println(n)
    }(i) // Pass current value
}

// ✅ CORRECT: Create local copy
for i := 0; i < 5; i++ {
    i := i // Shadow outer i
    go func() {
        fmt.Println(i)
    }()
}
```

**Why does the wrong version print 5?**

By the time the goroutine runs, the loop has finished and `i` is 5. All goroutines share the same `i` variable.

---

## Channels

### What Are Channels?

**Channels** are typed conduits for communication between goroutines. They allow goroutines to synchronize and exchange data.

**Philosophy:**

> "Don't communicate by sharing memory; share memory by communicating."

Instead of using locks to protect shared data, use channels to pass data between goroutines.

### Creating Channels

```go
// Create an unbuffered channel of ints
ch := make(chan int)

// Create a buffered channel with capacity 10
ch := make(chan int, 10)

// Channel of strings
messages := make(chan string)

// Channel of custom type
type User struct { Name string }
users := make(chan User)
```

### Zero Value

The zero value of a channel is `nil`. Operations on `nil` channels **block forever**.

```go
var ch chan int // nil channel
ch <- 5         // Blocks forever (deadlock)
<-ch            // Blocks forever (deadlock)
```

---

## Channel Operations

### Send Operation

```go
ch <- value
```

**Behavior:**
- **Unbuffered**: Blocks until another goroutine receives
- **Buffered**: Blocks only if buffer is full

**Example:**

```go
ch := make(chan int)

go func() {
    ch <- 42 // Send value into channel
}()

value := <-ch // Receive value from channel
fmt.Println(value) // 42
```

### Receive Operation

```go
value := <-ch        // Receive and assign
<-ch                 // Receive and discard
value, ok := <-ch    // Receive with closed check
```

**Behavior:**
- **Unbuffered**: Blocks until another goroutine sends
- **Buffered**: Blocks only if buffer is empty
- **Closed**: Returns zero value immediately (`ok` is false)

**Example:**

```go
ch := make(chan int)

go func() {
    ch <- 10
    ch <- 20
    close(ch) // Close channel when done
}()

// Receive until channel is closed
for value := range ch {
    fmt.Println(value)
}
// Output: 10, 20
```

### Close Operation

```go
close(ch)
```

**Rules:**
1. Only the **sender** should close channels
2. Sending to closed channel **panics**
3. Receiving from closed channel returns zero value
4. Can check if channel is closed with two-value receive
5. Closing a `nil` channel **panics**
6. Closing an already-closed channel **panics**

**Example:**

```go
ch := make(chan int, 2)
ch <- 1
ch <- 2
close(ch)

// Receiving from closed channel
v1 := <-ch        // 1 (buffered value)
v2 := <-ch        // 2 (buffered value)
v3 := <-ch        // 0 (zero value, channel closed)
v4, ok := <-ch    // v4=0, ok=false (closed)

// ch <- 3        // PANIC: send on closed channel
// close(ch)      // PANIC: close of closed channel
```

### Checking if Channel is Closed

```go
value, ok := <-ch
if !ok {
    // Channel is closed
}

// Or use range (stops when channel closes)
for value := range ch {
    fmt.Println(value)
}
```

---

## Buffered vs Unbuffered Channels

### Unbuffered Channels (Synchronous)

```go
ch := make(chan int) // No buffer
```

**Characteristics:**
- Sender **blocks** until receiver is ready
- Receiver **blocks** until sender is ready
- Provides synchronization (rendezvous)
- Zero capacity

**Use case:** Synchronization, guaranteed delivery

**Example:**

```go
func main() {
    ch := make(chan int)
    
    // This would deadlock (no receiver yet)
    // ch <- 42
    
    go func() {
        value := <-ch // Receiver ready
        fmt.Println(value)
    }()
    
    ch <- 42 // Sender blocks until receiver takes value
}
```

### Buffered Channels (Asynchronous)

```go
ch := make(chan int, 3) // Buffer size 3
```

**Characteristics:**
- Sender blocks only when buffer is **full**
- Receiver blocks only when buffer is **empty**
- Can send multiple values without blocking
- Capacity specified at creation

**Use case:** Producer-consumer, rate limiting, batching

**Example:**

```go
func main() {
    ch := make(chan int, 3)
    
    // Send without blocking (buffer has space)
    ch <- 1
    ch <- 2
    ch <- 3
    
    // ch <- 4 would block (buffer full)
    
    fmt.Println(<-ch) // 1
    fmt.Println(<-ch) // 2
    fmt.Println(<-ch) // 3
}
```

### Visualizing the Difference

**Unbuffered:**
```
Sender: ----[sends]----[waits for receiver]----
                   ↓
Channel:           [value in transit]
                   ↓
Receiver: ----[waits for sender]----[receives]----
```

**Buffered (size 2):**
```
Sender: ----[sends]----[sends]----[sends]----
              ↓          ↓          ↓
Channel:   [   1   ][   2   ] (full, blocks)
              ↓
Receiver: ----[receives later]----
```

### Choosing Buffer Size

```go
// Unbuffered: Strict synchronization
ch := make(chan int)

// Small buffer: Smooth out bursts
ch := make(chan int, 10)

// Large buffer: Decouple producer/consumer
ch := make(chan int, 1000)

// Match capacity: Known workload
ch := make(chan Task, numWorkers)
```

**Guidelines:**
- Start with **unbuffered** (simplest)
- Add buffer **only when needed** (profiling shows blocking)
- Size buffer based on **use case**:
  - Semaphore: buffer size = max concurrency
  - Rate limiter: buffer size = tokens per interval
  - Work queue: buffer size = expected queue depth

---

## Channel Directions

You can specify if a channel is **send-only** or **receive-only** in function signatures.

### Syntax

```go
// Send-only channel
func producer(ch chan<- int) {
    ch <- 42       // OK
    // val := <-ch // Compile error
}

// Receive-only channel
func consumer(ch <-chan int) {
    val := <-ch    // OK
    // ch <- 42    // Compile error
}

// Bidirectional channel (default)
func middleware(ch chan int) {
    ch <- 42
    val := <-ch
}
```

### Why Use Directional Channels?

1. **Type safety**: Prevents accidental sends/receives
2. **Intent**: Makes function purpose clear
3. **Prevent close misuse**: Can't close receive-only channel

**Example:**

```go
func main() {
    ch := make(chan int) // Bidirectional
    
    go producer(ch)  // Converts to send-only
    consumer(ch)     // Converts to receive-only
}

func producer(out chan<- int) {
    for i := 0; i < 5; i++ {
        out <- i
    }
    close(out) // OK: sender closes
}

func consumer(in <-chan int) {
    for val := range in {
        fmt.Println(val)
    }
    // close(in) // Compile error: can't close receive-only
}
```

---

## Select Statement

The `select` statement lets a goroutine wait on multiple channel operations.

### Basic Syntax

```go
select {
case msg := <-ch1:
    fmt.Println("Received from ch1:", msg)
case msg := <-ch2:
    fmt.Println("Received from ch2:", msg)
case ch3 <- 42:
    fmt.Println("Sent to ch3")
default:
    fmt.Println("No channel ready")
}
```

### How Select Works

1. **Evaluates all cases**
2. If **one or more** cases can proceed, **randomly** picks one
3. If **no cases** ready:
   - With `default`: Executes default
   - Without `default`: **Blocks** until a case is ready

**Why random?** Prevents starvation. If ch1 always ready, ch2 would never be checked.

### Examples

**Example 1: Non-blocking Receive**

```go
select {
case msg := <-ch:
    fmt.Println("Received:", msg)
default:
    fmt.Println("No message ready")
}
```

**Example 2: Timeout Pattern**

```go
select {
case result := <-ch:
    fmt.Println("Got result:", result)
case <-time.After(1 * time.Second):
    fmt.Println("Timeout!")
}
```

**Example 3: Multiple Channels**

```go
func main() {
    ch1 := make(chan string)
    ch2 := make(chan string)
    
    go func() {
        time.Sleep(100 * time.Millisecond)
        ch1 <- "from ch1"
    }()
    
    go func() {
        time.Sleep(200 * time.Millisecond)
        ch2 <- "from ch2"
    }()
    
    // Receive from whichever is ready first
    select {
    case msg1 := <-ch1:
        fmt.Println(msg1)
    case msg2 := <-ch2:
        fmt.Println(msg2)
    }
}
// Output: "from ch1" (because it's ready first)
```

**Example 4: Loop with Select**

```go
func worker(jobs <-chan int, done <-chan bool) {
    for {
        select {
        case job := <-jobs:
            fmt.Println("Processing job:", job)
        case <-done:
            fmt.Println("Worker stopping")
            return
        }
    }
}
```

**Example 5: All Channels Pattern**

```go
// Receive from all channels (order doesn't matter)
for i := 0; i < 2; i++ {
    select {
    case msg1 := <-ch1:
        fmt.Println("ch1:", msg1)
    case msg2 := <-ch2:
        fmt.Println("ch2:", msg2)
    }
}
```

---

## Synchronization Primitives

While channels are the Go way, sometimes you need low-level synchronization.

### sync.Mutex

**Mutual exclusion lock** - only one goroutine can hold it at a time.

```go
import "sync"

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
```

**When to use:**
- Protecting shared state (maps, slices, structs)
- Short critical sections
- Performance-critical code

### sync.RWMutex

**Read-write lock** - multiple readers OR one writer.

```go
type Cache struct {
    mu    sync.RWMutex
    items map[string]string
}

func (c *Cache) Get(key string) string {
    c.mu.RLock() // Multiple readers can hold RLock
    defer c.mu.RUnlock()
    return c.items[key]
}

func (c *Cache) Set(key, value string) {
    c.mu.Lock() // Exclusive lock
    defer c.mu.Unlock()
    c.items[key] = value
}
```

**When to use:**
- Read-heavy workloads
- Expensive reads that don't need exclusive access

### sync.WaitGroup

**Wait for collection of goroutines to finish.**

```go
func main() {
    var wg sync.WaitGroup
    
    for i := 0; i < 5; i++ {
        wg.Add(1) // Increment counter
        
        go func(n int) {
            defer wg.Done() // Decrement when done
            fmt.Println("Goroutine", n)
        }(i)
    }
    
    wg.Wait() // Block until counter is 0
    fmt.Println("All goroutines finished")
}
```

**Rules:**
1. Call `Add()` **before** launching goroutine
2. Call `Done()` **inside** goroutine (use `defer`)
3. Call `Wait()` in main goroutine

**Common Mistake:**

```go
// ❌ WRONG: Add inside goroutine (race condition)
for i := 0; i < 5; i++ {
    go func(n int) {
        wg.Add(1) // May execute after wg.Wait()
        defer wg.Done()
        fmt.Println(n)
    }(i)
}
wg.Wait()

// ✅ CORRECT: Add before launching
for i := 0; i < 5; i++ {
    wg.Add(1)
    go func(n int) {
        defer wg.Done()
        fmt.Println(n)
    }(i)
}
wg.Wait()
```

### sync.Once

**Ensure function executes exactly once**, even with multiple goroutines.

```go
var once sync.Once
var instance *Singleton

func GetInstance() *Singleton {
    once.Do(func() {
        instance = &Singleton{}
        fmt.Println("Initialized!")
    })
    return instance
}

// Call from multiple goroutines - only prints "Initialized!" once
```

**Use cases:**
- Lazy initialization
- One-time setup
- Singleton pattern

### sync.Cond

**Condition variable** - wait for/notify about condition changes.

```go
type Queue struct {
    mu    sync.Mutex
    cond  *sync.Cond
    items []int
}

func NewQueue() *Queue {
    q := &Queue{}
    q.cond = sync.NewCond(&q.mu)
    return q
}

func (q *Queue) Enqueue(item int) {
    q.mu.Lock()
    q.items = append(q.items, item)
    q.cond.Signal() // Wake one waiting goroutine
    q.mu.Unlock()
}

func (q *Queue) Dequeue() int {
    q.mu.Lock()
    defer q.mu.Unlock()
    
    for len(q.items) == 0 {
        q.cond.Wait() // Releases lock and waits
    }
    
    item := q.items[0]
    q.items = q.items[1:]
    return item
}
```

**When to use:** Advanced synchronization (prefer channels)

### sync.Pool

**Object pool** - recycle objects to reduce GC pressure.

```go
var bufferPool = sync.Pool{
    New: func() interface{} {
        return new(bytes.Buffer)
    },
}

func useBuffer() {
    buf := bufferPool.Get().(*bytes.Buffer)
    defer bufferPool.Put(buf)
    
    buf.Reset()
    buf.WriteString("Hello")
    // Use buffer...
}
```

**When to use:** High-allocation code paths (profiling shows GC pressure)

---

## Common Patterns

### 1. Worker Pool

**Problem:** Process many tasks with limited concurrency.

```go
func workerPool(numWorkers int, jobs <-chan int, results chan<- int) {
    var wg sync.WaitGroup
    
    // Start worker goroutines
    for i := 0; i < numWorkers; i++ {
        wg.Add(1)
        go func(id int) {
            defer wg.Done()
            
            // Each worker processes jobs from channel
            for job := range jobs {
                result := processJob(job)
                results <- result
            }
        }(i)
    }
    
    // Wait for all workers to finish
    wg.Wait()
    close(results)
}

func main() {
    jobs := make(chan int, 100)
    results := make(chan int, 100)
    
    // Start worker pool
    go workerPool(5, jobs, results)
    
    // Send jobs
    for i := 0; i < 50; i++ {
        jobs <- i
    }
    close(jobs)
    
    // Collect results
    for result := range results {
        fmt.Println(result)
    }
}

func processJob(job int) int {
    // Simulate work
    time.Sleep(100 * time.Millisecond)
    return job * 2
}
```

### 2. Pipeline

**Problem:** Chain multiple processing stages.

```go
// Stage 1: Generate numbers
func generator(nums ...int) <-chan int {
    out := make(chan int)
    go func() {
        for _, n := range nums {
            out <- n
        }
        close(out)
    }()
    return out
}

// Stage 2: Square numbers
func square(in <-chan int) <-chan int {
    out := make(chan int)
    go func() {
        for n := range in {
            out <- n * n
        }
        close(out)
    }()
    return out
}

// Stage 3: Sum numbers
func sum(in <-chan int) <-chan int {
    out := make(chan int)
    go func() {
        total := 0
        for n := range in {
            total += n
        }
        out <- total
        close(out)
    }()
    return out
}

// Chain pipeline stages
func main() {
    // 1² + 2² + 3² = 14
    nums := generator(1, 2, 3)
    squared := square(nums)
    result := sum(squared)
    
    fmt.Println(<-result) // 14
}
```

### 3. Fan-Out, Fan-In

**Fan-out:** Distribute work to multiple goroutines.  
**Fan-in:** Merge results from multiple goroutines.

```go
// Fan-out: Multiple workers process from same channel
func fanOut(in <-chan int, numWorkers int) []<-chan int {
    channels := make([]<-chan int, numWorkers)
    
    for i := 0; i < numWorkers; i++ {
        channels[i] = worker(in)
    }
    
    return channels
}

func worker(in <-chan int) <-chan int {
    out := make(chan int)
    go func() {
        for n := range in {
            out <- n * n
        }
        close(out)
    }()
    return out
}

// Fan-in: Merge multiple channels into one
func fanIn(channels ...<-chan int) <-chan int {
    out := make(chan int)
    var wg sync.WaitGroup
    
    for _, ch := range channels {
        wg.Add(1)
        go func(c <-chan int) {
            defer wg.Done()
            for n := range c {
                out <- n
            }
        }(ch)
    }
    
    go func() {
        wg.Wait()
        close(out)
    }()
    
    return out
}

func main() {
    in := generator(1, 2, 3, 4, 5)
    
    // Fan-out to 3 workers
    workers := fanOut(in, 3)
    
    // Fan-in results
    results := fanIn(workers...)
    
    for result := range results {
        fmt.Println(result)
    }
}
```

### 4. Cancellation with Context

**Problem:** Stop goroutines when work is no longer needed.

```go
import "context"

func worker(ctx context.Context, id int) {
    for {
        select {
        case <-ctx.Done():
            fmt.Println("Worker", id, "stopping:", ctx.Err())
            return
        default:
            // Do work
            time.Sleep(100 * time.Millisecond)
            fmt.Println("Worker", id, "working")
        }
    }
}

func main() {
    // Create cancellable context
    ctx, cancel := context.WithCancel(context.Background())
    
    // Start workers
    for i := 0; i < 3; i++ {
        go worker(ctx, i)
    }
    
    // Let them work
    time.Sleep(500 * time.Millisecond)
    
    // Cancel all workers
    cancel()
    
    time.Sleep(200 * time.Millisecond)
}
```

### 5. Semaphore

**Problem:** Limit concurrent access to resource.

```go
type Semaphore chan struct{}

func NewSemaphore(maxConcurrency int) Semaphore {
    return make(chan struct{}, maxConcurrency)
}

func (s Semaphore) Acquire() {
    s <- struct{}{} // Blocks when channel full
}

func (s Semaphore) Release() {
    <-s
}

func main() {
    sem := NewSemaphore(3) // Max 3 concurrent
    
    for i := 0; i < 10; i++ {
        go func(id int) {
            sem.Acquire()
            defer sem.Release()
            
            fmt.Println("Goroutine", id, "running")
            time.Sleep(1 * time.Second)
        }(i)
    }
    
    time.Sleep(5 * time.Second)
}
```

### 6. Rate Limiting

**Problem:** Limit rate of operations.

```go
func rateLimiter(rate time.Duration) {
    throttle := time.Tick(rate)
    
    for i := 0; i < 10; i++ {
        <-throttle // Blocks until next tick
        fmt.Println("Request", i, "at", time.Now())
    }
}

func main() {
    rateLimiter(500 * time.Millisecond)
}
```

**Token Bucket Implementation:**

```go
type RateLimiter struct {
    tokens chan struct{}
}

func NewRateLimiter(rps int) *RateLimiter {
    rl := &RateLimiter{
        tokens: make(chan struct{}, rps),
    }
    
    // Refill tokens
    go func() {
        ticker := time.NewTicker(time.Second / time.Duration(rps))
        defer ticker.Stop()
        
        for range ticker.C {
            select {
            case rl.tokens <- struct{}{}:
            default: // Bucket full
            }
        }
    }()
    
    return rl
}

func (rl *RateLimiter) Wait() {
    <-rl.tokens
}

func main() {
    limiter := NewRateLimiter(5) // 5 requests per second
    
    for i := 0; i < 20; i++ {
        limiter.Wait()
        fmt.Println("Request", i)
    }
}
```

---

## Best Practices

### 1. Close Channels from Sender

**Rule:** Only the **sender** should close a channel.

```go
// ✅ CORRECT
func producer(ch chan<- int) {
    for i := 0; i < 10; i++ {
        ch <- i
    }
    close(ch) // Sender closes
}

// ❌ WRONG: Receiver closing
func consumer(ch <-chan int) {
    for n := range ch {
        fmt.Println(n)
    }
    close(ch) // PANIC: receiver can't close
}
```

### 2. Avoid Goroutine Leaks

**Problem:** Goroutines that never terminate.

```go
// ❌ GOROUTINE LEAK
func leak() <-chan int {
    ch := make(chan int)
    go func() {
        ch <- 42 // Blocks forever if no receiver
    }()
    return ch
}

// ✅ FIXED: With timeout
func fixed() <-chan int {
    ch := make(chan int)
    go func() {
        select {
        case ch <- 42:
        case <-time.After(1 * time.Second):
            // Timeout, goroutine exits
        }
    }()
    return ch
}
```

**Detection:** Use `-test.run=XXX -test.bench=. -benchmem -test.memprofile=mem.out`

### 3. Don't Copy Mutexes

**Mutexes must not be copied** after first use.

```go
// ❌ WRONG
type Counter struct {
    mu sync.Mutex
    n  int
}

func (c Counter) Inc() { // Copies Counter (and mutex!)
    c.mu.Lock()
    c.n++
    c.mu.Unlock()
}

// ✅ CORRECT
func (c *Counter) Inc() { // Pointer receiver
    c.mu.Lock()
    c.n++
    c.mu.Unlock()
}
```

### 4. Use defer with Unlocks

**Always** use `defer` to ensure unlocking.

```go
// ✅ CORRECT
func (c *Counter) Inc() {
    c.mu.Lock()
    defer c.mu.Unlock() // Unlocks even if panic
    
    c.n++
    if c.n > 100 {
        panic("too high") // Still unlocks
    }
}

// ❌ WRONG: Could deadlock
func (c *Counter) Inc() {
    c.mu.Lock()
    c.n++
    if c.n > 100 {
        panic("too high") // Lock never released!
    }
    c.mu.Unlock()
}
```

### 5. Keep Critical Sections Small

**Minimize time holding locks.**

```go
// ❌ BAD: Long critical section
func (c *Cache) SlowGet(key string) string {
    c.mu.Lock()
    defer c.mu.Unlock()
    
    value := c.items[key]
    time.Sleep(1 * time.Second) // Holding lock!
    return value
}

// ✅ GOOD: Short critical section
func (c *Cache) FastGet(key string) string {
    c.mu.Lock()
    value := c.items[key]
    c.mu.Unlock()
    
    time.Sleep(1 * time.Second) // Lock released
    return value
}
```

### 6. Channels vs Mutexes

**Use channels when:**
- Passing ownership of data
- Distributing units of work
- Communicating async results

**Use mutexes when:**
- Protecting internal state
- Caching
- Performance-critical paths

```go
// Channel: Passing ownership
func producer() <-chan Work {
    ch := make(chan Work)
    go func() {
        ch <- fetchWork() // Transfer ownership
    }()
    return ch
}

// Mutex: Protecting state
type Cache struct {
    mu    sync.Mutex
    items map[string]int
}
```

---

## Common Pitfalls

### 1. Forgetting to Start Goroutine

```go
// ❌ WRONG: Forgot 'go' keyword
func main() {
    processData() // Blocks main, not concurrent
}

// ✅ CORRECT
func main() {
    go processData() // Runs concurrently
    time.Sleep(1 * time.Second)
}
```

### 2. Deadlock

**All goroutines blocked, program cannot proceed.**

```go
// ❌ DEADLOCK
func main() {
    ch := make(chan int)
    ch <- 42 // Blocks forever (no receiver)
}

// ✅ FIXED
func main() {
    ch := make(chan int)
    go func() {
        fmt.Println(<-ch) // Receiver ready
    }()
    ch <- 42
}
```

### 3. Race Condition

**Multiple goroutines access shared data without synchronization.**

```go
// ❌ RACE CONDITION
var counter int

func increment() {
    counter++ // Read-modify-write not atomic
}

func main() {
    for i := 0; i < 1000; i++ {
        go increment()
    }
    time.Sleep(1 * time.Second)
    fmt.Println(counter) // Unpredictable result
}

// ✅ FIXED with mutex
var (
    counter int
    mu      sync.Mutex
)

func increment() {
    mu.Lock()
    counter++
    mu.Unlock()
}

// ✅ FIXED with atomic
var counter int64

func increment() {
    atomic.AddInt64(&counter, 1)
}
```

**Detect races:** `go run -race main.go`

### 4. Closing Channel Twice

```go
// ❌ PANIC
ch := make(chan int)
close(ch)
close(ch) // PANIC: close of closed channel

// ✅ FIXED: Track if closed
type SafeChannel struct {
    ch     chan int
    closed bool
    mu     sync.Mutex
}

func (sc *SafeChannel) Close() {
    sc.mu.Lock()
    defer sc.mu.Unlock()
    
    if !sc.closed {
        close(sc.ch)
        sc.closed = true
    }
}
```

### 5. Sending to Closed Channel

```go
// ❌ PANIC
ch := make(chan int)
close(ch)
ch <- 42 // PANIC: send on closed channel

// ✅ FIXED: Check with select
select {
case ch <- 42:
    fmt.Println("Sent")
default:
    fmt.Println("Channel closed or full")
}
```

### 6. Not Waiting for Goroutines

```go
// ❌ WRONG: Main exits, kills goroutines
func main() {
    for i := 0; i < 10; i++ {
        go fmt.Println(i)
    }
    // No wait, program exits immediately
}

// ✅ CORRECT: Wait for completion
func main() {
    var wg sync.WaitGroup
    for i := 0; i < 10; i++ {
        wg.Add(1)
        go func(n int) {
            defer wg.Done()
            fmt.Println(n)
        }(i)
    }
    wg.Wait()
}
```

---

## Advanced Topics

### 1. Context Package

**Purpose:** Cancellation, deadlines, request-scoped values.

```go
import "context"

// Cancellation
ctx, cancel := context.WithCancel(context.Background())
defer cancel()

// Timeout
ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
defer cancel()

// Deadline
deadline := time.Now().Add(10 * time.Second)
ctx, cancel := context.WithDeadline(context.Background(), deadline)
defer cancel()

// Values (use sparingly)
ctx = context.WithValue(ctx, "userID", 42)
userID := ctx.Value("userID").(int)
```

**Propagating Context:**

```go
func handler(ctx context.Context) {
    // Pass context to all downstream operations
    result, err := database.Query(ctx, "SELECT ...")
    if err != nil {
        return
    }
    
    // Check if cancelled
    select {
    case <-ctx.Done():
        return // Context cancelled or expired
    default:
        // Continue
    }
}
```

### 2. Atomic Operations

**Lock-free synchronization** using `sync/atomic`.

```go
import "sync/atomic"

var counter int64

// Atomic increment
atomic.AddInt64(&counter, 1)

// Atomic load
value := atomic.LoadInt64(&counter)

// Atomic store
atomic.StoreInt64(&counter, 100)

// Compare-and-swap
swapped := atomic.CompareAndSwapInt64(&counter, 100, 200)
```

**Use cases:** Counters, flags, simple state machines.

### 3. Memory Model

**Go's memory model** defines when one goroutine sees effects of another.

**Happens-Before Rules:**

1. Initialization happens before main
2. Channel send happens before corresponding receive
3. Close happens before receive of closed channel
4. Lock happens before unlock
5. First call to `once.Do(f)` happens before any second call

**Example:**

```go
var a string

func setup() {
    a = "hello"
}

func main() {
    go setup()
    print(a) // May print "" (race)
}

// Fixed with channel
var done = make(chan bool)

func setup() {
    a = "hello"
    done <- true
}

func main() {
    go setup()
    <-done
    print(a) // Guaranteed to print "hello"
}
```

### 4. Profiling Goroutines

**See active goroutines:**

```go
import (
    "net/http"
    _ "net/http/pprof"
    "runtime"
)

func main() {
    // Start pprof server
    go http.ListenAndServe("localhost:6060", nil)
    
    // Your program...
}

// In browser: http://localhost:6060/debug/pprof/goroutine
// Or: go tool pprof http://localhost:6060/debug/pprof/goroutine
```

**Count goroutines:**

```go
numGoroutines := runtime.NumGoroutine()
fmt.Println("Active goroutines:", numGoroutines)
```

### 5. Preemptive Scheduling (Go 1.14+)

**Before Go 1.14:** Goroutines only yielded at function calls, channel operations, or syscalls.

**Problem:**

```go
// Pre-1.14: This goroutine never yields
func cpuBound() {
    for {
        // Tight loop, no function calls
    }
}
```

**Go 1.14+:** Scheduler can preempt long-running goroutines.

**How:** Signal-based preemption checks every 10ms.

---

## Summary

### Key Takeaways

1. **Goroutines** are lightweight, cheap to create
2. **Channels** provide synchronization and communication
3. **Select** multiplexes channel operations
4. **Mutexes** protect shared state when channels don't fit
5. **WaitGroups** coordinate goroutine completion
6. **Context** manages cancellation and deadlines
7. **Don't communicate by sharing memory; share memory by communicating**

### Decision Tree

```
Need concurrency?
├─ Passing data between goroutines?
│  └─ Use channels
├─ Protecting shared state?
│  └─ Use mutex/RWMutex
├─ Waiting for goroutines?
│  └─ Use WaitGroup
├─ Cancellation/timeout?
│  └─ Use context.Context
├─ One-time initialization?
│  └─ Use sync.Once
└─ Limiting concurrency?
   └─ Use buffered channel (semaphore)
```

### Further Reading

- [Effective Go - Concurrency](https://go.dev/doc/effective_go#concurrency)
- [Go Memory Model](https://go.dev/ref/mem)
- [Go Concurrency Patterns (video)](https://www.youtube.com/watch?v=f6kdp27TYZs)
- [Advanced Go Concurrency Patterns (video)](https://www.youtube.com/watch?v=QDDwwePbDtw)

---

**Last Updated:** January 4, 2026  
**Go Version:** 1.21+  
**Maintained By:** Community

