# Project 22: Design Patterns Library & Demo System

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a comprehensive library demonstrating all major design patterns with real-world examples. Your design patterns handbook in code.

**Difficulty:** Expert  
**Estimated Time:** 4-6 weeks (implement 3-4 patterns per week)  
**Prerequisites:** 10+ completed projects, strong understanding of interfaces

## What You'll Learn

- 23 classic design patterns + Go-specific patterns
- When and why to use each pattern
- Go-idiomatic implementations
- Trade-offs and alternatives
- Testing patterns
- Pattern combinations
- Anti-patterns to avoid

## Core Pattern Categories

1. **Creational Patterns** (6): Object creation mechanisms
   - Singleton, Factory, Abstract Factory, Builder, Prototype, Object Pool

2. **Structural Patterns** (7): Object composition
   - Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy

3. **Behavioral Patterns** (11): Object communication
   - Chain of Responsibility, Command, Iterator, Mediator, Memento
   - Observer, State, Strategy, Template Method, Visitor, Interpreter

4. **Concurrency Patterns** (5): Go-specific concurrent designs
   - Worker Pool, Pipeline, Fan-In/Out, Circuit Breaker, Semaphore

5. **Architectural Patterns** (4): High-level structures
   - MVC, Repository, Dependency Injection, Event Sourcing

## Key Implementations

### Creational - Singleton Pattern
```go
type Logger struct{}
var instance *Logger
var once sync.Once

func GetLogger() *Logger {
    once.Do(func() {
        instance = &Logger{}
    })
    return instance
}
```

### Structural - Decorator Pattern
```go
type Handler interface {
    Handle(req Request) Response
}

type LoggingDecorator struct {
    next Handler
}

func (l *LoggingDecorator) Handle(req Request) Response {
    log.Printf("Request: %v", req)
    resp := l.next.Handle(req)
    log.Printf("Response: %v", resp)
    return resp
}
```

### Behavioral - Strategy Pattern
```go
type PaymentStrategy interface {
    Pay(amount float64) error
}

type CreditCard struct{}
func (c *CreditCard) Pay(amount float64) error { /* ... */ }

type PayPal struct{}
func (p *PayPal) Pay(amount float64) error { /* ... */ }

type Checkout struct {
    strategy PaymentStrategy
}
```

### Concurrency - Worker Pool
```go
type WorkerPool struct {
    jobs    chan Job
    results chan Result
    workers int
}

func (wp *WorkerPool) Start() {
    for i := 0; i < wp.workers; i++ {
        go wp.worker()
    }
}

func (wp *WorkerPool) worker() {
    for job := range wp.jobs {
        result := job.Execute()
        wp.results <- result
    }
}
```

## Project Structure

```
design-patterns/
├── cmd/demo/             # Interactive demo CLI
├── patterns/
│   ├── creational/
│   ├── structural/
│   ├── behavioral/
│   ├── concurrency/
│   └── architectural/
├── examples/             # Real-world usage
└── docs/                 # Pattern documentation
```

## Learning Path

**Week 1-2:** Creational patterns + project setup  
**Week 3-4:** Structural patterns with real examples  
**Week 5:** Behavioral patterns (commonly used)  
**Week 6:** Behavioral (advanced) + Concurrency patterns  
**Week 7:** Architectural patterns + demo app  
**Week 8:** Polish, refactor previous projects with patterns

## Key Principles

- Favor composition over inheritance
- Program to interfaces, not implementations
- Encapsulate what varies
- Open/closed principle
- YAGNI: Don't over-engineer

## Full Details

Complete implementation in `golang-learning-projects.md` (search "Project 22" or around line 9500-11500):
- All 23+ patterns with code
- Real-world examples for each
- Testing strategies
- When to use / when NOT to use
- Anti-patterns to avoid
- Pattern combinations

---

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)
