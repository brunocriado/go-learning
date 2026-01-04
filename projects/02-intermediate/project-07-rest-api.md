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

## 📋 Task Checklist

Use this checklist to guide your implementation. Check off tasks as you complete them. **Remember**: These are guidance tasks, not solutions. Research and figure out the implementation details yourself.

### Phase 1: Project Setup & Database Foundation
- [ ] **Task 1.1**: Initialize Go module and create project directory structure
- [ ] **Task 1.2**: Install dependencies: `gorilla/mux`, `lib/pq`, `golang-jwt/jwt/v5`, `bcrypt`, `validator`
- [ ] **Task 1.3**: Create `.env` file for configuration (DB connection, JWT secret, port)
- [ ] **Task 1.4**: Research `godotenv` package - how to load environment variables?
- [ ] **Task 1.5**: Create `config/config.go` to load and validate configuration
- [ ] **Task 1.6**: Research PostgreSQL vs SQLite - which to use for learning?
- [ ] **Task 1.7**: Install and start PostgreSQL locally OR use SQLite
- [ ] **Task 1.8**: Create database and test connection
- [ ] **Task 1.9**: Research `database/sql` package - how does connection pooling work?
- [ ] **Task 1.10**: Implement `database/database.go` with connection setup
- [ ] **Task 1.11**: Add `Ping()` to verify database connection on startup

### Phase 2: Database Migrations
- [ ] **Task 2.1**: Research database migrations - why version control your schema?
- [ ] **Task 2.2**: Create `database/migrations/` directory
- [ ] **Task 2.3**: Write `001_create_users_table.sql` migration
- [ ] **Task 2.4**: Research SQL constraints - UNIQUE, NOT NULL, PRIMARY KEY, FOREIGN KEY
- [ ] **Task 2.5**: Write `002_create_posts_table.sql` with foreign key to users
- [ ] **Task 2.6**: Research ON DELETE CASCADE - what does it mean?
- [ ] **Task 2.7**: Implement migration runner in `database/migrations.go`
- [ ] **Task 2.8**: Add migration tracking table (which migrations have run)
- [ ] **Task 2.9**: Run migrations on application startup
- [ ] **Task 2.10**: Test: Drop database, restart app, verify tables created

### Phase 3: User Model & Authentication (`models/user.go`)
- [ ] **Task 3.1**: Define `User` struct with all fields (ID, Username, Email, PasswordHash, CreatedAt, UpdatedAt)
- [ ] **Task 3.2**: Add JSON tags for API responses (omit PasswordHash!)
- [ ] **Task 3.3**: Research `bcrypt` package - how does password hashing work?
- [ ] **Task 3.4**: Implement `HashPassword()` helper function
- [ ] **Task 3.5**: Implement `ValidatePassword()` to compare hash with plain text
- [ ] **Task 3.6**: Implement `CreateUser(db, user)` - insert into database
- [ ] **Task 3.7**: Handle duplicate email/username errors from database
- [ ] **Task 3.8**: Implement `GetUserByEmail(db, email)` with prepared statement
- [ ] **Task 3.9**: Research SQL injection - why parameterized queries?
- [ ] **Task 3.10**: Implement `GetUserByID(db, id)`
- [ ] **Task 3.11**: Test user creation and retrieval manually

### Phase 4: JWT Authentication (`utils/jwt.go`)
- [ ] **Task 4.1**: Research JWT tokens - structure (header, payload, signature)
- [ ] **Task 4.2**: What claims should you include? (userID, exp, iat)
- [ ] **Task 4.3**: Implement `GenerateToken(userID)` function
- [ ] **Task 4.4**: Research token expiration - how long should tokens live?
- [ ] **Task 4.5**: Implement `ValidateToken(tokenString)` function
- [ ] **Task 4.6**: Extract user ID from validated token
- [ ] **Task 4.7**: Handle expired tokens gracefully
- [ ] **Task 4.8**: Research signing algorithms - HS256 vs RS256
- [ ] **Task 4.9**: Store JWT secret in environment variable
- [ ] **Task 4.10**: Test token generation and validation manually

