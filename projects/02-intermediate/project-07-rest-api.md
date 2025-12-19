# Project 7: REST API with Database

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)

---

## Prerequisites & Requirements

**Before Starting:**
- **Completed**: Basic projects (especially Project 2: URL Shortener)
- Built HTTP servers in Go
- Worked with databases
- Understand REST API principles

**Knowledge Prerequisites:**
- **Must Know**: HTTP methods, JSON, structs, goroutines, SQL basics
- **Will Learn**: database/sql, JWT authentication, middleware, migrations

**External Dependencies:**
- `github.com/gorilla/mux` - HTTP router
- `github.com/lib/pq` (PostgreSQL) OR `github.com/mattn/go-sqlite3` (SQLite)
- `github.com/golang-jwt/jwt/v5` - JWT tokens
- `github.com/joho/godotenv` - Load .env files
- `golang.org/x/crypto/bcrypt` - Password hashing
- `github.com/go-playground/validator/v10` - Input validation

**Estimated Time:** 20-30 hours

---

## Overview

Build a full-featured REST API for a blog application with PostgreSQL/SQLite backend, user authentication, and proper API design.

### What You'll Learn

- **Database/SQL**: Work with relational databases
- **JWT Authentication**: Stateless authentication tokens
- **Middleware**: Authentication, logging, CORS, rate limiting
- **Request Validation**: Input validation and sanitization
- **Database Migrations**: Version control for schema
- **Testing**: Unit and integration tests

### Core Features

1. User registration and login with JWT
2. CRUD operations for blog posts/notes
3. User-specific content
4. Search and filtering
5. Pagination
6. Input validation and error handling
7. Rate limiting
8. Database migrations

---

## Project Structure

```
blog-api/
├── main.go                 # Entry point
├── config/config.go        # Configuration
├── models/
│   ├── user.go            # User model
│   └── post.go            # Post model
├── handlers/
│   ├── auth.go            # Register, login
│   ├── posts.go           # Post CRUD
│   └── users.go           # User management
├── middleware/
│   ├── auth.go            # JWT validation
│   ├── logger.go          # Request logging
│   └── ratelimit.go       # Rate limiting
├── database/
│   ├── database.go        # DB connection
│   └── migrations/        # SQL files
├── utils/
│   ├── jwt.go             # JWT helpers
│   └── validator.go       # Validation
├── go.mod
└── .env                   # Configuration
```

---

## Implementation Guide

### Step 1: Database Models

**`models/user.go`:**
- User struct: ID, Username, Email, PasswordHash, CreatedAt, UpdatedAt
- Methods: Create, GetByID, GetByEmail, Update, Delete, ValidatePassword

**`models/post.go`:**
- Post struct: ID, UserID, Title, Content, Published, CreatedAt, UpdatedAt
- Methods: Create, GetByID, GetAll, GetByUser, Update, Delete, Search

**Hints:**
- Always use parameterized queries (`?` placeholders)
- Hash passwords with bcrypt before storing
- Use `defer rows.Close()` for queries

### Step 2: Authentication

**JWT Token Generation:**
- Generate tokens with user ID and expiration
- Use secret key from environment variable
- Return token to client

**Register Handler:**
- Validate input (email format, password strength)
- Check if user already exists
- Hash password
- Create user in database

**Login Handler:**
- Find user by email
- Validate password
- Generate JWT token
- Return token and user info

### Step 3: Middleware

**Auth Middleware:**
- Extract token from Authorization header
- Validate token
- Store user ID in request context
- Return 401 if invalid

**Logger Middleware:**
- Log request method, path, IP
- Log response status and duration

**Rate Limit Middleware:**
- Track requests per IP
- Limit to N requests per minute
- Return 429 if exceeded

### Step 4: Post Handlers

**CRUD Operations:**
- CreatePost: Auth required, validate input
- GetPosts: Pagination, filtering
- GetPost: Return single post
- UpdatePost: Check ownership
- DeletePost: Check ownership

**Hints:**
- Get URL params: `mux.Vars(r)["id"]`
- Parse JSON body: `json.NewDecoder(r.Body).Decode(&struct)`
- Check ownership: `if post.UserID != userID { return 403 }`

### Step 5: Database Migrations

**001_initial.sql:**
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE posts (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    title VARCHAR(200) NOT NULL,
    content TEXT,
    published BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## Testing

```bash
# Register user
curl -X POST http://localhost:8080/api/register \
  -H "Content-Type: application/json" \
  -d '{"username":"john","email":"john@example.com","password":"secret123"}'

# Login
curl -X POST http://localhost:8080/api/login \
  -H "Content-Type: application/json" \
  -d '{"email":"john@example.com","password":"secret123"}'

# Create post (use token from login)
curl -X POST http://localhost:8080/api/posts \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -d '{"title":"My Post","content":"Hello!","published":true}'
```

---

## Challenge Yourself

1. **Comments System**: Add comments on posts
2. **File Uploads**: Store images for posts
3. **Email Verification**: Send confirmation email
4. **Password Reset**: Forgot password flow
5. **OAuth**: Login with Google/GitHub
6. **WebSockets**: Real-time notifications
7. **Caching**: Add Redis caching
8. **Full-Text Search**: PostgreSQL search
9. **API Versioning**: Support v1, v2 APIs
10. **GraphQL**: Build GraphQL API

---

## Common Gotchas

**Problem**: SQL injection vulnerability  
**Fix**: Always use parameterized queries

**Problem**: Password in plain text  
**Fix**: Use bcrypt.GenerateFromPassword()

**Problem**: JWT never expires  
**Fix**: Set expiration claim, validate

**Problem**: Database connection leaks  
**Fix**: defer rows.Close()

---

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)
