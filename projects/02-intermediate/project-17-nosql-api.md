# Project 17: NoSQL Database API (MongoDB/Redis)

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a RESTful API using NoSQL databases (MongoDB and Redis). Learn document storage, caching strategies, and NoSQL design patterns.

**Difficulty:** Intermediate  
**Estimated Time:** 30-45 hours

## Prerequisites

**Required Packages:**
```bash
go get go.mongodb.org/mongo-driver/mongo
go get github.com/go-redis/redis/v8
```

## What You'll Learn

- MongoDB CRUD operations
- Redis caching strategies
- Cache-aside pattern
- Write-through caching
- Indexing strategies
- Aggregation pipelines
- Data modeling for NoSQL

## Implementation Guide

```go
package main

import (
    "context"
    "github.com/go-redis/redis/v8"
    "go.mongodb.org/mongo-driver/mongo"
    "go.mongodb.org/mongo-driver/mongo/options"
)

type UserService struct {
    mongo *mongo.Collection
    redis *redis.Client
}

func NewUserService() *UserService {
    // MongoDB
    mongoClient, _ := mongo.Connect(context.Background(), 
        options.Client().ApplyURI("mongodb://localhost:27017"))
    collection := mongoClient.Database("myapp").Collection("users")
    
    // Redis
    redisClient := redis.NewClient(&redis.Options{
        Addr: "localhost:6379",
    })
    
    return &UserService{
        mongo: collection,
        redis: redisClient,
    }
}

func (s *UserService) GetUser(ctx context.Context, id string) (*User, error) {
    // Try cache first
    cached, err := s.redis.Get(ctx, "user:"+id).Result()
    if err == nil {
        var user User
        json.Unmarshal([]byte(cached), &user)
        return &user, nil
    }
    
    // Cache miss, query MongoDB
    var user User
    err = s.mongo.FindOne(ctx, bson.M{"_id": id}).Decode(&user)
    if err != nil {
        return nil, err
    }
    
    // Store in cache
    data, _ := json.Marshal(user)
    s.redis.Set(ctx, "user:"+id, data, 5*time.Minute)
    
    return &user, nil
}

func (s *UserService) CreateUser(ctx context.Context, user *User) error {
    _, err := s.mongo.InsertOne(ctx, user)
    if err != nil {
        return err
    }
    
    // Invalidate cache
    s.redis.Del(ctx, "user:"+user.ID)
    
    return nil
}
```

## Project Structure

```
nosql-api/
├── main.go
├── handlers/
│   └── users.go
├── services/
│   ├── user_service.go
│   └── cache.go
├── models/
│   └── user.go
└── README.md
```

## Next Steps

- Add session management
- Implement pub/sub with Redis
- Create aggregation pipelines
- Move to [Project 18: OpenSearch](project-18-opensearch.md)

---

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)