### Phase 5: Auth Handlers (`handlers/auth.go`)
- [ ] **Task 5.1**: Define `RegisterRequest` struct (Username, Email, Password)
- [ ] **Task 5.2**: Define `LoginRequest` struct (Email, Password)
- [ ] **Task 5.3**: Define `AuthResponse` struct (Token, User)
- [ ] **Task 5.4**: Research `validator` package - how to validate struct fields?
- [ ] **Task 5.5**: Implement input validation - email format, password length
- [ ] **Task 5.6**: Implement `RegisterHandler()` - validate, hash password, create user
- [ ] **Task 5.7**: Return JWT token in registration response
- [ ] **Task 5.8**: Implement `LoginHandler()` - find user, validate password
- [ ] **Task 5.9**: Return error if user not found or password incorrect
- [ ] **Task 5.10**: Return JWT token in login response
- [ ] **Task 5.11**: Test registration with duplicate email - should fail
- [ ] **Task 5.12**: Test login with wrong password - should fail

### Phase 6: Auth Middleware (`middleware/auth.go`)
- [ ] **Task 6.1**: Research `context` package - how to pass data through middleware?
- [ ] **Task 6.2**: Implement `AuthMiddleware()` wrapper function
- [ ] **Task 6.3**: Extract token from `Authorization: Bearer <token>` header
- [ ] **Task 6.4**: Handle missing Authorization header
- [ ] **Task 6.5**: Validate token and extract user ID
- [ ] **Task 6.6**: Store user ID in request context
- [ ] **Task 6.7**: Research context keys - why use custom type?
- [ ] **Task 6.8**: Helper function: `GetUserIDFromContext(ctx)`
- [ ] **Task 6.9**: Return 401 Unauthorized if token invalid
- [ ] **Task 6.10**: Test middleware with valid and invalid tokens

### Phase 7: Post Model (`models/post.go`)
- [ ] **Task 7.1**: Define `Post` struct (ID, UserID, Title, Content, Published, CreatedAt, UpdatedAt)
- [ ] **Task 7.2**: Add JSON tags for API responses
- [ ] **Task 7.3**: Implement `CreatePost(db, post)` - insert into database
- [ ] **Task 7.4**: Set CreatedAt and UpdatedAt automatically
- [ ] **Task 7.5**: Implement `GetPostByID(db, id)` 
- [ ] **Task 7.6**: Implement `GetAllPosts(db, limit, offset)` for pagination
- [ ] **Task 7.7**: Research SQL LIMIT and OFFSET - how does pagination work?
- [ ] **Task 7.8**: Implement `GetPostsByUser(db, userID, limit, offset)`
- [ ] **Task 7.9**: Implement `UpdatePost(db, post)` - update by ID
- [ ] **Task 7.10**: Implement `DeletePost(db, id)`
- [ ] **Task 7.11**: Add `CountPosts(db)` for total count (pagination metadata)
- [ ] **Task 7.12**: Test all post operations manually

### Phase 8: Post Handlers (`handlers/posts.go`)
- [ ] **Task 8.1**: Define `CreatePostRequest` struct
- [ ] **Task 8.2**: Define `UpdatePostRequest` struct
- [ ] **Task 8.3**: Define `PostResponse` with pagination metadata
- [ ] **Task 8.4**: Implement `CreatePostHandler()` - require authentication
- [ ] **Task 8.5**: Get user ID from context (from auth middleware)
- [ ] **Task 8.6**: Validate title and content (not empty)
- [ ] **Task 8.7**: Implement `GetPostsHandler()` with pagination
- [ ] **Task 8.8**: Parse query params: `?page=1&limit=10`
- [ ] **Task 8.9**: Calculate offset from page number
- [ ] **Task 8.10**: Implement `GetPostHandler()` - single post by ID
- [ ] **Task 8.11**: Implement `UpdatePostHandler()` - check ownership
- [ ] **Task 8.12**: Verify user owns post before updating
- [ ] **Task 8.13**: Implement `DeletePostHandler()` - check ownership
- [ ] **Task 8.14**: Return 403 Forbidden if user doesn't own post
- [ ] **Task 8.15**: Implement `GetMyPostsHandler()` - current user's posts only
- [ ] **Task 8.16**: Add query filters: `?published=true`

