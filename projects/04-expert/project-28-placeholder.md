# Project 28: gRPC Microservices

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a complete microservices system using gRPC for inter-service communication with API gateway, service discovery, and observability.

**Difficulty:** Expert  
**Estimated Time:** 5-7 weeks  
**Prerequisites:** REST API project, understanding of microservices, Protocol Buffers knowledge

## What You'll Learn

- Protocol Buffers (protobuf)
- gRPC service definition
- Unary RPC calls
- Server streaming
- Client streaming
- Bidirectional streaming
- gRPC interceptors (middleware)
- Error handling in gRPC
- Service mesh integration

## Core Features

1. **Multiple Microservices:**
   - User service (authentication)
   - Product service (catalog)
   - Order service (orders)
   - Notification service (async)

2. **Communication Patterns:**
   - Unary calls (request-response)
   - Server streaming (feed updates)
   - Client streaming (batch upload)
   - Bidirectional (chat, real-time sync)

3. **Infrastructure:**
   - API Gateway (gRPC-Gateway or custom)
   - Service discovery (Consul/etcd)
   - Load balancing (client-side)
   - Distributed tracing (OpenTelemetry)

4. **Production Features:**
   - Authentication with interceptors
   - Rate limiting
   - Circuit breaker
   - Retries with exponential backoff
   - Health checking

## Protocol Buffers Definition

```protobuf
syntax = "proto3";

package user;

option go_package = "github.com/user/service/proto";

service UserService {
  rpc CreateUser(CreateUserRequest) returns (User);
  rpc GetUser(GetUserRequest) returns (User);
  rpc ListUsers(ListUsersRequest) returns (stream User);
  rpc UpdateUserStream(stream UpdateUserRequest) returns (UpdateUserResponse);
}

message User {
  string id = 1;
  string name = 2;
  string email = 3;
  int64 created_at = 4;
}

message CreateUserRequest {
  string name = 1;
  string email = 2;
}

message GetUserRequest {
  string id = 1;
}
```

## gRPC Server Implementation

```go
type userServer struct {
    pb.UnimplementedUserServiceServer
    db *sql.DB
}

func (s *userServer) CreateUser(ctx context.Context, req *pb.CreateUserRequest) (*pb.User, error) {
    user := &pb.User{
        Id:        uuid.New().String(),
        Name:      req.Name,
        Email:     req.Email,
        CreatedAt: time.Now().Unix(),
    }
    
    // Save to database
    _, err := s.db.ExecContext(ctx, 
        "INSERT INTO users (id, name, email) VALUES (?, ?, ?)",
        user.Id, user.Name, user.Email,
    )
    if err != nil {
        return nil, status.Errorf(codes.Internal, "failed to create user: %v", err)
    }
    
    return user, nil
}

func (s *userServer) ListUsers(req *pb.ListUsersRequest, stream pb.UserService_ListUsersServer) error {
    rows, _ := s.db.Query("SELECT id, name, email FROM users")
    defer rows.Close()
    
    for rows.Next() {
        var user pb.User
        rows.Scan(&user.Id, &user.Name, &user.Email)
        
        if err := stream.Send(&user); err != nil {
            return err
        }
    }
    
    return nil
}
```

## gRPC Client

```go
conn, _ := grpc.Dial("localhost:50051", 
    grpc.WithInsecure(),
    grpc.WithBlock(),
)
defer conn.Close()

client := pb.NewUserServiceClient(conn)

user, err := client.CreateUser(context.Background(), &pb.CreateUserRequest{
    Name:  "Alice",
    Email: "alice@example.com",
})
```

## Interceptors (Middleware)

```go
func AuthInterceptor(ctx context.Context, req interface{}, info *grpc.UnaryServerInfo, handler grpc.UnaryHandler) (interface{}, error) {
    // Extract metadata
    md, ok := metadata.FromIncomingContext(ctx)
    if !ok {
        return nil, status.Error(codes.Unauthenticated, "missing metadata")
    }
    
    // Validate token
    token := md.Get("authorization")
    if !isValidToken(token) {
        return nil, status.Error(codes.Unauthenticated, "invalid token")
    }
    
    return handler(ctx, req)
}

server := grpc.NewServer(
    grpc.UnaryInterceptor(AuthInterceptor),
)
```

## Project Structure

```
grpc-microservices/
├── proto/
│   ├── user.proto
│   ├── product.proto
│   ├── order.proto
│   └── notification.proto
├── services/
│   ├── user/
│   │   ├── server.go
│   │   └── handler.go
│   ├── product/
│   ├── order/
│   └── notification/
├── gateway/
│   └── api_gateway.go    # HTTP to gRPC
├── discovery/
│   └── consul.go
└── client/
    └── client.go         # gRPC clients
```

## Streaming Patterns

**Server Streaming:**
- Server sends multiple responses
- Client receives stream
- Use case: Live updates, large result sets

**Client Streaming:**
- Client sends multiple requests
- Server sends single response
- Use case: Batch uploads, aggregation

**Bidirectional:**
- Both send/receive streams
- Full-duplex communication
- Use case: Chat, real-time collaboration

## Full Details

Complete implementation in `golang-learning-projects.md` (search "Project 28"):
- All streaming patterns with code
- Interceptor examples
- Service discovery integration
- Error handling strategies
- gRPC-Gateway setup
- Load balancing
- TLS configuration

---

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)
