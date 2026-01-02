# Go Types: Complete Guide

A comprehensive deep dive into Go's type system: primitives, composite types, and their interactions.

---

## Table of Contents

### Part 1: Primitive Types
1. [Introduction](#introduction)
2. [Numeric Types](#numeric-types)
3. [Boolean Type](#boolean-type)
4. [String Type](#string-type)
5. [Rune Type (Deep Dive)](#rune-type-deep-dive)
6. [Byte Type](#byte-type)
7. [Character Encoding: The Foundation](#character-encoding-the-foundation)
8. [String vs []byte vs []rune](#string-vs-byte-vs-rune)

### Part 2: Composite Types
9. [Arrays](#arrays)
10. [Slices (Deep Dive)](#slices-deep-dive)
11. [Maps (Deep Dive)](#maps-deep-dive)
12. [Pointers](#pointers)
13. [Structs](#structs)

### Part 3: Practical Usage
14. [Common Patterns & Use Cases](#common-patterns--use-cases)
15. [Performance Considerations](#performance-considerations)
16. [Best Practices](#best-practices)

---

## Introduction

Go has a small set of **primitive types** (also called basic types or built-in types). Understanding these deeply is crucial because:

1. They're the foundation of all data structures
2. Go is **strongly typed** - you must understand type conversions
3. Character handling (strings, bytes, runes) is unique in Go
4. Performance characteristics differ significantly

### Official Documentation

- **Go Language Spec**: https://go.dev/ref/spec#Types
- **Strings Package**: https://pkg.go.dev/strings
- **Unicode Package**: https://pkg.go.dev/unicode
- **UTF-8 Package**: https://pkg.go.dev/unicode/utf8

---

## Numeric Types

### Integer Types

Go provides **10 integer types** with explicit sizes:

```go
// Signed integers (can be negative)
int8    // -128 to 127                    (1 byte)
int16   // -32,768 to 32,767              (2 bytes)
int32   // -2,147,483,648 to 2,147,483,647 (4 bytes)
int64   // -9,223,372,036,854,775,808 to ... (8 bytes)

// Unsigned integers (only positive)
uint8   // 0 to 255                       (1 byte)
uint16  // 0 to 65,535                    (2 bytes)
uint32  // 0 to 4,294,967,295             (4 bytes)
uint64  // 0 to 18,446,744,073,709,551,615 (8 bytes)

// Platform-dependent sizes
int     // Same as int32 or int64 (depends on CPU architecture)
uint    // Same as uint32 or uint64
```

### Special Integer Aliases

```go
byte    // Alias for uint8 (used for raw data)
rune    // Alias for int32 (used for Unicode code points)
```

### Floating-Point Types

```go
float32 // IEEE-754 32-bit floating point
float64 // IEEE-754 64-bit floating point (default for literals)
```

### Complex Types

```go
complex64  // Complex number with float32 real and imaginary parts
complex128 // Complex number with float64 real and imaginary parts
```

### Examples:

```go
// Integer types
var age int = 30
var smallNumber int8 = 127
var bigNumber uint64 = 18446744073709551615

// Floating point
var price float64 = 19.99
var temperature float32 = 98.6

// Complex numbers
var signal complex128 = 1 + 2i
```

---

## Boolean Type

The simplest type - only two values:

```go
bool  // true or false
```

**Important characteristics:**
- **NOT** an integer (unlike C/C++)
- Cannot convert `1` to `true` or `0` to `false` directly
- Zero value is `false`

```go
var isActive bool        // false (zero value)
var isValid bool = true

// ❌ This is INVALID in Go
if 1 {  // ERROR: cannot use 1 (type int) as type bool
    // ...
}

// ✅ Must be explicit
if isValid {
    // ...
}
```

---

## String Type

### What is a String?

In Go, a **string** is a fundamental type that represents text. Understanding strings deeply is crucial because Go's design differs from many other languages.

**Formal definition**: A string is an **immutable sequence of bytes**, typically (but not necessarily) representing UTF-8 encoded text.

**Key conceptual points:**
1. **Immutable**: Once created, a string's contents cannot be changed
2. **Byte sequence**: Under the hood, strings are just arrays of bytes
3. **UTF-8 by default**: Go assumes strings contain UTF-8 encoded Unicode text
4. **Not null-terminated**: Unlike C strings, Go strings know their length
5. **Value type**: Strings are passed by value, but copying is cheap (explained below)

### Why Immutability Matters

Immutability means you cannot modify a string in place:

```go
s := "Hello"
s[0] = 'h'  // ❌ Compile error: cannot assign to s[0]
```

**Why did Go choose immutability?**

1. **Thread Safety**: Immutable strings can be shared between goroutines safely without locks
2. **String Interning**: Multiple variables can share the same underlying data
3. **Predictability**: Functions receiving strings know they won't be modified
4. **Hash Keys**: Strings make excellent map keys (value won't change)

**How to "modify" a string:**
```go
s := "Hello"

// Option 1: Create new string with concatenation
s = "h" + s[1:]  // "hello"

// Option 2: Convert to []byte, modify, convert back
b := []byte(s)
b[0] = 'h'
s = string(b)  // "hello"

// Option 3: Convert to []rune for multi-byte characters
r := []rune(s)
r[0] = 'h'
s = string(r)  // "hello"
```

### String Internals

Unlike many languages where strings are objects, Go strings are **value types** implemented as a simple struct:

```go
// Actual implementation in Go runtime (reflect/value.go):
type StringHeader struct {
    Data uintptr  // Pointer to underlying byte array
    Len  int      // Length in BYTES (not characters!)
}
```

**What this means:**

```go
s := "Hello"

// The variable 's' contains:
// - Data: memory address pointing to ['H','e','l','l','o']
// - Len: 5
```

**Memory layout:**
```
Stack (variable s):          Heap (actual string data):
┌──────────────┐            ┌─┬─┬─┬─┬─┐
│ Data: 0x1234 │  ───────>  │H│e│l│l│o│
│ Len:  5      │            └─┴─┴─┴─┴─┘
└──────────────┘            Address: 0x1234
```

**Copying strings is cheap:**
```go
s1 := "Hello, World!"
s2 := s1  // Only copies pointer + length (16 bytes)
          // NOT the entire "Hello, World!" data
```

Both `s1` and `s2` point to the **same underlying byte array**. This is safe because strings are immutable!

### Key Characteristics

```go
s := "Hello, 世界"

// Length in BYTES (not characters!)
fmt.Println(len(s))  // 13 (not 9!)
// "Hello, " = 7 bytes
// "世" = 3 bytes (UTF-8)
// "界" = 3 bytes (UTF-8)
// Total: 13 bytes

// Indexing gives BYTES (not characters!)
fmt.Printf("%c\n", s[0])   // 'H' (1 byte)
fmt.Printf("%c\n", s[7])   // '�' (partial byte - WRONG!)

// Strings are IMMUTABLE
// s[0] = 'h'  // ERROR: cannot assign to s[0]
```

### String Literals

```go
// Interpreted strings (escape sequences processed)
s1 := "Hello\nWorld"  // Contains newline
s2 := "Path: C:\\Users\\file.txt"  // Backslashes escaped

// Raw strings (backticks - no escape processing)
s3 := `Hello\nWorld`  // Literal backslash and 'n'
s4 := `Path: C:\Users\file.txt`  // Backslashes preserved
s5 := `Multi
line
string`  // Can span multiple lines
```

---

## Rune Type (Deep Dive)

### What is a Rune?

**Definition**: A **rune** is an **alias for `int32`** that represents a **Unicode code point**.

```go
type rune = int32  // Defined in Go source
```

**But what does that actually mean?**

A rune is Go's way of representing a **single character** in the Unicode standard. Think of it as the answer to: "What is one character?"

**Why not just use `int32`?**

You *could* use `int32`, but `rune` provides **semantic meaning**:

```go
// These are technically identical:
var ch1 int32 = 65
var ch2 rune = 65

// But the intent is different:
var number int32 = 65        // I'm storing the number 65
var character rune = 'A'     // I'm storing the character 'A' (which is 65)
```

The type name `rune` tells other programmers (and yourself): "This variable holds a character, not just any number."

### Why 32 Bits? The Math Behind Runes

Unicode defines 1,114,112 possible code points (characters):
- From U+0000 to U+10FFFF (in hexadecimal)
- In decimal: 0 to 1,114,111

**Can we fit this in smaller types?**

```
uint8  (byte):  0 to 255             ❌ Too small (only 256 values)
uint16:         0 to 65,535          ❌ Too small (only 65,536 values)
int32  (rune):  -2,147,483,648 to 2,147,483,647  ✅ Fits! (4+ billion values)
```

**Why signed (`int32`) instead of unsigned (`uint32`)?**

Historical reasons and compatibility with the C programming language's `wchar_t`. The negative values are never used for valid Unicode, so the effective range is 0 to 2,147,483,647.

### Historical Context: Why Runes Exist

#### The Unicode Story

**1960s-1980s**: ASCII (American Standard Code for Information Interchange)
- 7 bits = 128 characters
- Only English letters, digits, basic punctuation
- Every character = 1 byte

```
'A' = 65
'Z' = 90
'0' = 48
```

**Problem**: What about other languages?
- Chinese has 50,000+ characters
- Arabic, Hebrew, Cyrillic, etc.
- Mathematical symbols, emojis

**1991**: Unicode was created
- Goal: One unique number for EVERY character in EVERY language
- Called a **code point** (written as U+XXXX)

```
'A'  = U+0041 (code point 65)
'世' = U+4E16 (code point 19,990)
'💻' = U+1F4BB (code point 128,187)
```

#### UTF-8 Encoding: The Solution

**Problem**: Unicode has 1,112,064 possible code points. How to store them efficiently in computer memory?

**Naive solutions (why they don't work):**

1. **One byte per character**: Only 256 characters possible (too small)
2. **Two bytes per character**: Only 65,536 characters (still too small)
3. **Four bytes per character**: Fits all Unicode, but **wastes space**
   - "Hello" would take 20 bytes instead of 5
   - Most text is ASCII (English letters, digits, punctuation)
   - 4× memory usage for common text!

**UTF-8: Variable-Length Encoding (Brilliant Solution)**

UTF-8 uses **1 to 4 bytes per character**, depending on what character it is:

```
ASCII characters:        1 byte  (A-Z, 0-9, punctuation)
European characters:     2 bytes (é, ñ, ü, Cyrillic)
Asian characters:        3 bytes (世, 界, 한, の)
Emoji & rare symbols:    4 bytes (💻, 🎉, 𝔸)
```

**Why is this brilliant?**

1. **Backward compatible with ASCII**: English text uses same bytes as before
2. **Space efficient**: Common characters (English) use less space
3. **Self-synchronizing**: You can find character boundaries anywhere in the string
4. **No byte-order issues**: Works same on all computers (big-endian, little-endian)

**UTF-8 encoding examples:**

```
'A'  (U+0041)  = 01000001                                      (1 byte)
'€'  (U+20AC)  = 11100010 10000010 10101100                    (3 bytes)
'世' (U+4E16)  = 11100100 10111000 10010110                    (3 bytes)
'💻' (U+1F4BB) = 11110000 10011111 10010010 10111011           (4 bytes)
```

**How to read the bit patterns:**

- **1 byte**: `0xxxxxxx` — If first bit is 0, it's a 1-byte character (ASCII)
- **2 bytes**: `110xxxxx 10xxxxxx` — Starts with 110, continuation with 10
- **3 bytes**: `1110xxxx 10xxxxxx 10xxxxxx` — Starts with 1110
- **4 bytes**: `11110xxx 10xxxxxx 10xxxxxx 10xxxxxx` — Starts with 11110

The `x` bits contain the actual Unicode code point value.

### Rune in Go

A **rune** represents one Unicode code point (one character, conceptually):

```go
var ch rune = 'A'       // Single quotes for rune literals
var ch2 rune = '世'
var ch3 rune = '💻'
var ch4 rune = '\n'     // Escape sequences work

fmt.Printf("%d\n", ch)   // 65 (code point value)
fmt.Printf("%c\n", ch)   // A (character representation)
fmt.Printf("%U\n", ch)   // U+0041 (Unicode code point)
```

### Why Not Just Use int32?

**You could**, but `rune` is **semantically clearer**:

```go
// ❌ Less clear
var character int32 = 65

// ✅ Clear intent
var character rune = 'A'
```

### Rune Literals

```go
// Character literals (single quotes)
r1 := 'A'           // rune (inferred type)
r2 := '世'
r3 := '💻'

// Unicode escape sequences
r4 := '\n'          // Newline
r5 := '\t'          // Tab
r6 := '\u4E16'      // '世' (4-digit Unicode)
r7 := '\U0001F4BB'  // '💻' (8-digit Unicode)

// Numeric value
r8 := rune(65)      // 'A'
```

---

## Byte Type

### What is a Byte?

**Definition**: A **byte** is an **alias for `uint8`** that represents a raw 8-bit value (0-255).

```go
type byte = uint8  // Defined in Go source
```

**Conceptual understanding:**

A byte is the **fundamental unit of computer memory**. It's 8 bits, which can represent:
- Numbers: 0 to 255 (unsigned)
- Raw binary data: file contents, network packets, images
- Single ASCII characters: 'A' = 65, 'Z' = 90
- One piece of a multi-byte UTF-8 character

**When to think "byte" vs "uint8":**

```go
var age uint8 = 25           // Thinking: small positive integer
var pixelValue byte = 255    // Thinking: raw data (pixel color)
```

Both are identical in Go, but `byte` conveys "raw data" while `uint8` conveys "small number."

### Historical Context: The Byte

A **byte** is historically 8 bits, but this wasn't always guaranteed. In the 1960s-70s, computers had bytes of different sizes (6-bit, 7-bit, 9-bit, etc.). 

The IBM System/360 (1964) standardized the 8-bit byte, and it became universal because:
1. Powers of 2 (2^8 = 256) are computationally efficient
2. 256 values can represent extended ASCII character set
3. Aligns well with memory addressing

In Go (and modern computing), a byte is **always 8 bits**.

### Byte vs Rune

| Aspect | byte | rune |
|--------|------|------|
| **Type** | `uint8` | `int32` |
| **Size** | 1 byte (8 bits) | 4 bytes (32 bits) |
| **Range** | 0-255 | 0 to 1,114,111 (Unicode range) |
| **Purpose** | Raw binary data | Unicode character |
| **Literal** | `'A'` or `byte('A')` | `'A'` |

```go
// Both represent 'A', but different semantics
var b byte = 65   // Raw byte value
var r rune = 'A'  // Unicode character

// byte can only hold ASCII (0-255)
var b1 byte = 'A'   // ✅ OK (65)
var b2 byte = '世'  // ❌ Overflow! (19,990 > 255)

// rune can hold any Unicode
var r1 rune = 'A'   // ✅ OK
var r2 rune = '世'  // ✅ OK
var r3 rune = '💻'  // ✅ OK
```

---

## Character Encoding: The Foundation

### Understanding the Layers

```
┌─────────────────────────────────────┐
│  "Hello, 世界"  (string in code)   │
└─────────────────────────────────────┘
                 ↓
┌─────────────────────────────────────┐
│  Unicode Code Points (abstract)     │
│  H=U+0048, e=U+0065, l=U+006C, ...  │
│  世=U+4E16, 界=U+754C              │
└─────────────────────────────────────┘
                 ↓
┌─────────────────────────────────────┐
│  UTF-8 Encoding (bytes in memory)   │
│  48 65 6C 6C 6F 2C 20               │
│  E4 B8 96 E7 95 8C                  │
└─────────────────────────────────────┘
```

### Example: Breaking Down "世"

```go
s := "世"

## String vs []byte vs []rune

### The Fundamental Question

"How should I represent text in my Go program?"

This is one of the most important decisions when working with strings, and the answer depends on **what you need to do** with the text.

### Conceptual Understanding

Think of these three types as **different views** of the same text:

```
Text: "Hello, 世界"

View 1 (string):     Immutable sequence of UTF-8 bytes
View 2 ([]byte):     Mutable sequence of UTF-8 bytes  
View 3 ([]rune):     Mutable sequence of Unicode characters
```

**Analogy**: Like viewing a document
- **string**: PDF (read-only, efficient to share)
- **[]byte**: Word doc in binary mode (can edit bytes, but might break formatting)
- **[]rune**: Word doc in normal mode (can edit characters properly)

### Why Three Types?

**Why not just one string type?**

Different operations have different requirements:

1. **Reading text**: Immutable string is perfect (thread-safe, efficient)
2. **Network I/O**: Need []byte (binary data, not always text)
3. **Text processing**: Need []rune (character-level operations)

**Example scenario:**
```go
// Receive data from network (bytes)
data := []byte{...}

// Convert to string for display
message := string(data)

// Process character-by-character
chars := []rune(message)
chars[0] = unicode.ToUpper(chars[0])  // Capitalize first letter
```

Each type serves its purpose!

### Comparison Table

| Aspect | `string` | `[]byte` | `[]rune` |
|--------|----------|----------|----------|
| **Mutability** | Immutable | Mutable | Mutable |
| **Element Type** | byte (uint8) | byte (uint8) | rune (int32) |
| **Indexing Returns** | byte | byte | rune |
| **Length** | Bytes | Bytes | Characters |
| **Memory** | Efficient | Efficient | 4× string size |
| **Use Case** | Text, keys | Binary data, I/O | Character manipulation |
| **Thread-safe** | Yes (immutable) | No (mutable) | No (mutable) |
| **Map keys** | Yes | No | No |

### Detailed Examples
// Output: E4 B8 96
```

### UTF-8 Encoding Rules

| Code Point Range | Bytes | Byte Pattern |
|------------------|-------|--------------|
| U+0000 to U+007F | 1 | `0xxxxxxx` |
| U+0080 to U+07FF | 2 | `110xxxxx 10xxxxxx` |
| U+0800 to U+FFFF | 3 | `1110xxxx 10xxxxxx 10xxxxxx` |
| U+10000 to U+10FFFF | 4 | `11110xxx 10xxxxxx 10xxxxxx 10xxxxxx` |

---

### Detailed Examples

#### String: Immutable Byte Sequence

```go
s := "Hello, 世界"

// Length in BYTES
fmt.Println(len(s))  // 13

// Indexing gets BYTES (NOT characters!)
fmt.Printf("%c\n", s[0])  // 'H'
fmt.Printf("%c\n", s[7])  // '�' WRONG! (partial UTF-8 byte)

// Immutable - cannot change
// s[0] = 'h'  // ERROR!

// Must create new string
s2 := "h" + s[1:]  // "hello, 世界"
```

#### []byte: Mutable Byte Sequence

```go
b := []byte("Hello, 世界")

// Length in BYTES (same as string)
fmt.Println(len(b))  // 13

// Indexing gets BYTES
fmt.Printf("%c\n", b[0])  // 'H'

// Mutable - can change!
b[0] = 'h'
fmt.Println(string(b))  // "hello, 世界"

// Efficient for binary data, I/O operations
data := []byte{0xFF, 0xD8, 0xFF, 0xE0}  // JPEG header
```

#### []rune: Mutable Character Sequence

```go
r := []rune("Hello, 世界")

// Length in CHARACTERS
fmt.Println(len(r))  // 9 (not 13!)

// Indexing gets CHARACTERS
fmt.Printf("%c\n", r[0])  // 'H'
fmt.Printf("%c\n", r[7])  // '世' CORRECT!

// Mutable
r[0] = 'h'
r[7] = '界'
fmt.Println(string(r))  // "hello, 界界"

// Memory: 4 bytes per rune
// "Hello, 世界" as string:  13 bytes
// "Hello, 世界" as []rune:  36 bytes (9 runes × 4 bytes)
```

### Conversions

```go
s := "Hello, 世界"

// String → []byte (shares underlying data if possible)
b := []byte(s)

// String → []rune (allocates new memory, decodes UTF-8)
r := []rune(s)

// []byte → String
s2 := string(b)

// []rune → String
s3 := string(r)

// Direct conversions
ch := rune('A')
by := byte('A')
```

### Pattern 3: Reversing a String

**The Problem**: Reversing a string character-by-character

**Why this is tricky**: UTF-8 multi-byte characters!

```go
// ❌ WRONG - reverses bytes (corrupts UTF-8)
func reverseBad(s string) string {
    b := []byte(s)
    for i, j := 0, len(b)-1; i < j; i, j = i+1, j-1 {
        b[i], b[j] = b[j], b[i]
    }
    return string(b)
}

fmt.Println(reverseBad("Hello"))         // "olleH" ✅
fmt.Println(reverseBad("Hello, 世界"))   // "�界�世 ,olleH" ❌ CORRUPTED!
```

**Why it breaks:**

```
Original:  "世" = [E4 B8 96] (3 bytes in UTF-8)
Reversed:       [96 B8 E4] (invalid UTF-8 sequence!)
Result:    '�' (replacement character for invalid UTF-8)
```

When you reverse bytes, multi-byte UTF-8 sequences get scrambled. The byte pattern `[96 B8 E4]` doesn't match any valid UTF-8 encoding, so Go replaces it with the "replacement character" (�).

**Visual explanation:**
```
"Hello, 世界" in bytes:
[H] [e] [l] [l] [o] [,] [ ] [E4 B8 96] [E7 95 8C]
                            └── "世" ──┘ └── "界" ──┘

Reversed bytes (WRONG):
[E7 95 8C] [E4 B8 96] [ ] [,] [o] [l] [l] [e] [H]
└── broken! ──┘ └── broken! ──┘
```

**The Fix**: Reverse characters, not bytes

```go
// ✅ RIGHT - reverses characters
func reverseGood(s string) string {
    runes := []rune(s)  // Convert to characters first
    for i, j := 0, len(runes)-1; i < j; i, j = i+1, j-1 {
        runes[i], runes[j] = runes[j], runes[i]
    }
    return string(runes)  // Convert back to UTF-8
}

fmt.Println(reverseGood("Hello"))         // "olleH" ✅
fmt.Println(reverseGood("Hello, 世界"))   // "界世 ,olleH" ✅ CORRECT!
```

**Why it works:**

```
"Hello, 世界" as runes (characters):
['H'] ['e'] ['l'] ['l'] ['o'] [','] [' '] ['世'] ['界']
  ↓ Reverse these ↓
['界'] ['世'] [' '] [','] ['o'] ['l'] ['l'] ['e'] ['H']
  ↓ Convert back to UTF-8 ↓
"界世 ,olleH"
```

Each rune represents a complete character, so reversing maintains UTF-8 integrity! fmt.Printf("%c ", s[i])
}
// Output: H e l l o ,   ä ¸ � ç � �  (GARBLED!)

// ✅ RIGHT - range decodes UTF-8 automatically
for i, ch := range s {
    fmt.Printf("%d: %c [U+%04X]\n", i, ch, ch)
}
// Output:
// 0: H [U+0048]
// 1: e [U+0065]
// 2: l [U+006C]
// 3: l [U+006C]
// 4: o [U+006F]
// 5: , [U+002C]
// 6:   [U+0020]
// 7: 世 [U+4E16]  ← Notice: index jumps from 7 to 10!
// 10: 界 [U+754C]
```

**Important**: `range` on string returns:
- **index**: byte position (not character position!)
- **value**: rune (decoded character)



### Pattern 4: Substring by Character Position

```go
s := "Hello, 世界"

// ❌ WRONG - slicing by bytes
substr := s[7:10]  // Gets bytes 7-9
fmt.Println(substr)  // "世" (works by luck!)

substr2 := s[7:9]  // Gets bytes 7-8 (incomplete UTF-8!)
fmt.Println(substr2)  // "�" CORRUPTED!

// ✅ RIGHT - convert to []rune first
runes := []rune(s)
substr3 := string(runes[7:9])  // Characters 7-8
fmt.Println(substr3)  // "世界" CORRECT!
```

### Pattern 5: Checking if Character is in Set

```go
// Using rune
func isVowel(ch rune) bool {
    vowels := "aeiouAEIOU"
    for _, v := range vowels {
        if ch == v {
            return true
        }
    }
    return false
}

// Using map for efficiency
var vowelMap = map[rune]bool{
    'a': true, 'e': true, 'i': true, 'o': true, 'u': true,
    'A': true, 'E': true, 'I': true, 'O': true, 'U': true,
}

func isVowelFast(ch rune) bool {
    return vowelMap[ch]
}
```

### Pattern 6: Building Strings Efficiently

```go
// ❌ SLOW - string concatenation in loop
func buildSlow(n int) string {
    s := ""
    for i := 0; i < n; i++ {
        s += "a"  // Creates new string each time!
    }
    return s
}

// ✅ FAST - use strings.Builder
func buildFast(n int) string {
    var b strings.Builder
    b.Grow(n)  // Pre-allocate capacity
    for i := 0; i < n; i++ {
        b.WriteRune('a')
    }
    return b.String()
}

// ✅ FAST - use []rune when manipulating characters
func buildRunes(n int) string {
    runes := make([]rune, n)
    for i := 0; i < n; i++ {
        runes[i] = 'a'
    }
    return string(runes)
}
```

---

## Performance Considerations

### Memory Usage

```go
s := "Hello, 世界"  // 13 bytes in memory

b := []byte(s)     // 13 bytes (copy of string)
r := []rune(s)     // 36 bytes (9 runes × 4 bytes each)

// Approximate memory:
// string:  13 bytes + header (16 bytes) = ~29 bytes
// []byte:  13 bytes + header (24 bytes) = ~37 bytes
// []rune:  36 bytes + header (24 bytes) = ~60 bytes
```

### Conversion Costs

```go
s := "Hello, 世界"

// String → []byte: O(n) copy
b := []byte(s)  // Copies all bytes

// String → []rune: O(n) decode + allocate
r := []rune(s)  // Decodes UTF-8, allocates 4× space

// []rune → string: O(n) encode
s2 := string(r)  // Encodes to UTF-8

// range over string: O(n) decode on-the-fly
for _, ch := range s {  // Decodes each rune incrementally
    _ = ch
}
```

### Benchmarks (Approximate)

| Operation | Time | Memory |
|-----------|------|--------|
| `len(string)` | O(1) | 0 |
| `utf8.RuneCountInString(s)` | O(n) | 0 |
| `[]byte(string)` | O(n) | n bytes |
| `[]rune(string)` | O(n) | 4n bytes |
| `range string` | O(n) | 0 |
| `string + string` | O(n+m) | n+m bytes |
| `strings.Builder` | O(n) amortized | n bytes |

---

## Best Practices

### ✅ DO

```go
// ✅ Use string for immutable text
var name string = "Alice"

// ✅ Use []byte for binary data, I/O
data, _ := os.ReadFile("file.bin")  // Returns []byte

// ✅ Use []rune when manipulating individual characters
func reverse(s string) string {
    runes := []rune(s)
    // ... reverse logic
    return string(runes)
}

// ✅ Use range to iterate over characters
for _, ch := range s {
    fmt.Printf("%c\n", ch)
}

// ✅ Use strings.Builder for efficient concatenation
var b strings.Builder
for i := 0; i < 1000; i++ {
    b.WriteString("data")
}

// ✅ Use utf8 package for UTF-8 operations
import "unicode/utf8"
count := utf8.RuneCountInString(s)

// ✅ Use rune for character literals
var newline rune = '\n'
var emoji rune = '🎉'
```

### ❌ DON'T

```go
// ❌ Don't index strings expecting characters
ch := s[5]  // Gets byte, not character!

// ❌ Don't use len() to count characters
count := len(s)  // Counts bytes!

// ❌ Don't concatenate strings in loops
s := ""
for i := 0; i < 1000; i++ {
    s += "data"  // Very slow!
}

// ❌ Don't slice strings without considering UTF-8
substr := s[3:7]  // Might split multi-byte character!

// ❌ Don't convert to []rune unless necessary
r := []rune(s)  // Expensive! Only if you need to modify
```

---

## Quick Reference Card

### Type Sizes

```go
bool       // 1 byte
int8       // 1 byte
int16      // 2 bytes
int32      // 4 bytes
int64      // 8 bytes
uint8      // 1 byte
uint16     // 2 bytes
uint32     // 4 bytes
uint64     // 8 bytes
byte       // 1 byte (alias for uint8)
rune       // 4 bytes (alias for int32)
float32    // 4 bytes
float64    // 8 bytes
complex64  // 8 bytes
complex128 // 16 bytes
string     // 16 bytes (header) + data
```

### Common Operations

```go
// String length (bytes)
len(s)

// Character count
utf8.RuneCountInString(s)
len([]rune(s))

// Iterate characters
for _, ch := range s { }

// Convert types
[]byte(s)
[]rune(s)
string(bytes)
string(runes)

// Character at position
runes := []rune(s)
ch := runes[i]

// Substring by characters
string([]rune(s)[start:end])

// Build strings
var b strings.Builder
b.WriteString("text")
b.WriteRune('字')
result := b.String()
```

---

## Arrays

### What is an Array?

**Definition**: An **array** is a **fixed-size** sequence of elements of the same type.

```go
var arr [5]int  // Array of 5 integers
```

**Key conceptual points:**
1. **Fixed size**: Size is part of the type (`[5]int` ≠ `[10]int`)
2. **Value type**: Arrays are copied when assigned or passed to functions
3. **Contiguous memory**: Elements stored sequentially in memory
4. **Zero-indexed**: First element at index 0
5. **Rarely used directly**: Slices are preferred in most cases

### Why Fixed Size?

**Historical context**: Arrays in most languages (C, Java, etc.) have fixed sizes for performance reasons:

1. **Stack allocation**: Fixed-size arrays can live on the stack (fast)
2. **Cache efficiency**: Contiguous memory improves CPU cache hits
3. **Compile-time optimization**: Compiler knows exact memory layout

**Why Go made arrays value types:**

Most languages make arrays reference types (pointers). Go chose value semantics because:

1. **Predictability**: Assigning an array copies it (no hidden sharing)
2. **Safety**: Can't accidentally modify an array through another variable
3. **Simplicity**: No null array references (unlike Java, C#)

### Array Basics

```go
// Declaration
var arr1 [5]int              // [0, 0, 0, 0, 0] (zero values)
var arr2 [3]string           // ["", "", ""]

// Initialization
arr3 := [5]int{1, 2, 3, 4, 5}          // Explicit size
arr4 := [...]int{1, 2, 3}              // Compiler counts: [3]int
arr5 := [5]int{0: 10, 4: 50}           // Sparse: [10, 0, 0, 0, 50]

// Access
fmt.Println(arr3[0])   // 1
arr3[2] = 99           // [1, 2, 99, 4, 5]

// Length
fmt.Println(len(arr3)) // 5 (compile-time constant!)
```

### Arrays are Value Types

**Critical difference from other languages:**

```go
arr1 := [3]int{1, 2, 3}
arr2 := arr1  // COPIES entire array!

arr2[0] = 99
fmt.Println(arr1)  // [1, 2, 3]  (unchanged!)
fmt.Println(arr2)  // [99, 2, 3]
```

**Memory visualization:**
```
arr1: [1] [2] [3]  (address 0x1000)
arr2: [1] [2] [3]  (address 0x2000) ← Separate copy!
       ↓
arr2: [99] [2] [3] (arr1 unchanged)
```

**Function parameters:**
```go
func modify(arr [3]int) {
    arr[0] = 99  // Modifies the COPY
}

arr := [3]int{1, 2, 3}
modify(arr)
fmt.Println(arr)  // [1, 2, 3] (unchanged!)
```

To modify the original, use a pointer:
```go
func modifyPtr(arr *[3]int) {
    arr[0] = 99  // Modifies original
}

arr := [3]int{1, 2, 3}
modifyPtr(&arr)
fmt.Println(arr)  // [99, 2, 3]
```

### Size is Part of the Type

```go
var arr1 [3]int
var arr2 [5]int

// arr1 = arr2  // ❌ ERROR: cannot use arr2 (type [5]int) as type [3]int
```

**Why this matters:**
- Can't have a function that accepts "any size array"
- Must know size at compile time
- This limitation led to the creation of slices

### When to Use Arrays

**Use arrays when:**
1. Size is truly fixed and known at compile time
2. Need value semantics (automatic copying)
3. Working with low-level code (C interop, hardware)
4. Small, fixed-size mathematical constructs (3D points, RGB colors)

```go
// Good use cases:
type Point3D [3]float64    // Always 3 dimensions
type RGBColor [3]uint8     // Always Red, Green, Blue
type ChessBoard [8][8]int  // Always 8×8
```

**Don't use arrays when:**
- Size varies at runtime → Use slices
- Passing to functions frequently → Use slices (avoid copying)
- Need dynamic growth → Use slices

---

## Slices (Deep Dive)

### What is a Slice?

**Definition**: A **slice** is a **dynamically-sized**, flexible view into an underlying array.

```go
var s []int  // Slice (no size specified!)
```

**Key conceptual points:**
1. **Dynamic size**: Can grow and shrink at runtime
2. **Reference type**: Slices reference an underlying array
3. **Three components**: Pointer, length, capacity
4. **Most common collection**: 99% of the time, use slices instead of arrays
5. **Nil-able**: A slice can be `nil` (unlike arrays)

### Why Slices Exist

**The problem with arrays:**
```go
func process(data [1000]int) {  // Copies 1000 integers!
    // ...
}
```

Every function call copies the entire array. For large arrays, this is catastrophic for performance.

**The solution: Slices**

A slice is a **descriptor** that points to an array:

```go
// Slice implementation (runtime/slice.go):
type slice struct {
    array unsafe.Pointer  // Pointer to underlying array
    len   int            // Number of elements
    cap   int            // Capacity of underlying array
}
```

**Memory visualization:**
```
Slice variable (24 bytes):        Underlying array (heap):
┌─────────────────┐              ┌──┬──┬──┬──┬──┬──┐
│ ptr:  0x5000    │   ────────>  │10│20│30│40│50│60│
│ len:  4         │              └──┴──┴──┴──┴──┴──┘
│ cap:  6         │               ↑           ↑
└─────────────────┘               len=4      cap=6
```

**Why this is brilliant:**
1. Copying a slice only copies 24 bytes (ptr + len + cap)
2. Multiple slices can share the same underlying array
3. Slicing operations are O(1) (just adjust ptr/len/cap)

### Slice Basics

```go
// Declaration (nil slice)
var s1 []int             // nil, len=0, cap=0

// Literal initialization
s2 := []int{1, 2, 3, 4, 5}  // len=5, cap=5

// Using make (pre-allocate)
s3 := make([]int, 5)        // len=5, cap=5, [0,0,0,0,0]
s4 := make([]int, 3, 10)    // len=3, cap=10, [0,0,0]
//           type  len cap

// From array
arr := [5]int{1, 2, 3, 4, 5}
s5 := arr[1:4]  // [2, 3, 4] (slice of array)

// Nil check
if s1 == nil {
    fmt.Println("slice is nil")
}
```

### Length vs Capacity

**Length**: Number of elements currently in the slice  
**Capacity**: Number of elements in the underlying array (from slice start)

```go
s := make([]int, 3, 10)
fmt.Println(len(s))  // 3
fmt.Println(cap(s))  // 10

// Can access indices 0-2 (len)
fmt.Println(s[0])  // 0
fmt.Println(s[2])  // 0
// fmt.Println(s[5])  // ❌ PANIC: index out of range

// But capacity is 10 (can grow to 10 without reallocation)
s = append(s, 4, 5, 6, 7, 8, 9, 10)  // No reallocation!
fmt.Println(len(s))  // 10
fmt.Println(cap(s))  // 10
```

### Slicing Operations

```go
s := []int{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}

// Format: s[start:end]  (end is exclusive!)
s1 := s[2:5]   // [2, 3, 4]
s2 := s[:3]    // [0, 1, 2]  (from start)
s3 := s[7:]    // [7, 8, 9]  (to end)
s4 := s[:]     // [0...9]    (entire slice)

// Three-index slice: s[start:end:cap]
s5 := s[2:5:7]  // [2,3,4], cap=5 (7-2)
```

**Why slicing is O(1):**
```
Original:  ptr → [0][1][2][3][4][5][6][7][8][9]
                  ↑                           
                 len=10, cap=10

s[2:5]:    ptr → [0][1][2][3][4][5][6][7][8][9]
                        ↑     ↑
                       len=3, cap=8 (from index 2)
```

No copying! Just adjust pointer, length, capacity.

### Append and Growth

```go
s := []int{1, 2, 3}
fmt.Printf("len=%d cap=%d\n", len(s), cap(s))  // len=3 cap=3

s = append(s, 4)
fmt.Printf("len=%d cap=%d\n", len(s), cap(s))  // len=4 cap=6
//                                              Capacity doubled!
```

**How append works:**

1. **If capacity available**: Add element, increment length
2. **If capacity full**: 
   - Allocate new array (typically 2× capacity)
   - Copy all elements to new array
   - Add new element
   - Return new slice pointing to new array

**Growth strategy** (approximate):
```
Old cap → New cap
0       → 1
1       → 2
2-256   → 2× old cap
256+    → 1.25× old cap (reduces to ~1.25× for large slices)
```

**Why you should pre-allocate:**
```go
// ❌ SLOW - multiple reallocations
s := []int{}
for i := 0; i < 100000; i++ {
    s = append(s, i)  // Reallocates ~17 times!
}

// ✅ FAST - one allocation
s := make([]int, 0, 100000)  // len=0, cap=100000
for i := 0; i < 100000; i++ {
    s = append(s, i)  // No reallocations!
}
```

### Slice Sharing and Pitfalls

**Slices share underlying arrays:**
```go
s1 := []int{1, 2, 3, 4, 5}
s2 := s1[1:4]  // [2, 3, 4]

s2[0] = 99

fmt.Println(s1)  // [1, 99, 3, 4, 5]  ← Changed!
fmt.Println(s2)  // [99, 3, 4]
```

**Why?** Both slices point to the same underlying array:
```
s1: ptr → [1][2][3][4][5]
          len=5, cap=5

s2: ptr → [1][2][3][4][5]
             ↑ len=3, cap=4

Modifying s2[0] modifies the shared array element!
```

**Solution: Copy to avoid sharing**
```go
s1 := []int{1, 2, 3, 4, 5}
s2 := make([]int, 3)
copy(s2, s1[1:4])  // [2, 3, 4]

s2[0] = 99
fmt.Println(s1)  // [1, 2, 3, 4, 5]  ← Unchanged!
fmt.Println(s2)  // [99, 3, 4]
```

### Nil vs Empty Slice

```go
var s1 []int        // nil slice
s2 := []int{}       // empty slice (non-nil)
s3 := make([]int, 0) // empty slice (non-nil)

// All have len=0, cap=0
fmt.Println(len(s1), len(s2), len(s3))  // 0 0 0

// But nil check differs:
fmt.Println(s1 == nil)  // true
fmt.Println(s2 == nil)  // false
fmt.Println(s3 == nil)  // false
```

**When it matters:**
```go
// JSON encoding
json.Marshal(s1)  // null
json.Marshal(s2)  // []

// Append works the same on both
s1 = append(s1, 1)  // Works!
s2 = append(s2, 1)  // Works!
```

**Best practice:** Check length, not nil:
```go
if len(s) == 0 {  // Works for both nil and empty
    // ...
}
```

---

## Maps (Deep Dive)

### What is a Map?

**Definition**: A **map** is an unordered collection of **key-value pairs** with fast lookups.

```go
var m map[string]int  // Map from strings to integers
```

**Key conceptual points:**
1. **Hash table**: Implemented as a hash table (O(1) average lookups)
2. **Reference type**: Maps are references to hash table data structure
3. **Unordered**: Iteration order is randomized (intentionally!)
4. **Nil-able**: A map can be `nil` (cannot write to nil map!)
5. **Not thread-safe**: Need sync.RWMutex for concurrent access

### Why Maps Exist

**The problem:** How to efficiently store and retrieve data by key?

**Naive solution: Slice of pairs**
```go
type Pair struct { Key string; Value int }
pairs := []Pair{{"Alice", 30}, {"Bob", 25}}

// Lookup: O(n) - must scan entire slice!
for _, p := range pairs {
    if p.Key == "Alice" {
        fmt.Println(p.Value)
    }
}
```

**Map solution: Hash table**
```go
m := map[string]int{"Alice": 30, "Bob": 25}
age := m["Alice"]  // O(1) - instant lookup!
```

### How Hash Tables Work

**Conceptual explanation:**

1. **Hash function**: Convert key to number (hash code)
2. **Bucket selection**: Use hash code to choose a bucket
3. **Store value**: Put key-value pair in bucket
4. **Collision handling**: If bucket full, use linked list or probing

**Visual example:**
```
Hash("Alice") = 1234 → Bucket 4 → {"Alice": 30}
Hash("Bob")   = 5678 → Bucket 8 → {"Bob": 25}
Hash("Carol") = 1299 → Bucket 4 → Collision!
                       Bucket 4 → {"Alice": 30} → {"Carol": 28}
```

**Why O(1) lookup?**

Compute hash → Go to bucket → (Usually) find key immediately

Worst case: O(n) if all keys hash to same bucket (rare with good hash function)

### Map Basics

```go
// Declaration (nil map - cannot write!)
var m1 map[string]int  // nil

// Initialization with make
m2 := make(map[string]int)  // Empty map (can write)

// Literal initialization
m3 := map[string]int{
    "Alice": 30,
    "Bob":   25,
    "Carol": 28,
}

// Insert/Update
m3["David"] = 35       // Insert new key
m3["Alice"] = 31       // Update existing key

// Lookup
age := m3["Alice"]     // 31
missing := m3["Eve"]   // 0 (zero value for int)

// Check existence
age, exists := m3["Alice"]
if exists {
    fmt.Println("Alice is", age)
}

// Delete
delete(m3, "Bob")      // Remove key
delete(m3, "Unknown")  // Safe even if key doesn't exist

// Length
fmt.Println(len(m3))   // 3
```

### The Nil Map Trap

```go
var m map[string]int  // nil map

// Reading is safe
val := m["key"]       // Returns 0 (zero value)
_, exists := m["key"] // exists = false
fmt.Println(len(m))   // 0

// Writing PANICS!
m["key"] = 10  // ❌ PANIC: assignment to entry in nil map
```

**Why this design?**

Reading a nil map is defined to return zero values (convenient for optional configs). But writing would require allocating a map, which could hide bugs.

**Solution:**
```go
m := make(map[string]int)  // Always initialize before writing
```

### Iteration Order is Random

```go
m := map[string]int{"a": 1, "b": 2, "c": 3}

for k, v := range m {
    fmt.Println(k, v)
}
// Output order: UNPREDICTABLE!
// Run 1: a 1, c 3, b 2
// Run 2: b 2, a 1, c 3
```

**Why randomized?**

Go **intentionally** randomizes iteration order to prevent code from relying on order (which was never guaranteed). This catches bugs early.

**Need sorted iteration?**
```go
// Extract keys, sort, then iterate
keys := make([]string, 0, len(m))
for k := range m {
    keys = append(keys, k)
}
sort.Strings(keys)

for _, k := range keys {
    fmt.Println(k, m[k])
}
```

### Key Requirements

**Keys must be comparable** (support `==` operator):

```go
// ✅ Valid key types
map[string]int         // strings
map[int]string         // integers
map[float64]bool       // floats (careful with precision!)
map[rune]string        // runes
map[struct{}]int       // structs (if fields comparable)

type Point struct{ X, Y int }
map[Point]string       // ✅ OK (int fields are comparable)

// ❌ Invalid key types
map[[]int]string       // ❌ slices not comparable
map[map[string]int]int // ❌ maps not comparable

type BadKey struct{ Data []int }
map[BadKey]string      // ❌ struct has non-comparable field
```

**Why this restriction?**

Hash tables need to:
1. Hash the key (compute bucket)
2. Compare keys (find exact match in bucket)

Slices/maps don't have defined `==` behavior, so they can't be keys.

### Maps are Reference Types

```go
m1 := map[string]int{"Alice": 30}
m2 := m1  // Both reference the SAME map!

m2["Alice"] = 99
fmt.Println(m1["Alice"])  // 99 (changed!)
```

**Memory model:**
```
m1 → [Map Data Structure]
       ↑
m2 ────┘  (both point to same map)
```

**Function parameters:**
```go
func modify(m map[string]int) {
    m["Alice"] = 99  // Modifies original map!
}

m := map[string]int{"Alice": 30}
modify(m)
fmt.Println(m["Alice"])  // 99
```

No need for pointers - maps are already references!

### Map Performance

| Operation | Average | Worst Case |
|-----------|---------|------------|
| Lookup    | O(1)    | O(n) |
| Insert    | O(1)    | O(n) (rehash) |
| Delete    | O(1)    | O(n) |
| Iteration | O(n)    | O(n) |

**When to pre-allocate:**
```go
// If you know size, pre-allocate:
m := make(map[string]int, 10000)  // Reserve space for 10k entries

// Avoids multiple rehashes as map grows
```

---

## Pointers

### What is a Pointer?

**Definition**: A **pointer** is a variable that stores the **memory address** of another variable.

```go
var p *int  // Pointer to an integer
```

**Key conceptual points:**
1. **Memory address**: Pointers hold locations in memory
2. **Indirection**: Access value through `*p` (dereferencing)
3. **Pass by reference**: Pointers allow functions to modify original data
4. **Nil-able**: Pointers can be `nil` (no address)
5. **No pointer arithmetic**: Unlike C/C++ (safer but less flexible)

### Why Pointers Exist

**The fundamental problem:**

```go
func increment(x int) {
    x = x + 1  // Modifies the COPY
}

num := 10
increment(num)
fmt.Println(num)  // 10 (unchanged!)
```

Go passes by value. Functions receive copies of arguments.

**Solution: Pointers**

```go
func increment(x *int) {
    *x = *x + 1  // Modifies original through pointer
}

num := 10
increment(&num)  // Pass address
fmt.Println(num)  // 11 (changed!)
```

### Pointer Basics

```go
// Create variable
num := 42

// Get pointer with & (address-of operator)
p := &num
fmt.Printf("%p\n", p)  // 0xc000012345 (memory address)

// Dereference with * (value-at operator)
fmt.Println(*p)  // 42

// Modify through pointer
*p = 99
fmt.Println(num)  // 99 (original changed!)

// Nil pointer
var p2 *int
fmt.Println(p2 == nil)  // true
// fmt.Println(*p2)  // ❌ PANIC: nil pointer dereference
```

### Pointer Syntax

```go
var p *int     // * in type: "pointer to int"
p = &num       // & before variable: "address of num"
val := *p      // * before pointer: "value at p"
```

**Memory model:**
```
num (address 0x1000): [42]
                       ↑
p   (address 0x2000): [0x1000]
```

`p` contains the address `0x1000`, which points to `num`'s value `42`.

### When to Use Pointers

**Use pointers when:**

1. **Need to modify original**: Function must change caller's data
```go
func update(u *User) {
    u.Age = 30  // Modifies original User
}
```

2. **Avoid copying large structs**: Efficiency
```go
type LargeStruct struct {
    Data [1000000]int
}

// ❌ Copies 8MB!
func processSlow(ls LargeStruct) { }

// ✅ Copies 8 bytes (pointer)
func processFast(ls *LargeStruct) { }
```

3. **Optional values**: `nil` means "not set"
```go
type Config struct {
    Port *int  // nil = use default port
}
```

4. **Shared mutable state**: Multiple goroutines access same data
```go
type Counter struct {
    mu    sync.Mutex
    value int
}

func (c *Counter) Increment() {  // Must use pointer receiver
    c.mu.Lock()
    c.value++
    c.mu.Unlock()
}
```

**Don't use pointers when:**

- Small types (int, bool, string, small structs) - copying is cheap
- Immutable data - no modification needed
- Slices, maps, channels - already reference types (pointers inside)

### Pointer Receivers vs Value Receivers

```go
type Person struct {
    Name string
    Age  int
}

// Value receiver - receives copy
func (p Person) PrintAge() {
    fmt.Println(p.Age)
}

// Pointer receiver - receives pointer
func (p *Person) IncrementAge() {
    p.Age++  // Modifies original
}

person := Person{"Alice", 30}
person.PrintAge()      // 30
person.IncrementAge()  // Modifies person
person.PrintAge()      // 31
```

**Rule of thumb:**
- **Value receiver**: Method only reads data, struct is small
- **Pointer receiver**: Method modifies data, or struct is large, or consistency (if ANY method uses pointer, ALL should)

### Pointers and Nil

```go
var p *int
if p == nil {
    fmt.Println("pointer is nil")
}

// Safe to call methods on nil pointer (if method handles it!)
type Node struct {
    Value int
    Next  *Node
}

func (n *Node) Length() int {
    if n == nil {
        return 0  // Handle nil gracefully
    }
    return 1 + n.Next.Length()
}

var list *Node  // nil
fmt.Println(list.Length())  // 0 (works!)
```

### Pointers vs References (Other Languages)

**Go pointers are simpler than C/C++:**

```go
// ❌ Go does NOT have:
// - Pointer arithmetic: p++, p+5
// - Manual memory management: malloc/free
// - Multiple levels: **int, ***int (rarely needed)
// - Arrays of pointers require explicit []*int
```

**Go pointers are more explicit than Java/Python:**

```go
// Java: All objects are implicit references
// Go: Primitives and structs are values, pointers are explicit

// This clarity prevents hidden aliasing bugs!
```

---

## Structs

### What is a Struct?

**Definition**: A **struct** is a composite data type that groups together variables (fields) under a single name.

```go
type Person struct {
    Name string
    Age  int
}
```

**Key conceptual points:**
1. **Value type**: Structs are copied when assigned (like arrays)
2. **Fixed layout**: Fields defined at compile time
3. **No inheritance**: Go uses composition instead
4. **Memory contiguous**: Fields stored sequentially
5. **Exported fields**: Capitalized fields are public

### Struct Basics

```go
// Definition
type Person struct {
    Name    string
    Age     int
    Email   string
    private int  // Unexported (lowercase)
}

// Initialization
p1 := Person{"Alice", 30, "alice@example.com", 0}
p2 := Person{Name: "Bob", Age: 25}  // Named fields
p3 := Person{}  // Zero values: {"", 0, "", 0}

// Field access
fmt.Println(p1.Name)  // "Alice"
p1.Age = 31           // Modify field

// Pointer to struct
p := &Person{"Carol", 28, "carol@example.com", 0}
fmt.Println(p.Name)  // Auto-dereference! (syntactic sugar)
// Equivalent: (*p).Name
```

### Anonymous Structs

```go
// Define and initialize in one place
config := struct {
    Host string
    Port int
}{
    Host: "localhost",
    Port: 8080,
}

fmt.Println(config.Host)  // "localhost"
```

**Use cases:**
- One-time data structures
- Test fixtures
- JSON encoding/decoding templates

### Struct Tags

```go
type User struct {
    ID       int    `json:"id"`
    Username string `json:"username" db:"user_name" validate:"required"`
    Email    string `json:"email,omitempty"`
}

// Used by encoding/json, databases, validation libraries
```

---

## Summary

### Key Takeaways

**Primitive Types:**
1. **String** = immutable sequence of UTF-8 encoded bytes
2. **Rune** = int32 representing a Unicode code point (one character)
3. **Byte** = uint8 representing a raw byte of data
4. **len(string)** returns bytes, NOT characters
5. **range string** decodes UTF-8 and returns runes

**Composite Types:**
6. **Arrays** = fixed-size, value types, size is part of type
7. **Slices** = dynamic-size, reference type (ptr + len + cap), most common collection
8. **Maps** = hash tables, reference type, unordered, O(1) lookups
9. **Pointers** = memory addresses, enable pass-by-reference, nil-able
10. **Structs** = value types, composition over inheritance

**Best Practices:**
- Use **slices** instead of arrays (99% of the time)
- Use **[]rune** when you need to manipulate individual characters
- Use **[]byte** for binary data and I/O operations
- Use **strings.Builder** for efficient string concatenation
- Use **pointer receivers** when methods modify data or structs are large
- **Pre-allocate** slices and maps when size is known
- **Check length**, not nil, for slices
- **Initialize maps** with `make()` before writing

### Decision Tree

```
Need to work with text?
├─ Immutable? → Use string
├─ Need to modify characters? → Use []rune
├─ Need to count characters? → Use utf8.RuneCountInString() or len([]rune(s))
└─ Binary data / I/O? → Use []byte

Building strings?
├─ Single concatenation? → Use +
├─ Loop concatenation? → Use strings.Builder
└─ Fixed size? → Use []rune or []byte then convert
```

---

## Related Documentation

- [Go Sync Package Guide](go-sync-package-complete-guide.md)
- [Go crypto/md5 Package Guide](go-crypto-md5-package-complete-guide.md)
- [Go flag Package Guide](go-flag-package-complete-guide.md)

---

[← Back to Documentation](README.md) | [↑ Back to Index](../MASTER-INDEX.md)
