# Go `crypto/md5` Package: Complete Guide

A comprehensive reference for Go's `crypto/md5` package - understanding hash functions, checksums, and the MD5 algorithm.

---

## Table of Contents

1. [Introduction](#introduction)
2. [What is MD5?](#what-is-md5)
3. [What are Hash Functions?](#what-are-hash-functions)
4. [Understanding the hash.Hash Interface](#understanding-the-hashhash-interface)
5. [Package Constants](#package-constants)
6. [Package Functions](#package-functions)
7. [Basic Usage Patterns](#basic-usage-patterns)
8. [Common Use Cases](#common-use-cases)
9. [Security Considerations](#security-considerations)
10. [Alternatives to MD5](#alternatives-to-md5)
11. [Best Practices](#best-practices)

---

## Introduction

The `crypto/md5` package implements the MD5 hash algorithm as defined in RFC 1321.

### Official Documentation

- **crypto/md5 Package**: https://pkg.go.dev/crypto/md5
- **hash Package**: https://pkg.go.dev/hash
- **RFC 1321 (MD5 Specification)**: https://rfc-editor.org/rfc/rfc1321.html

### What is this Package For?

The `crypto/md5` package provides:
- MD5 hash computation
- Checksum generation
- Data fingerprinting
- File integrity verification (in non-security contexts)

### ⚠️ Critical Security Warning

**MD5 is cryptographically broken and should NOT be used for secure applications.**

From the official documentation:
> "MD5 is cryptographically broken and should not be used for secure applications."

**Do NOT use MD5 for:**
- ❌ Password hashing
- ❌ Digital signatures
- ❌ Security-critical checksums
- ❌ Certificate verification
- ❌ Any cryptographic purpose

**Acceptable uses (non-security):**
- ✅ Non-cryptographic checksums
- ✅ Data deduplication
- ✅ Cache keys
- ✅ Hash tables (where collision is acceptable)
- ✅ Legacy system compatibility

---

## What is MD5?

### MD5 Overview

**MD5 (Message-Digest Algorithm 5)** is a widely used hash function that produces a 128-bit (16-byte) hash value, typically expressed as a 32-character hexadecimal number.

**Key characteristics:**
- **Fixed output size**: Always 128 bits (16 bytes)
- **Deterministic**: Same input always produces same output
- **Fast**: Designed for speed
- **One-way**: Cannot reverse the hash to get original data
- **Broken**: Collision attacks are practical (since 2004)

### What MD5 Produces

```
Input:  "Hello, World!"
MD5:    65a8e27d8879283831b664bd8b7f0ad4

Input:  "Hello, World!!"  (note extra !)
MD5:    f6d46b0adfd99d3b7eb03e89e8c77028

Input:  <1GB file>
MD5:    Always 32 hex chars (16 bytes)
```

**Properties:**
- Small input change → completely different hash (avalanche effect)
- Any size input → fixed 16-byte output
- Fast to compute
- Infeasible to reverse (one-way function)

### MD5 vs Other Hashes

| Algorithm | Output Size | Speed | Security | Use Case |
|-----------|-------------|-------|----------|----------|
| **MD5** | 128 bits (16 bytes) | Very Fast | ❌ Broken | Non-security checksums |
| **SHA-1** | 160 bits (20 bytes) | Fast | ⚠️ Deprecated | Legacy compatibility |
| **SHA-256** | 256 bits (32 bytes) | Moderate | ✅ Secure | Security applications |
| **SHA-512** | 512 bits (64 bytes) | Moderate | ✅ Secure | High security |
| **bcrypt** | Variable | Very Slow | ✅ Secure | Password hashing |

---

## What are Hash Functions?

### Hash Function Basics

A **hash function** takes an input (of any size) and produces a fixed-size output called a **hash**, **digest**, or **checksum**.

**Think of it like a fingerprint:**
- Uniquely identifies data (mostly)
- Much smaller than original data
- Can't recreate original from fingerprint
- Small change in data → completely different fingerprint

### Properties of Good Hash Functions

1. **Deterministic**: Same input always gives same output
   ```
   hash("hello") = abc123
   hash("hello") = abc123  (always)
   ```

2. **Fixed output size**: Regardless of input size
   ```
   hash("a")           = 32 characters
   hash(<1GB file>)    = 32 characters (same size)
   ```

3. **Fast to compute**: Efficient calculation
   ```go
   // Very fast even for large data
   hash := md5.Sum(largeData)
   ```

4. **Avalanche effect**: Small input change → big output change
   ```
   hash("hello")  = 5d41402abc4b2a76b9719d911017c592
   hash("Hello")  = 8b1a9953c4611296a827abf8c47804d7  (completely different)
   ```

5. **One-way**: Can't reverse hash to get original
   ```
   hash("password") = 5f4dcc3b5aa765d61d8327deb882cf99
   // Cannot compute: reverseHash("5f4dcc3b5aa765d61d8327deb882cf99") = ?
   ```

6. **Collision resistance** (for cryptographic hashes): Hard to find two inputs with same hash
   ```
   // Should be extremely rare:
   hash(input1) == hash(input2) where input1 != input2
   ```

### Hash Function Applications

**Non-cryptographic uses:**
- Data deduplication (find duplicate files)
- Cache keys (quick lookups)
- Hash tables (data structure)
- Checksums (detect accidental corruption)

**Cryptographic uses** (NOT MD5 - use SHA-256+):
- Digital signatures
- Password storage (with salt)
- Certificate verification
- Message authentication codes (HMAC)

---

## Understanding the hash.Hash Interface

### The hash.Hash Interface

`crypto/md5.New()` returns a `hash.Hash` interface. Understanding this interface is crucial:

```go
type Hash interface {
    // Embedded io.Writer - write data to hash
    io.Writer
    
    // Sum appends current hash to b and returns result
    Sum(b []byte) []byte
    
    // Reset resets hash to initial state
    Reset()
    
    // Size returns number of bytes Sum will return (16 for MD5)
    Size() int
    
    // BlockSize returns underlying block size (64 for MD5)
    BlockSize() int
}
```

### Interface Methods Explained

#### `io.Writer` (embedded)

The `Write(p []byte) (n int, err error)` method adds data to the hash:

```go
h := md5.New()
h.Write([]byte("Hello"))     // Add "Hello"
h.Write([]byte(", "))        // Add ", "
h.Write([]byte("World!"))    // Add "World!"
// Now h contains hash of "Hello, World!"
```

**Important**: `Write` for hash functions **never returns an error**:
```go
n, err := h.Write(data)
// err is always nil for hash functions
// n is always len(data)
```

#### `Sum(b []byte) []byte`

Appends current hash to `b` and returns the slice:

```go
h := md5.New()
h.Write([]byte("data"))

// Get hash as new slice
hash1 := h.Sum(nil)           // Returns 16-byte slice

// Append hash to existing slice
existing := []byte("prefix: ")
hash2 := h.Sum(existing)      // Returns "prefix: " + hash bytes
```

**Important**: `Sum()` does **not** change the hash state:
```go
h := md5.New()
h.Write([]byte("data"))

hash1 := h.Sum(nil)
hash2 := h.Sum(nil)
// hash1 == hash2 (Sum doesn't change state)

h.Write([]byte("more"))
hash3 := h.Sum(nil)
// hash3 != hash1 (different input)
```

#### `Reset()`

Resets the hash to initial state for reuse:

```go
h := md5.New()
h.Write([]byte("first"))
hash1 := h.Sum(nil)

h.Reset()  // Clear the hash state

h.Write([]byte("second"))
hash2 := h.Sum(nil)
// hash2 is hash of "second", not "firstsecond"
```

#### `Size()` and `BlockSize()`

Return constants about the hash algorithm:

```go
h := md5.New()

size := h.Size()        // 16 (MD5 always produces 16 bytes)
blockSize := h.BlockSize()  // 64 (MD5 processes 64-byte blocks)
```

---

## Package Constants

```go
const BlockSize = 64    // MD5 processes data in 64-byte blocks
const Size = 16         // MD5 produces 16-byte (128-bit) hashes
```

### BlockSize

**What it means**: MD5 processes data in chunks of 64 bytes internally.

**Why it matters**: 
- Writing multiples of 64 bytes may be slightly more efficient
- Mostly implementation detail - you can write any size

```go
// These are equivalent in result, might differ slightly in performance
h.Write(make([]byte, 64))  // One block
h.Write(make([]byte, 100)) // One block + 36 bytes
```

### Size

**What it means**: MD5 hash is always 16 bytes (128 bits).

**Why it matters**:
- Allocate correct buffer size
- Validate hash lengths
- Convert to hex string (32 hex characters = 16 bytes × 2)

```go
hash := h.Sum(nil)
fmt.Println(len(hash))  // Always 16

// Convert to hex string (32 characters)
hexString := fmt.Sprintf("%x", hash)
fmt.Println(len(hexString))  // Always 32
```

---

## Package Functions

### func New() hash.Hash

Creates a new hash.Hash computing the MD5 checksum.

**Signature:**
```go
func New() hash.Hash
```

**Returns**: A `hash.Hash` interface for computing MD5.

**Usage:**
```go
h := md5.New()

// Write data incrementally
h.Write([]byte("Hello, "))
h.Write([]byte("World!"))

// Get the hash
hash := h.Sum(nil)

// Convert to readable hex
fmt.Printf("%x\n", hash)
```

**When to use:**
- Streaming data (files, network)
- Multiple writes before finalizing
- Reusing hash instance (with Reset())

### func Sum(data []byte) [Size]byte

Returns the MD5 checksum of the data in one call.

**Signature:**
```go
func Sum(data []byte) [Size]byte  // Returns [16]byte
```

**Returns**: 16-byte array containing MD5 hash.

**Usage:**
```go
data := []byte("Hello, World!")
hash := md5.Sum(data)

// hash is [16]byte, not []byte
fmt.Printf("%x\n", hash)  // Print as hex

// Convert to slice if needed
hashSlice := hash[:]
```

**When to use:**
- All data available at once
- Quick one-off hashes
- Simple checksums

**Important differences from New():**
```go
// Sum returns [16]byte (array)
hash1 := md5.Sum(data)
var arr [16]byte = hash1  // Array

// New returns []byte via Sum(nil) (slice)
h := md5.New()
h.Write(data)
hash2 := h.Sum(nil)  // Slice []byte
```

---

## Basic Usage Patterns

### Pattern 1: Simple Hash (All Data at Once)

Use `Sum()` when all data is available:

```go
package main

import (
    "crypto/md5"
    "fmt"
)

func main() {
    data := []byte("The quick brown fox jumps over the lazy dog")
    
    // Compute MD5 in one call
    hash := md5.Sum(data)
    
    // Print as hex string
    fmt.Printf("MD5: %x\n", hash)
    // Output: MD5: 9e107d9d372bb6826bd81d3542a419d6
}
```

### Pattern 2: Incremental Hash (Streaming Data)

Use `New()` when data comes in chunks:

```go
package main

import (
    "crypto/md5"
    "fmt"
)

func main() {
    h := md5.New()
    
    // Write data incrementally
    h.Write([]byte("The quick "))
    h.Write([]byte("brown fox "))
    h.Write([]byte("jumps over "))
    h.Write([]byte("the lazy dog"))
    
    // Get final hash
    hash := h.Sum(nil)
    
    fmt.Printf("MD5: %x\n", hash)
    // Same output: 9e107d9d372bb6826bd81d3542a419d6
}
```

### Pattern 3: File Hash

Hash a file by reading in chunks:

```go
package main

import (
    "crypto/md5"
    "fmt"
    "io"
    "os"
)

func hashFile(filename string) (string, error) {
    file, err := os.Open(filename)
    if err != nil {
        return "", err
    }
    defer file.Close()
    
    h := md5.New()
    
    // Copy file to hash (efficient streaming)
    if _, err := io.Copy(h, file); err != nil {
        return "", err
    }
    
    // Get hash
    hash := h.Sum(nil)
    
    return fmt.Sprintf("%x", hash), nil
}

func main() {
    hash, err := hashFile("example.txt")
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
    
    fmt.Println("File MD5:", hash)
}
```

### Pattern 4: String Hash Helper

Convenience function for hashing strings:

```go
package main

import (
    "crypto/md5"
    "fmt"
)

func md5String(s string) string {
    hash := md5.Sum([]byte(s))
    return fmt.Sprintf("%x", hash)
}

func main() {
    fmt.Println(md5String("hello"))
    // Output: 5d41402abc4b2a76b9719d911017c592
    
    fmt.Println(md5String("world"))
    // Output: 7d793037a0760186574b0282f2f435e7
}
```

### Pattern 5: Reusing Hash Instance

Use `Reset()` to reuse hash for multiple computations:

```go
package main

import (
    "crypto/md5"
    "fmt"
)

func main() {
    h := md5.New()
    
    // Hash first string
    h.Write([]byte("first"))
    hash1 := h.Sum(nil)
    fmt.Printf("Hash 1: %x\n", hash1)
    
    // Reset and hash second string
    h.Reset()
    h.Write([]byte("second"))
    hash2 := h.Sum(nil)
    fmt.Printf("Hash 2: %x\n", hash2)
    
    // Hash 1 and Hash 2 are independent
}
```

### Pattern 6: Hash with Prefix/Suffix

Use `Sum(b)` to append hash to existing data:

```go
package main

import (
    "crypto/md5"
    "fmt"
)

func main() {
    h := md5.New()
    h.Write([]byte("data"))
    
    // Append hash to prefix
    prefix := []byte("HASH:")
    result := h.Sum(prefix)
    
    fmt.Printf("Result: %s\n", result)
    // Output: Result: HASH:<16 bytes of hash>
    
    // Extract just the hash (last 16 bytes)
    hashOnly := result[len(prefix):]
    fmt.Printf("Hash only: %x\n", hashOnly)
}
```

---

## Common Use Cases

### Use Case 1: File Deduplication

Find duplicate files by comparing MD5 hashes:

```go
package main

import (
    "crypto/md5"
    "fmt"
    "io"
    "os"
)

type FileHash struct {
    Path string
    Hash string
}

func hashFile(path string) (string, error) {
    file, err := os.Open(path)
    if err != nil {
        return "", err
    }
    defer file.Close()
    
    h := md5.New()
    if _, err := io.Copy(h, file); err != nil {
        return "", err
    }
    
    return fmt.Sprintf("%x", h.Sum(nil)), nil
}

func findDuplicates(files []string) map[string][]string {
    hashMap := make(map[string][]string)
    
    for _, file := range files {
        hash, err := hashFile(file)
        if err != nil {
            continue
        }
        hashMap[hash] = append(hashMap[hash], file)
    }
    
    // Keep only duplicates
    duplicates := make(map[string][]string)
    for hash, paths := range hashMap {
        if len(paths) > 1 {
            duplicates[hash] = paths
        }
    }
    
    return duplicates
}

func main() {
    files := []string{"file1.txt", "file2.txt", "file3.txt"}
    dupes := findDuplicates(files)
    
    for hash, paths := range dupes {
        fmt.Printf("Duplicate files (hash %s):\n", hash[:8])
        for _, path := range paths {
            fmt.Printf("  - %s\n", path)
        }
    }
}
```

### Use Case 2: Cache Keys

Generate cache keys from complex data:

```go
package main

import (
    "crypto/md5"
    "fmt"
)

type Request struct {
    Method string
    URL    string
    Body   string
}

func cacheKey(req Request) string {
    h := md5.New()
    h.Write([]byte(req.Method))
    h.Write([]byte(req.URL))
    h.Write([]byte(req.Body))
    
    return fmt.Sprintf("%x", h.Sum(nil))
}

func main() {
    req1 := Request{Method: "GET", URL: "/api/users", Body: ""}
    req2 := Request{Method: "GET", URL: "/api/users", Body: ""}
    req3 := Request{Method: "POST", URL: "/api/users", Body: "data"}
    
    fmt.Println("Key 1:", cacheKey(req1))
    fmt.Println("Key 2:", cacheKey(req2))  // Same as Key 1
    fmt.Println("Key 3:", cacheKey(req3))  // Different
}
```

### Use Case 3: Data Integrity Check (Non-Security)

Verify data wasn't corrupted during transmission:

```go
package main

import (
    "crypto/md5"
    "fmt"
)

type DataPacket struct {
    Data     []byte
    Checksum string
}

func createPacket(data []byte) DataPacket {
    hash := md5.Sum(data)
    return DataPacket{
        Data:     data,
        Checksum: fmt.Sprintf("%x", hash),
    }
}

func verifyPacket(packet DataPacket) bool {
    hash := md5.Sum(packet.Data)
    expected := fmt.Sprintf("%x", hash)
    return expected == packet.Checksum
}

func main() {
    // Sender creates packet
    original := []byte("Important data")
    packet := createPacket(original)
    
    // Receiver verifies packet
    if verifyPacket(packet) {
        fmt.Println("Data integrity verified")
    } else {
        fmt.Println("Data corrupted!")
    }
    
    // Simulate corruption
    packet.Data[0] = 'X'
    if !verifyPacket(packet) {
        fmt.Println("Corruption detected!")
    }
}
```

### Use Case 4: ETag Generation (HTTP Caching)

Generate ETags for HTTP response caching:

```go
package main

import (
    "crypto/md5"
    "fmt"
    "net/http"
)

func generateETag(content []byte) string {
    hash := md5.Sum(content)
    return fmt.Sprintf("\"%x\"", hash)
}

func handler(w http.ResponseWriter, r *http.Request) {
    content := []byte("This is the response content")
    etag := generateETag(content)
    
    // Check if client has cached version
    if r.Header.Get("If-None-Match") == etag {
        w.WriteHeader(http.StatusNotModified)
        return
    }
    
    // Send new content with ETag
    w.Header().Set("ETag", etag)
    w.Write(content)
}
```

---

## Security Considerations

### Why MD5 is Broken

**Collision attacks are practical** - attackers can create two different files with the same MD5 hash:

```
file1.pdf (legitimate contract)
MD5: abc123...

file2.pdf (fraudulent contract)
MD5: abc123...  (SAME HASH!)
```

This was demonstrated in 2004 and has only gotten easier since.

### What This Means

**Never use MD5 for:**

1. **Password Hashing**
   ```go
   // ❌ NEVER DO THIS
   password := "user_password"
   hash := md5.Sum([]byte(password))
   // Easily cracked with rainbow tables
   ```

2. **Digital Signatures**
   ```go
   // ❌ NEVER DO THIS
   document := []byte("Important contract")
   signature := md5.Sum(document)
   // Attacker can create different document with same hash
   ```

3. **Security Checksums**
   ```go
   // ❌ NEVER DO THIS for security
   downloadedFile := fetchFile(url)
   if md5Hash(downloadedFile) != expectedHash {
       // Attacker could have created collision
   }
   ```

### Safe Uses of MD5

**Acceptable for non-security purposes:**

```go
// ✅ OK: Non-cryptographic checksum
func detectAccidentalCorruption(data []byte, expectedHash string) bool {
    hash := fmt.Sprintf("%x", md5.Sum(data))
    return hash == expectedHash
}

// ✅ OK: Cache key generation
func cacheKey(url string) string {
    return fmt.Sprintf("%x", md5.Sum([]byte(url)))
}

// ✅ OK: File deduplication
func findDuplicateFiles(files []string) map[string][]string {
    // MD5 collision unlikely for normal files
    // Not used for security verification
}

// ✅ OK: Hash table buckets
func getBucket(key string) int {
    hash := md5.Sum([]byte(key))
    return int(hash[0]) % numBuckets
}
```

---

## Alternatives to MD5

### For Security: Use SHA-256 or SHA-512

```go
import "crypto/sha256"

// ✅ For security-critical hashing
hash := sha256.Sum256(data)
fmt.Printf("%x\n", hash)
```

```go
import "crypto/sha512"

// ✅ For higher security
hash := sha512.Sum512(data)
fmt.Printf("%x\n", hash)
```

### For Passwords: Use bcrypt, scrypt, or argon2

```go
import "golang.org/x/crypto/bcrypt"

// ✅ For password hashing
password := []byte("user_password")
hash, err := bcrypt.GenerateFromPassword(password, bcrypt.DefaultCost)

// Verify password
err = bcrypt.CompareHashAndPassword(hash, password)
```

### For Fast Non-Crypto Hashing: Use hash/fnv or hash/maphash

```go
import "hash/fnv"

// ✅ For fast, non-cryptographic hashing
h := fnv.New64a()
h.Write(data)
hash := h.Sum64()  // uint64, very fast
```

---

## Best Practices

### DO ✅

```go
// ✅ Use for non-security checksums
hash := md5.Sum(data)

// ✅ Use io.Copy for large files
h := md5.New()
io.Copy(h, file)

// ✅ Reset and reuse hash instance
h.Reset()

// ✅ Convert to hex for display
fmt.Printf("%x", hash)

// ✅ Use Sum() for simple one-off hashes
quickHash := md5.Sum([]byte("data"))

// ✅ Document why you're using MD5 (not for security)
// MD5 used for cache keys only, not security
cacheKey := md5String(url)
```

### DON'T ❌

```go
// ❌ Never use for passwords
passwordHash := md5.Sum([]byte(password))  // INSECURE

// ❌ Never use for security verification
if md5.Sum(file) == trustedHash {  // VULNERABLE
    executeFile(file)
}

// ❌ Don't ignore that MD5 is broken
// "It's probably fine" - NO!

// ❌ Don't copy mutex (applies to hash.Hash)
h1 := md5.New()
h2 := h1  // Creates problems, pass pointer instead

// ❌ Don't assume uniqueness for security
// Two different files CAN have same MD5

// ❌ Don't concatenate hashes manually
// Use h.Write() multiple times instead
wrongHash := md5.Sum([]byte(str1 + str2))  // Don't do this
h := md5.New()  // Do this instead
h.Write([]byte(str1))
h.Write([]byte(str2))
```

---

## Summary

### Quick Reference

| Operation | Code | Use Case |
|-----------|------|----------|
| Simple hash | `md5.Sum(data)` | All data at once |
| Stream hash | `h := md5.New(); h.Write(chunk)` | Large files, streaming |
| File hash | `io.Copy(md5.New(), file)` | Hash entire file |
| Hex string | `fmt.Sprintf("%x", hash)` | Human-readable output |
| Reset hash | `h.Reset()` | Reuse hash instance |

### Key Takeaways

1. **MD5 is fast** - Good for non-security checksums
2. **MD5 is broken** - Never use for security
3. **MD5 is deterministic** - Same input = same output
4. **MD5 is fixed-size** - Always 16 bytes (128 bits)
5. **Use alternatives for security** - SHA-256, SHA-512, bcrypt

### When to Use MD5

✅ **Acceptable:**
- Non-cryptographic checksums
- Cache keys
- File deduplication
- Hash table buckets
- Legacy system compatibility

❌ **Never:**
- Password hashing
- Digital signatures
- Security verification
- Anything requiring collision resistance

---

## Related Documentation

- [Go hash Package](https://pkg.go.dev/hash) - Hash interface documentation
- [Go crypto/sha256 Package](https://pkg.go.dev/crypto/sha256) - Secure alternative
- [Go io Package](https://pkg.go.dev/io) - io.Copy for streaming hashes

---

[← Back to Documentation](README.md) | [↑ Back to Index](../MASTER-INDEX.md)