### Phase 9: Routing & Server Setup (`main.go`)
- [ ] **Task 9.1**: Research `gorilla/mux` - why use it over stdlib?
- [ ] **Task 9.2**: Create router with `mux.NewRouter()`
- [ ] **Task 9.3**: Define public routes: POST `/api/register`, POST `/api/login`
- [ ] **Task 9.4**: Define protected routes: require auth middleware
- [ ] **Task 9.5**: Register POST `/api/posts` - create post
- [ ] **Task 9.6**: Register GET `/api/posts` - list posts
- [ ] **Task 9.7**: Register GET `/api/posts/{id}` - get single post
- [ ] **Task 9.8**: Register PUT `/api/posts/{id}` - update post
- [ ] **Task 9.9**: Register DELETE `/api/posts/{id}` - delete post
- [ ] **Task 9.10**: Register GET `/api/me/posts` - current user's posts
- [ ] **Task 9.11**: Apply auth middleware to protected routes
- [ ] **Task 9.12**: Apply logging middleware to all routes
- [ ] **Task 9.13**: Add CORS middleware for cross-origin requests
- [ ] **Task 9.14**: Start server and test all endpoints

### Phase 10: Logging Middleware (`middleware/logger.go`)
- [ ] **Task 10.1**: Implement `LoggerMiddleware()` wrapper
- [ ] **Task 10.2**: Log request method, path, and timestamp
- [ ] **Task 10.3**: Research `time.Since()` for request duration
- [ ] **Task 10.4**: Capture response status code (response writer wrapper)
- [ ] **Task 10.5**: Log response status and duration after handler completes
- [ ] **Task 10.6**: Add request ID for tracing (optional)
- [ ] **Task 10.7**: Format logs as JSON for production (optional)

### Phase 11: Rate Limiting (`middleware/ratelimit.go`)
- [ ] **Task 11.1**: Research rate limiting strategies - token bucket vs sliding window
- [ ] **Task 11.2**: Implement IP-based rate limiting
- [ ] **Task 11.3**: Store request counts in memory (map with mutex)
- [ ] **Task 11.4**: Clean up expired entries periodically
- [ ] **Task 11.5**: Return 429 Too Many Requests if limit exceeded
- [ ] **Task 11.6**: Add `Retry-After` header
- [ ] **Task 11.7**: Make limit configurable (requests per minute)
- [ ] **Task 11.8**: Test rate limiting with rapid requests

### Phase 12: Input Validation (`utils/validator.go`)
- [ ] **Task 12.1**: Research `go-playground/validator` - how to use struct tags?
- [ ] **Task 12.2**: Add validation tags to request structs: `validate:"required,email"`
- [ ] **Task 12.3**: Implement `ValidateStruct(s interface{})` helper
- [ ] **Task 12.4**: Return user-friendly validation error messages
- [ ] **Task 12.5**: Validate email format
- [ ] **Task 12.6**: Validate password strength (min length, complexity)
- [ ] **Task 12.7**: Validate title length (max 200 characters)
- [ ] **Task 12.8**: Test validation with invalid inputs

### Phase 13: Error Handling & Responses
- [ ] **Task 13.1**: Define standard error response format (JSON)
- [ ] **Task 13.2**: Implement `respondWithJSON()` helper
- [ ] **Task 13.3**: Implement `respondWithError()` helper
- [ ] **Task 13.4**: Map database errors to HTTP status codes
- [ ] **Task 13.5**: Handle foreign key constraint violations
- [ ] **Task 13.6**: Return proper status codes: 200, 201, 400, 401, 403, 404, 500
- [ ] **Task 13.7**: Add error messages to help API consumers
- [ ] **Task 13.8**: Never expose internal errors (database, stack traces)

