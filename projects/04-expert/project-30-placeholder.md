# Project 30: Authentication & Authorization System

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a complete authentication and authorization system with JWT, OAuth 2.0, role-based access control, and security best practices.

**Difficulty:** Expert  
**Estimated Time:** 4-6 weeks  
**Prerequisites:** REST API project completed, understanding of security concepts, database experience

## What You'll Learn

- JWT token generation and validation
- Refresh token rotation
- OAuth 2.0 flows
- Password hashing best practices
- Permission modeling
- RBAC implementation
- API key management
- Security headers
- Rate limiting per user

## Core Features

1. **Authentication Methods:**
   - Email/password with JWT
   - OAuth 2.0 (Google, GitHub)
   - API keys for services
   - Magic links (passwordless)
   - Two-factor authentication (TOTP)

2. **Authorization:**
   - Role-based access control (RBAC)
   - Permission system
   - Resource-based permissions
   - Attribute-based access control (ABAC)

3. **Security Features:**
   - Password complexity requirements
   - Account lockout after failed attempts
   - Email verification
   - Password reset flow
   - Session management
   - Audit logging

4. **Token Management:**
   - Access token (short-lived, 15min)
   - Refresh token (long-lived, 7 days)
   - Token rotation
   - Token blacklisting
   - JWT claims validation

## JWT Implementation

```go
import "github.com/golang-jwt/jwt/v5"

type Claims struct {
    UserID string   `json:"user_id"`
    Email  string   `json:"email"`
    Roles  []string `json:"roles"`
    jwt.RegisteredClaims
}

func GenerateJWT(userID, email string, roles []string) (string, error) {
    claims := &Claims{
        UserID: userID,
        Email:  email,
        Roles:  roles,
        RegisteredClaims: jwt.RegisteredClaims{
            ExpiresAt: jwt.NewNumericDate(time.Now().Add(15 * time.Minute)),
            IssuedAt:  jwt.NewNumericDate(time.Now()),
            Issuer:    "my-app",
        },
    }
    
    token := jwt.NewWithClaims(jwt.SigningMethodHS256, claims)
    return token.SignedString([]byte(secretKey))
}

func ValidateJWT(tokenString string) (*Claims, error) {
    token, err := jwt.ParseWithClaims(tokenString, &Claims{}, func(token *jwt.Token) (interface{}, error) {
        return []byte(secretKey), nil
    })
    
    if err != nil {
        return nil, err
    }
    
    if claims, ok := token.Claims.(*Claims); ok && token.Valid {
        return claims, nil
    }
    
    return nil, errors.New("invalid token")
}
```

## Password Hashing

```go
import "golang.org/x/crypto/bcrypt"

func HashPassword(password string) (string, error) {
    hash, err := bcrypt.GenerateFromPassword([]byte(password), bcrypt.DefaultCost)
    if err != nil {
        return "", err
    }
    return string(hash), nil
}

func CheckPassword(password, hash string) bool {
    err := bcrypt.CompareHashAndPassword([]byte(hash), []byte(password))
    return err == nil
}
```

## RBAC Middleware

```go
func RequireRole(allowedRoles ...string) func(http.Handler) http.Handler {
    return func(next http.Handler) http.Handler {
        return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
            // Extract JWT from Authorization header
            tokenString := extractToken(r)
            claims, err := ValidateJWT(tokenString)
            if err != nil {
                http.Error(w, "Unauthorized", http.StatusUnauthorized)
                return
            }
            
            // Check if user has required role
            hasRole := false
            for _, userRole := range claims.Roles {
                for _, allowedRole := range allowedRoles {
                    if userRole == allowedRole {
                        hasRole = true
                        break
                    }
                }
            }
            
            if !hasRole {
                http.Error(w, "Forbidden", http.StatusForbidden)
                return
            }
            
            // Add claims to context
            ctx := context.WithValue(r.Context(), "claims", claims)
            next.ServeHTTP(w, r.WithContext(ctx))
        })
    }
}

// Usage
http.Handle("/admin", RequireRole("admin")(adminHandler))
```

## OAuth 2.0 (Google)

