# Project 24: Message Queue & Event-Driven System

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a complete message queue system with producers, consumers, dead letter queues, and monitoring for event-driven architecture.

**Difficulty:** Expert  
**Estimated Time:** 4-6 weeks  
**Prerequisites:** REST API, Redis projects, understanding of distributed systems

## What You'll Learn

- Message queue patterns
- At-least-once vs exactly-once delivery
- Consumer group balancing
- Message persistence
- Backpressure handling
- Circuit breaker for consumers
- Dead Letter Queue (DLQ)
- Event sourcing patterns

## Core Features

1. **Producer Service:**
   - Publish messages to queue
   - Message serialization (JSON, Protobuf)
   - Batching for performance
   - Confirm delivery
   - Retry with exponential backoff

2. **Consumer Service:**
   - Subscribe to topics/queues
   - Process messages concurrently
   - Acknowledge messages
   - Handle failures (DLQ)
   - Graceful shutdown

3. **Queue Management:**
   - Create/delete queues
   - Configure retention
   - Monitor queue depth
   - Purge messages
   - View DLQ

4. **Use Cases:**
   - Order processing pipeline
   - Email notification system
   - Image processing queue
   - Log aggregation

## RabbitMQ Integration

```go
conn, _ := amqp.Dial("amqp://guest:guest@localhost:5672/")
ch, _ := conn.Channel()

// Declare queue
q, _ := ch.QueueDeclare(
    "tasks",  // name
    true,     // durable
    false,    // delete when unused
    false,    // exclusive
    false,    // no-wait
    nil,      // arguments
)

// Publish message
err := ch.Publish(
    "",      // exchange
    q.Name,  // routing key
    false,   // mandatory
    false,   // immediate
    amqp.Publishing{
        ContentType: "application/json",
        Body:        []byte(message),
    },
)

// Consume messages
msgs, _ := ch.Consume(
    q.Name, // queue
    "",     // consumer
    false,  // auto-ack
    false,  // exclusive
    false,  // no-local
    false,  // no-wait
    nil,    // args
)

for msg := range msgs {
    // Process message
    process(msg.Body)
    msg.Ack(false)
}
```

## Consumer Worker Pool Pattern

```go
type Consumer struct {
    queue   string
    handler MessageHandler
    workers int
}

func (c *Consumer) Start(ctx context.Context) {
    msgs := c.consumeMessages()
    
    // Worker pool
    for i := 0; i < c.workers; i++ {
        go c.worker(ctx, msgs)
    }
}

func (c *Consumer) worker(ctx context.Context, msgs <-chan Message) {
    for {
        select {
        case <-ctx.Done():
            return
        case msg := <-msgs:
            if err := c.handler.Handle(msg); err != nil {
                c.sendToDLQ(msg)
            } else {
                msg.Ack()
            }
        }
    }
}
```

## Project Structure

```
message-queue/
├── producer/
│   ├── producer.go       # Message publisher
│   └── batch.go          # Batch publishing
├── consumer/
│   ├── consumer.go       # Message consumer
│   ├── worker.go         # Worker pool
│   └── handler.go        # Message handlers
├── queue/
│   ├── rabbitmq.go       # RabbitMQ client
│   ├── kafka.go          # Kafka client
│   └── nats.go           # NATS client
├── models/
│   └── message.go        # Message types
├── examples/
│   ├── order/            # Order processing
│   ├── email/            # Email sender
│   └── image/            # Image processor
└── monitoring/
    └── metrics.go        # Queue metrics
```

## Error Handling Strategy

- **Transient errors:** Retry with exponential backoff
- **Permanent errors:** Send to DLQ immediately
- **Max retries exceeded:** Send to DLQ
- **Processing timeout:** Requeue message

## Exchange Types (RabbitMQ)

- **Direct:** Routing key exact match
- **Topic:** Pattern matching (e.g., `logs.*.error`)
- **Fanout:** Broadcast to all queues
- **Headers:** Attribute-based routing

## Full Details

Complete implementation in `golang-learning-projects.md` (search "Project 24"):
- RabbitMQ and Kafka integration
- Consumer patterns and worker pools
- DLQ implementation
- Message retry logic
- Monitoring and metrics
- Real-world use cases

---

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)