### Phase 14: Testing & Debugging
- [ ] **Task 14.1**: Test user registration - valid input
- [ ] **Task 14.2**: Test registration with duplicate email
- [ ] **Task 14.3**: Test login with correct credentials
- [ ] **Task 14.4**: Test login with wrong password
- [ ] **Task 14.5**: Test creating post without authentication (should fail)
- [ ] **Task 14.6**: Test creating post with authentication
- [ ] **Task 14.7**: Test pagination - different page sizes
- [ ] **Task 14.8**: Test updating someone else's post (should fail)
- [ ] **Task 14.9**: Test deleting post (ownership check)
- [ ] **Task 14.10**: Test rate limiting - exceed limit
- [ ] **Task 14.11**: Test with invalid JWT token
- [ ] **Task 14.12**: Test with expired JWT token
- [ ] **Task 14.13**: Verify database migrations run correctly
- [ ] **Task 14.14**: Check for SQL injection vulnerabilities
- [ ] **Task 14.15**: Test concurrent requests for race conditions
- [ ] **Task 14.16**: Run with `-race` flag to detect race conditions

### Phase 15: Advanced Features (Optional)
- [ ] **Task 15.1**: Add search functionality - search posts by title/content
- [ ] **Task 15.2**: Research full-text search in PostgreSQL
- [ ] **Task 15.3**: Add post filtering: `?published=true&user_id=5`
- [ ] **Task 15.4**: Add sorting: `?sort_by=created_at&order=desc`
- [ ] **Task 15.5**: Implement password reset flow
- [ ] **Task 15.6**: Add email verification on registration
- [ ] **Task 15.7**: Implement refresh tokens (long-lived)
- [ ] **Task 15.8**: Add user profile endpoints (GET, PUT `/api/users/{id}`)
- [ ] **Task 15.9**: Add post categories or tags
- [ ] **Task 15.10**: Implement comments system

### Bonus Challenges
- [ ] **Bonus 1**: Write unit tests for handlers using `httptest`
- [ ] **Bonus 2**: Write integration tests for database operations
- [ ] **Bonus 3**: Add database transaction support for complex operations
- [ ] **Bonus 4**: Implement soft deletes (deleted_at field)
- [ ] **Bonus 5**: Add Redis caching for frequently accessed posts
- [ ] **Bonus 6**: Implement API versioning (v1, v2 routes)
- [ ] **Bonus 7**: Add Swagger/OpenAPI documentation
- [ ] **Bonus 8**: Dockerize the application
- [ ] **Bonus 9**: Deploy to cloud (Heroku, Railway, AWS)
- [ ] **Bonus 10**: Add observability (Prometheus metrics, tracing)

---

## 🤔 Debugging Questions to Ask Yourself

**Database & SQL:**
- What's the difference between `Query()` and `QueryRow()`?
- When should you use `Exec()` vs `Query()`?
- Why must you always close `rows` with `defer rows.Close()`?
- What happens if you don't use parameterized queries?
- How does connection pooling improve performance?

**Authentication & Security:**
- Why hash passwords instead of storing plain text?
- What's the difference between authentication and authorization?
- How does JWT differ from session-based auth?
- What should you include in JWT claims?
- Where should you store JWT tokens on the client?

**Middleware & Context:**
- How does middleware chaining work?
- Why use `context.Context` to pass user ID?
- What happens if middleware calls `next.ServeHTTP()` twice?
- How do you apply middleware to specific routes only?

**API Design:**
- What's the difference between PUT and PATCH?
- When should you return 201 vs 200?
- What's idempotency and why does it matter?
- How do you handle partial updates?
- What are best practices for pagination?

**Error Handling:**
- Should you expose internal errors to API consumers?
- How do you distinguish between client errors (4xx) and server errors (5xx)?
- What information should error responses include?
- How do you handle database constraint violations gracefully?

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