```go
import "golang.org/x/oauth2"
import "golang.org/x/oauth2/google"

var googleOAuth = &oauth2.Config{
    ClientID:     os.Getenv("GOOGLE_CLIENT_ID"),
    ClientSecret: os.Getenv("GOOGLE_CLIENT_SECRET"),
    RedirectURL:  "http://localhost:8080/auth/google/callback",
    Scopes: []string{
        "https://www.googleapis.com/auth/userinfo.email",
        "https://www.googleapis.com/auth/userinfo.profile",
    },
    Endpoint: google.Endpoint,
}

func HandleGoogleLogin(w http.ResponseWriter, r *http.Request) {
    state := generateRandomState()
    url := googleOAuth.AuthCodeURL(state)
    http.Redirect(w, r, url, http.StatusTemporaryRedirect)
}

func HandleGoogleCallback(w http.ResponseWriter, r *http.Request) {
    code := r.URL.Query().Get("code")
    
    token, err := googleOAuth.Exchange(context.Background(), code)
    if err != nil {
        http.Error(w, "Failed to exchange token", http.StatusInternalServerError)
        return
    }
    
    // Get user info
    client := googleOAuth.Client(context.Background(), token)
    resp, _ := client.Get("https://www.googleapis.com/oauth2/v2/userinfo")
    defer resp.Body.Close()
    
    var userInfo struct {
        Email string `json:"email"`
        Name  string `json:"name"`
    }
    json.NewDecoder(resp.Body).Decode(&userInfo)
    
    // Create/update user in database
    user := createOrUpdateUser(userInfo.Email, userInfo.Name)
    
    // Generate JWT for our app
    jwt, _ := GenerateJWT(user.ID, user.Email, user.Roles)
    
    // Return JWT to client
    json.NewEncoder(w).Encode(map[string]string{"token": jwt})
}
```

## Database Schema

```sql
CREATE TABLE users (
    id UUID PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255),
    email_verified BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE roles (
    id UUID PRIMARY KEY,
    name VARCHAR(50) UNIQUE NOT NULL
);

CREATE TABLE permissions (
    id UUID PRIMARY KEY,
    name VARCHAR(50) UNIQUE NOT NULL,
    resource VARCHAR(50),
    action VARCHAR(50)
);

CREATE TABLE user_roles (
    user_id UUID REFERENCES users(id),
    role_id UUID REFERENCES roles(id),
    PRIMARY KEY (user_id, role_id)
);

CREATE TABLE role_permissions (
    role_id UUID REFERENCES roles(id),
    permission_id UUID REFERENCES permissions(id),
    PRIMARY KEY (role_id, permission_id)
);

CREATE TABLE refresh_tokens (
    token VARCHAR(255) PRIMARY KEY,
    user_id UUID REFERENCES users(id),
    expires_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Project Structure

```
auth-system/
├── auth/
│   ├── jwt.go            # JWT handling
│   ├── oauth.go          # OAuth flows
│   └── password.go       # Password hashing
├── rbac/
│   ├── roles.go
│   ├── permissions.go
│   └── middleware.go
├── models/
│   ├── user.go
│   ├── role.go
│   └── permission.go
└── providers/
    ├── google.go
    └── github.go
```

## Security Best Practices

**JWT:**
- Use short expiration for access tokens
- Implement refresh token rotation
- Store refresh tokens securely
- Validate all claims
- Use strong signing algorithms (RS256 or HS256)

**Passwords:**
- Minimum 8 characters
- Require complexity (uppercase, lowercase, number, symbol)
- Use bcrypt with cost ≥12
- Rate limit login attempts
- Lock account after 5 failed attempts

**OAuth:**
- Verify state parameter (CSRF protection)
- Use HTTPS only
- Store client secrets securely
- Validate redirect URIs

## Full Details

Complete implementation in `golang-learning-projects.md` (search "Project 30"):
- Complete JWT implementation
- OAuth 2.0 for multiple providers
- Full RBAC system
- Security best practices
- API key management
- 2FA implementation
- Session management

---

[← Back to Expert Projects](README.md) | [↑ Back to Index](../../projects-index.md)
