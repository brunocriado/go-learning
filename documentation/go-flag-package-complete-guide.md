# The Complete Guide to Go's `flag` Package

**Go Version:** 1.19+ (Compatible with 1.25.5)  
**Official Documentation:** https://pkg.go.dev/flag

---

## Table of Contents

1. [Introduction](#introduction)
2. [Core Concepts](#core-concepts)
3. [Command-Line Anatomy](#command-line-anatomy)
4. [Global Flags vs FlagSets](#global-flags-vs-flagsets)
5. [Flag Types Reference](#flag-types-reference)
6. [Parsing Mechanisms](#parsing-mechanisms)
7. [FlagSet Deep Dive](#flagset-deep-dive)
8. [Positional Arguments](#positional-arguments)
9. [Error Handling](#error-handling)
10. [Custom Usage Messages](#custom-usage-messages)
11. [Advanced Features](#advanced-features)
12. [Best Practices](#best-practices)
13. [Complete Examples](#complete-examples)
14. [Common Patterns](#common-patterns)
15. [Troubleshooting](#troubleshooting)

---

## Introduction

The `flag` package is Go's built-in library for parsing command-line arguments. Unlike many languages that require external libraries for CLI parsing, Go provides a robust, type-safe solution in its standard library.

**What flag does:**
- Parses command-line arguments into Go types
- Generates automatic help messages
- Validates input types
- Supports subcommands (via FlagSets)
- Provides both pointer-based and variable-based flag definitions

**What flag does NOT do:**
- Complex nested subcommands (use libraries like cobra/cli for that)
- Automatic completion generation
- Flag aliases (can't have both `-v` and `--verbose` for same flag)
- POSIX-style flag bundling (`-abc` for `-a -b -c`)

---

## Core Concepts

### What is a Flag?

A flag is a command-line option that modifies program behavior:

```bash
program -name=value
program --name value
program -enable
```

### Flag vs Argument

```bash
./program -flag value argument1 argument2
          └─ flag ─┘ └── arguments ──┘
```

- **Flags**: Named options (start with `-` or `--`)
- **Arguments**: Positional values (no dash prefix)

### The Flag Structure

Every flag has:
1. **Name**: How it appears on command line (`-name`)
2. **Type**: What Go type it represents (`string`, `int`, `bool`, etc.)
3. **Default**: Value if flag not provided
4. **Usage**: Help text describing the flag

---

## Command-Line Anatomy

Understanding `os.Args`:

```go
// Command: ./myapp server -port=8080 -verbose config.yaml

os.Args[0] = "./myapp"      // Program name
os.Args[1] = "server"       // First argument (could be subcommand)
os.Args[2] = "-port=8080"   // Flag with value
os.Args[3] = "-verbose"     // Boolean flag
os.Args[4] = "config.yaml"  // Positional argument
```

**Flag Syntax Variations:**

All these are equivalent:
```bash
-flag value
-flag=value
--flag value
--flag=value
```

**Boolean Flags:**
```bash
-enable              # Sets to true
-enable=true         # Explicit true
-enable=false        # Explicit false
-enable=1            # Also true
-enable=0            # Also false
```

**Integer Flags Accept:**
```bash
-count=42            # Decimal
-count=0644          # Octal (leading 0)
-count=0x2A          # Hexadecimal
-count=-10           # Negative
```

**Duration Flags:**
```bash
-timeout=30s         # 30 seconds
-timeout=1.5h        # 1.5 hours
-timeout=500ms       # Milliseconds
```

**Flag Parsing Stops At:**
- First non-flag argument (doesn't start with `-`)
- The `--` terminator
- An error in flag parsing

Example:
```bash
./program -flag1 value1 arg1 -flag2 value2
                        ↑
                 Parsing stops here!
                 -flag2 becomes a positional argument
```

---

## Global Flags vs FlagSets

### Approach 1: Global Flags (Simple Programs)

**Use when:** Your program has one set of flags that apply to everything.

```go
package main

import (
    "flag"
    "fmt"
)

func main() {
    // Define flags
    name := flag.String("name", "World", "person to greet")
    count := flag.Int("count", 1, "number of times")
    verbose := flag.Bool("verbose", false, "verbose output")
    
    // Parse ALL flags from os.Args[1:]
    flag.Parse()
    
    // Use flags (they're pointers!)
    for i := 0; i < *count; i++ {
        fmt.Printf("Hello, %s!\n", *name)
    }
    
    if *verbose {
        fmt.Println("Done!")
    }
}
```

**Usage:**
```bash
./program -name=Alice -count=3 -verbose
# Output:
# Hello, Alice!
# Hello, Alice!
# Hello, Alice!
# Done!
```

**Global Flag Functions:**
- `flag.String()`, `flag.Int()`, `flag.Bool()`, etc.
- `flag.Parse()` - Must call before accessing flags
- `flag.Arg(i)` - Access positional arguments
- `flag.Args()` - All positional arguments as slice

---

### Approach 2: FlagSets (Subcommands)

**Use when:** Your program has different commands with different flags (like git, docker, kubectl).

```go
package main

import (
    "flag"
    "fmt"
    "os"
)

func main() {
    // Check if subcommand provided
    if len(os.Args) < 2 {
        fmt.Println("expected 'start' or 'stop' subcommands")
        os.Exit(1)
    }

    // Create separate FlagSets for each subcommand
    startCmd := flag.NewFlagSet("start", flag.ExitOnError)
    stopCmd := flag.NewFlagSet("stop", flag.ExitOnError)

    // 'start' command flags
    startPort := startCmd.Int("port", 8080, "server port")
    startVerbose := startCmd.Bool("verbose", false, "verbose logging")

    // 'stop' command flags
    stopForce := stopCmd.Bool("force", false, "force shutdown")
    stopTimeout := stopCmd.Duration("timeout", 30*time.Second, "shutdown timeout")

    // Route to appropriate subcommand
    switch os.Args[1] {
    case "start":
        startCmd.Parse(os.Args[2:])  // Parse flags AFTER 'start'
        fmt.Printf("Starting server on port %d\n", *startPort)
        if *startVerbose {
            fmt.Println("Verbose mode enabled")
        }

    case "stop":
        stopCmd.Parse(os.Args[2:])   // Parse flags AFTER 'stop'
        fmt.Printf("Stopping server (force=%v, timeout=%v)\n", 
            *stopForce, *stopTimeout)

    default:
        fmt.Printf("Unknown command: %s\n", os.Args[1])
        os.Exit(1)
    }
}
```

**Usage:**
```bash
./program start -port=3000 -verbose
# Starting server on port 3000
# Verbose mode enabled

./program stop -force -timeout=10s
# Stopping server (force=true, timeout=10s)
```

**Why Use FlagSets?**

1. **Isolation**: Each subcommand has its own flags
2. **No Conflicts**: `start -verbose` and `stop -verbose` are separate
3. **Clear Help**: Each subcommand can have its own help text
4. **Scalability**: Easy to add new subcommands

---

## Flag Types Reference

### All Available Types

| Function | Return Type | Use Case | Example |
|----------|-------------|----------|---------|
| `flag.Bool()` | `*bool` | Enable/disable features | `-debug` |
| `flag.Int()` | `*int` | Counts, IDs | `-port=8080` |
| `flag.Int64()` | `*int64` | Large numbers | `-size=9999999999` |
| `flag.Uint()` | `*uint` | Positive numbers | `-count=10` |
| `flag.Uint64()` | `*uint64` | Large positive | `-bytes=1000000` |
| `flag.Float64()` | `*float64` | Decimals | `-rate=0.05` |
| `flag.String()` | `*string` | Text values | `-name=Alice` |
| `flag.Duration()` | `*time.Duration` | Time periods | `-timeout=30s` |

### Function Signatures

**Pattern 1: Return Pointer**
```go
func String(name string, value string, usage string) *string
```

**Pattern 2: Modify Variable (Var functions)**
```go
func StringVar(p *string, name string, value string, usage string)
```

### Detailed Examples

#### Bool Flags

```go
// Method 1: Get pointer
debug := flag.Bool("debug", false, "enable debug mode")
flag.Parse()
if *debug {
    fmt.Println("Debug enabled")
}

// Method 2: Bind to variable
var verbose bool
flag.BoolVar(&verbose, "verbose", false, "verbose output")
flag.Parse()
if verbose {
    fmt.Println("Verbose enabled")
}
```

**Usage:**
```bash
./program -debug              # Sets to true
./program -debug=true         # Explicit true
./program -debug=false        # Explicit false
./program -debug=1            # Also true (1, t, T, TRUE, True)
./program -debug=0            # Also false (0, f, F, FALSE, False)
```

#### Integer Flags

```go
port := flag.Int("port", 8080, "server port")
workers := flag.Int64("workers", 10, "number of workers")
retries := flag.Uint("retries", 3, "max retries")

flag.Parse()

fmt.Printf("Port: %d\n", *port)
fmt.Printf("Workers: %d\n", *workers)
fmt.Printf("Retries: %d\n", *retries)
```

**Usage:**
```bash
./program -port=3000 -workers=100 -retries=5
```

**Accepted Formats:**
```bash
-port=8080       # Decimal
-port=0600       # Octal (leading 0)
-port=0x1F90     # Hexadecimal
-count=-5        # Negative (for Int/Int64)
```

#### String Flags

```go
name := flag.String("name", "default", "user name")
file := flag.String("file", "", "input file path")

flag.Parse()

if *name == "default" {
    fmt.Println("Using default name")
}

if *file == "" {
    fmt.Println("No file specified")
}
```

#### Duration Flags

```go
import "time"

timeout := flag.Duration("timeout", 30*time.Second, "operation timeout")
interval := flag.Duration("interval", 5*time.Minute, "check interval")

flag.Parse()

fmt.Printf("Will timeout after: %v\n", *timeout)

// Use in time operations
time.Sleep(*interval)
```

**Usage:**
```bash
./program -timeout=1m30s      # 1 minute 30 seconds
./program -timeout=500ms      # 500 milliseconds
./program -timeout=2h         # 2 hours
./program -interval=1.5h      # 1 hour 30 minutes
```

**Valid Duration Units:**
- `ns` - nanoseconds
- `us` / `µs` - microseconds
- `ms` - milliseconds
- `s` - seconds
- `m` - minutes
- `h` - hours

#### Float Flags

```go
rate := flag.Float64("rate", 0.05, "sampling rate (0.0-1.0)")
threshold := flag.Float64("threshold", 99.9, "accuracy threshold")

flag.Parse()

if *rate < 0.0 || *rate > 1.0 {
    fmt.Println("Rate must be between 0.0 and 1.0")
    os.Exit(1)
}
```

---

## Parsing Mechanisms

### flag.Parse() - Global Parsing

```go
import (
    "flag"
    "fmt"
)

var (
    name    = flag.String("name", "World", "name to greet")
    excited = flag.Bool("excited", false, "add exclamation")
)

func main() {
    // Parse MUST be called before accessing flags
    flag.Parse()
    
    greeting := fmt.Sprintf("Hello, %s", *name)
    if *excited {
        greeting += "!"
    }
    fmt.Println(greeting)
}
```

**When to call Parse():**
- After all flags are defined
- Before accessing any flag values
- Only call once per program

**What Parse() does:**
1. Iterates through `os.Args[1:]`
2. Matches arguments to defined flags
3. Converts string values to proper types
4. Sets flag pointers to their values
5. Stores remaining args for `flag.Arg()`/`flag.Args()`

### FlagSet.Parse() - Subcommand Parsing

```go
createCmd := flag.NewFlagSet("create", flag.ExitOnError)
name := createCmd.String("name", "", "resource name")

// Parse from os.Args[2:] (skip program name and subcommand)
createCmd.Parse(os.Args[2:])

fmt.Printf("Creating resource: %s\n", *name)
```

**Why os.Args[2:]?**
```
./program create -name=foo
   [0]     [1]     [2]

os.Args[0] = "./program"  (skip - program name)
os.Args[1] = "create"     (skip - already handled in switch)
os.Args[2:] = ["-name=foo"]  (parse these!)
```

### Parsing Errors

```go
// With flag.ExitOnError (default)
fs := flag.NewFlagSet("cmd", flag.ExitOnError)
fs.Parse(args)  // Exits program on error

// With flag.ContinueOnError (custom handling)
fs := flag.NewFlagSet("cmd", flag.ContinueOnError)
err := fs.Parse(args)
if err != nil {
    fmt.Fprintf(os.Stderr, "Parse error: %v\n", err)
    // Custom error handling
}

// With flag.PanicOnError (for testing)
fs := flag.NewFlagSet("cmd", flag.PanicOnError)
fs.Parse(args)  // Panics on error (useful in tests)
```

---

## FlagSet Deep Dive

### Creating a FlagSet

```go
func NewFlagSet(name string, errorHandling ErrorHandling) *FlagSet
```

**Parameters:**

1. **name**: Name of the command (used in error messages)
   ```go
   fs := flag.NewFlagSet("upload", flag.ExitOnError)
   // Error: "flag provided but not defined: -xyz in upload"
   ```

2. **errorHandling**: How to handle parsing errors
   - `flag.ContinueOnError` - Return error, continue execution
   - `flag.ExitOnError` - Print error and call `os.Exit(2)`
   - `flag.PanicOnError` - Panic (useful for tests)

### FlagSet Methods

All global `flag.*` functions have FlagSet equivalents:

```go
fs := flag.NewFlagSet("mycommand", flag.ExitOnError)

// Define flags
name := fs.String("name", "", "name")
count := fs.Int("count", 0, "count")
enabled := fs.Bool("enabled", false, "enabled")

// Parse
fs.Parse(os.Args[2:])

// Access positional args
arg1 := fs.Arg(0)           // First positional arg
allArgs := fs.Args()        // All positional args
numArgs := fs.NArg()        // Count of positional args

// Query flags
numFlags := fs.NFlag()      // How many flags were SET
parsed := fs.Parsed()       // Has Parse been called?

// Lookup specific flag
if f := fs.Lookup("name"); f != nil {
    fmt.Printf("Flag 'name' exists with value: %s\n", f.Value)
}
```

### FlagSet Usage Customization

```go
fs := flag.NewFlagSet("deploy", flag.ExitOnError)

// Custom usage function
fs.Usage = func() {
    fmt.Fprintf(os.Stderr, "Usage: myapp deploy [OPTIONS]\n\n")
    fmt.Fprintf(os.Stderr, "Deploy application to production.\n\n")
    fmt.Fprintf(os.Stderr, "Options:\n")
    fs.PrintDefaults()
    fmt.Fprintf(os.Stderr, "\nExamples:\n")
    fmt.Fprintf(os.Stderr, "  myapp deploy -env=prod -version=1.2.3\n")
}

env := fs.String("env", "staging", "target environment")
version := fs.String("version", "latest", "version to deploy")

fs.Parse(os.Args[2:])
```

**Triggering Usage:**
```bash
./program deploy -h        # Automatic help flag
./program deploy --help    # Also works
./program deploy -unknown  # On error (with ExitOnError)
```

### Setting Output Destination

```go
fs := flag.NewFlagSet("cmd", flag.ContinueOnError)

// Redirect output (default is os.Stderr)
var buf bytes.Buffer
fs.SetOutput(&buf)

// Now errors and help go to buffer
fs.Parse(invalidArgs)
fmt.Println(buf.String())
```

---

## Positional Arguments

Arguments that come after flags (or that aren't flags).

### Accessing Positional Args

```go
// Global flags
flag.Parse()

arg1 := flag.Arg(0)          // First arg after flags
arg2 := flag.Arg(1)          // Second arg after flags
allArgs := flag.Args()       // []string of all args
count := flag.NArg()         // Number of args

// FlagSet
fs := flag.NewFlagSet("cmd", flag.ExitOnError)
fs.Parse(os.Args[2:])

arg1 := fs.Arg(0)
allArgs := fs.Args()
count := fs.NArg()
```

### Example: Search Command

```go
package main

import (
    "flag"
    "fmt"
    "os"
)

func main() {
    if len(os.Args) < 2 {
        fmt.Println("expected 'search' subcommand")
        os.Exit(1)
    }

    searchCmd := flag.NewFlagSet("search", flag.ExitOnError)
    caseSensitive := searchCmd.Bool("case", false, "case sensitive search")
    regex := searchCmd.Bool("regex", false, "use regex")

    switch os.Args[1] {
    case "search":
        searchCmd.Parse(os.Args[2:])

        // Check for required positional argument
        if searchCmd.NArg() < 1 {
            fmt.Println("Error: search term required")
            searchCmd.Usage()
            os.Exit(1)
        }

        searchTerm := searchCmd.Arg(0)  // First positional arg
        files := searchCmd.Args()[1:]   // Remaining args are files

        fmt.Printf("Searching for: %s\n", searchTerm)
        fmt.Printf("Case sensitive: %v\n", *caseSensitive)
        fmt.Printf("Use regex: %v\n", *regex)
        
        if len(files) > 0 {
            fmt.Printf("In files: %v\n", files)
        } else {
            fmt.Println("Searching in current directory")
        }

    default:
        fmt.Printf("Unknown command: %s\n", os.Args[1])
        os.Exit(1)
    }
}
```

**Usage:**
```bash
./program search -case -regex "pattern" file1.txt file2.txt
# Searching for: pattern
# Case sensitive: true
# Use regex: true
# In files: [file1.txt file2.txt]
```

### Mixing Flags and Arguments

**Flags must come BEFORE arguments:**
```bash
./program -flag value arg1 arg2    # ✅ Correct
./program arg1 -flag value arg2    # ❌ Wrong! -flag becomes arg
```

**To include arguments that look like flags:**
```bash
./program -- -this-looks-like-flag-but-isnt
               ↑
          Everything after -- is an argument
```

Example:
```go
flag.Parse()

// Command: ./program -name=foo -- -bar
// flag.Arg(0) = "-bar" (it's an argument, not a flag!)
```

---

## Error Handling

### Three Error Handling Strategies

#### 1. ExitOnError (Default, Recommended for Most Programs)

```go
fs := flag.NewFlagSet("cmd", flag.ExitOnError)

// Automatically exits on error with:
// - Exit code 2 for parse errors
// - Exit code 0 for -h/-help
```

**Behavior:**
```bash
./program cmd -invalid
# Error: flag provided but not defined: -invalid
# Usage of cmd:
#   ... help text ...
# [Program exits with code 2]
```

#### 2. ContinueOnError (Custom Error Handling)

```go
fs := flag.NewFlagSet("cmd", flag.ContinueOnError)

err := fs.Parse(os.Args[2:])
if err != nil {
    if err == flag.ErrHelp {
        // User requested help with -h
        os.Exit(0)
    }
    
    // Custom error handling
    fmt.Fprintf(os.Stderr, "Configuration error: %v\n", err)
    fmt.Fprintf(os.Stderr, "Run 'program cmd -h' for usage\n")
    os.Exit(1)
}
```

#### 3. PanicOnError (Testing Only)

```go
fs := flag.NewFlagSet("cmd", flag.PanicOnError)

// Panics on error - useful for tests
// Tests can recover() from panic
```

### Validating Flag Values

Flags only validate TYPE, not VALUE. You must validate ranges/constraints:

```go
port := flag.Int("port", 8080, "server port")
threads := flag.Int("threads", 4, "worker threads")
name := flag.String("name", "", "username")

flag.Parse()

// Validate port range
if *port < 1 || *port > 65535 {
    fmt.Fprintf(os.Stderr, "Error: port must be between 1 and 65535\n")
    flag.Usage()
    os.Exit(1)
}

// Validate positive values
if *threads < 1 {
    fmt.Fprintf(os.Stderr, "Error: threads must be positive\n")
    os.Exit(1)
}

// Validate required flags
if *name == "" {
    fmt.Fprintf(os.Stderr, "Error: -name is required\n")
    flag.Usage()
    os.Exit(1)
}
```

### The ErrHelp Constant

```go
var ErrHelp = errors.New("flag: help requested")
```

Returned when `-h` or `-help` is used but not defined as a flag.

```go
fs := flag.NewFlagSet("cmd", flag.ContinueOnError)
err := fs.Parse(args)

if err == flag.ErrHelp {
    // User wants help
    os.Exit(0)  // Exit cleanly
}
```

---

## Custom Usage Messages

### Default Usage Output

By default, `-h` or `--help` produces:

```
Usage of program:
  -name string
        user name (default "guest")
  -port int
        server port (default 8080)
  -verbose
        enable verbose output
```

### Customizing Usage

```go
package main

import (
    "flag"
    "fmt"
    "os"
)

func main() {
    // Override global Usage function
    flag.Usage = func() {
        fmt.Fprintf(os.Stderr, "MyApp - A tool for doing things\n\n")
        fmt.Fprintf(os.Stderr, "Usage: %s [OPTIONS] COMMAND\n\n", os.Args[0])
        fmt.Fprintf(os.Stderr, "Options:\n")
        flag.PrintDefaults()
        fmt.Fprintf(os.Stderr, "\nCommands:\n")
        fmt.Fprintf(os.Stderr, "  start    Start the service\n")
        fmt.Fprintf(os.Stderr, "  stop     Stop the service\n")
        fmt.Fprintf(os.Stderr, "\nExamples:\n")
        fmt.Fprintf(os.Stderr, "  %s -port=3000 start\n", os.Args[0])
        fmt.Fprintf(os.Stderr, "  %s -verbose stop\n", os.Args[0])
    }

    port := flag.Int("port", 8080, "server port")
    verbose := flag.Bool("verbose", false, "verbose logging")

    flag.Parse()

    // ... rest of program
}
```

### Per-FlagSet Usage

```go
createCmd := flag.NewFlagSet("create", flag.ExitOnError)

createCmd.Usage = func() {
    fmt.Fprintf(os.Stderr, "Usage: program create [OPTIONS]\n\n")
    fmt.Fprintf(os.Stderr, "Create a new resource.\n\n")
    fmt.Fprintf(os.Stderr, "Options:\n")
    createCmd.PrintDefaults()
}

name := createCmd.String("name", "", "resource name (required)")
typ := createCmd.String("type", "default", "resource type")

createCmd.Parse(os.Args[2:])
```

### Customizing Flag Help Text

Use backticks for parameter names:

```go
// Without backticks
flag.String("input", "", "search directory for files")
// Output: -input string
//             search directory for files

// With backticks
flag.String("input", "", "search `directory` for files")
// Output: -input directory
//             search directory for files
```

---

## Advanced Features

### Visit and VisitAll

Iterate over flags:

```go
// VisitAll - all defined flags
flag.VisitAll(func(f *flag.Flag) {
    fmt.Printf("Flag: %s (default: %s)\n", f.Name, f.DefValue)
})

// Visit - only flags that were SET by user
flag.Visit(func(f *flag.Flag) {
    fmt.Printf("User set: %s = %s\n", f.Name, f.Value)
})
```

**Example: Detecting What User Actually Set**

```go
port := flag.Int("port", 8080, "server port")
flag.Parse()

wasSet := false
flag.Visit(func(f *flag.Flag) {
    if f.Name == "port" {
        wasSet = true
    }
})

if wasSet {
    fmt.Printf("User specified port: %d\n", *port)
} else {
    fmt.Printf("Using default port: %d\n", *port)
}
```

### Programmatically Setting Flags

```go
fs := flag.NewFlagSet("cmd", flag.ExitOnError)
port := fs.Int("port", 8080, "port")

// Set programmatically (before Parse)
fs.Set("port", "3000")

fs.Parse([]string{})  // Parse empty args

fmt.Println(*port)  // 3000
```

### Checking If Parse Was Called

```go
if flag.Parsed() {
    fmt.Println("Flags have been parsed")
} else {
    fmt.Println("Must call flag.Parse() first!")
}
```

### Custom Flag Types (Advanced)

Implement the `flag.Value` interface:

```go
type Value interface {
    String() string
    Set(string) error
}
```

**Example: Slice Flag**

```go
type SliceFlag []string

func (s *SliceFlag) String() string {
    return strings.Join(*s, ",")
}

func (s *SliceFlag) Set(value string) error {
    *s = append(*s, value)
    return nil
}

// Usage
var tags SliceFlag
flag.Var(&tags, "tag", "tags (can be repeated)")
flag.Parse()

// ./program -tag=foo -tag=bar -tag=baz
// tags = ["foo", "bar", "baz"]
```

---

## Best Practices

### 1. Define Flags at Package Level (Global Flags)

```go
var (
    configFile = flag.String("config", "config.yaml", "config file")
    verbose    = flag.Bool("verbose", false, "verbose output")
)

func main() {
    flag.Parse()
    // Use *configFile and *verbose
}
```

### 2. Validate Early, Fail Fast

```go
flag.Parse()

// Validate immediately after parsing
if *port < 1024 {
    fmt.Fprintln(os.Stderr, "Error: port must be >= 1024")
    os.Exit(1)
}
```

### 3. Always Provide Usage Text

```go
// ✅ Good
port := flag.Int("port", 8080, "server port (1024-65535)")

// ❌ Bad
port := flag.Int("port", 8080, "")
```

### 4. Use Sensible Defaults

```go
// ✅ Good - works out of the box
port := flag.Int("port", 8080, "server port")

// ❌ Bad - requires user to always set
port := flag.Int("port", 0, "server port (required)")
```

### 5. Print Errors to os.Stderr

```go
// ✅ Correct
fmt.Fprintf(os.Stderr, "Error: %v\n", err)

// ❌ Wrong
fmt.Printf("Error: %v\n", err)  // Errors go to stdout
```

### 6. Consistent Naming

```go
// ✅ Use lowercase, hyphen-separated
flag.String("config-file", "config.yaml", "...")
flag.Bool("verbose-mode", false, "...")

// ❌ Avoid camelCase or underscores
flag.String("configFile", "", "...")   // Bad
flag.String("config_file", "", "...")  // Bad
```

### 7. Order Matters for Subcommands

```bash
# ✅ Correct order
./program subcommand -flag value

# ❌ Wrong order
./program -flag subcommand value  # Won't work as expected
```

### 8. Document Your CLI

Create a `printHelp()` function:

```go
func printHelp() {
    fmt.Println("MyApp - Description of your app")
    fmt.Println("\nUsage:")
    fmt.Println("  myapp [OPTIONS] COMMAND")
    fmt.Println("\nCommands:")
    fmt.Println("  start    Start the server")
    fmt.Println("  stop     Stop the server")
    fmt.Println("\nOptions:")
    flag.PrintDefaults()
}
```

---

## Complete Examples

### Example 1: Simple Server

```go
package main

import (
    "flag"
    "fmt"
    "log"
    "net/http"
    "os"
)

func main() {
    // Define flags
    port := flag.Int("port", 8080, "server port")
    host := flag.String("host", "localhost", "server host")
    verbose := flag.Bool("verbose", false, "verbose logging")

    // Parse
    flag.Parse()

    // Validate
    if *port < 1024 || *port > 65535 {
        fmt.Fprintln(os.Stderr, "Error: port must be 1024-65535")
        os.Exit(1)
    }

    // Start server
    addr := fmt.Sprintf("%s:%d", *host, *port)
    
    if *verbose {
        log.Printf("Starting server on %s\n", addr)
    }

    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        if *verbose {
            log.Printf("Request: %s %s\n", r.Method, r.URL.Path)
        }
        fmt.Fprintf(w, "Hello from %s\n", addr)
    })

    log.Fatal(http.ListenAndServe(addr, nil))
}
```

### Example 2: File Processor with Subcommands

```go
package main

import (
    "flag"
    "fmt"
    "os"
)

func main() {
    if len(os.Args) < 2 {
        printUsage()
        os.Exit(1)
    }

    // Create subcommands
    compressCmd := flag.NewFlagSet("compress", flag.ExitOnError)
    extractCmd := flag.NewFlagSet("extract", flag.ExitOnError)

    // Compress flags
    compressLevel := compressCmd.Int("level", 5, "compression level (1-9)")
    compressOutput := compressCmd.String("output", "", "output file")

    // Extract flags
    extractDest := extractCmd.String("dest", ".", "destination directory")
    extractVerbose := extractCmd.Bool("verbose", false, "verbose output")

    // Route commands
    switch os.Args[1] {
    case "compress":
        compressCmd.Parse(os.Args[2:])
        
        if compressCmd.NArg() < 1 {
            fmt.Fprintln(os.Stderr, "Error: input file required")
            compressCmd.Usage()
            os.Exit(1)
        }

        inputFile := compressCmd.Arg(0)
        outputFile := *compressOutput
        if outputFile == "" {
            outputFile = inputFile + ".gz"
        }

        fmt.Printf("Compressing %s to %s (level %d)\n", 
            inputFile, outputFile, *compressLevel)
        // ... compression logic

    case "extract":
        extractCmd.Parse(os.Args[2:])
        
        if extractCmd.NArg() < 1 {
            fmt.Fprintln(os.Stderr, "Error: archive file required")
            extractCmd.Usage()
            os.Exit(1)
        }

        archiveFile := extractCmd.Arg(0)
        
        fmt.Printf("Extracting %s to %s\n", archiveFile, *extractDest)
        if *extractVerbose {
            fmt.Println("Verbose mode enabled")
        }
        // ... extraction logic

    case "help", "-h", "--help":
        printUsage()

    default:
        fmt.Fprintf(os.Stderr, "Unknown command: %s\n", os.Args[1])
        printUsage()
        os.Exit(1)
    }
}

func printUsage() {
    fmt.Println("File Compressor - Compress and extract files")
    fmt.Println("\nUsage:")
    fmt.Println("  filecomp compress [OPTIONS] FILE")
    fmt.Println("  filecomp extract [OPTIONS] ARCHIVE")
    fmt.Println("\nCommands:")
    fmt.Println("  compress    Compress a file")
    fmt.Println("  extract     Extract an archive")
    fmt.Println("  help        Show this help")
}
```

---

## Common Patterns

### Pattern 1: Required Flags

```go
name := flag.String("name", "", "username (required)")
flag.Parse()

if *name == "" {
    fmt.Fprintln(os.Stderr, "Error: -name is required")
    flag.Usage()
    os.Exit(1)
}
```

### Pattern 2: Mutually Exclusive Flags

```go
json := flag.Bool("json", false, "output as JSON")
xml := flag.Bool("xml", false, "output as XML")
flag.Parse()

if *json && *xml {
    fmt.Fprintln(os.Stderr, "Error: cannot use both -json and -xml")
    os.Exit(1)
}
```

### Pattern 3: Default Behavior with Flags

```go
all := flag.Bool("all", false, "show all items")
pending := flag.Bool("pending", false, "show pending items")
completed := flag.Bool("completed", false, "show completed items")
flag.Parse()

if *all {
    showAll()
} else if *pending {
    showPending()
} else if *completed {
    showCompleted()
} else {
    // Default behavior if no flags
    showPending()  // Show pending by default
}
```

### Pattern 4: Dry Run Mode

```go
dryRun := flag.Bool("dry-run", false, "show what would be done")
flag.Parse()

files := getFilesToDelete()

if *dryRun {
    fmt.Println("Would delete:")
    for _, f := range files {
        fmt.Println("  ", f)
    }
} else {
    fmt.Println("Deleting:")
    for _, f := range files {
        fmt.Println("  ", f)
        os.Remove(f)
    }
}
```

### Pattern 5: Config File Override

```go
configFile := flag.String("config", "default.yaml", "config file")
host := flag.String("host", "", "override host from config")
port := flag.Int("port", 0, "override port from config")

flag.Parse()

// Load config
config := loadConfig(*configFile)

// Command-line flags override config
if *host != "" {
    config.Host = *host
}
if *port != 0 {
    config.Port = *port
}
```

---

## Troubleshooting

### Problem: Flags After Subcommand Don't Work

```bash
./program upload file.txt -verbose
# -verbose is treated as an argument, not a flag!
```

**Solution:** Put flags before arguments:
```bash
./program upload -verbose file.txt
```

### Problem: Flag Value Contains Spaces

```bash
./program -name "John Doe"   # ✅ Correct (quoted)
./program -name=John Doe     # ❌ Wrong! "Doe" becomes argument
./program -name="John Doe"   # ✅ Correct (quoted)
```

### Problem: Boolean Flag Isn't Working

```bash
./program -debug true   # ❌ Wrong! "true" is an argument
./program -debug=true   # ✅ Correct
./program -debug        # ✅ Also correct (implies true)
```

### Problem: Flag Defined But Not Recognized

**Check parse order:**
```go
name := flag.String("name", "", "name")

// ❌ Wrong order
fmt.Println(*name)  // Using before Parse!
flag.Parse()

// ✅ Correct order
flag.Parse()
fmt.Println(*name)  // Using after Parse
```

### Problem: Want to Parse Flags Multiple Times

**You can't!** `Parse()` should only be called once.

```go
// ❌ Wrong
flag.Parse()
// ... later ...
flag.Parse()  // Doesn't re-parse, already parsed!

// ✅ Use FlagSets for different contexts
fs1 := flag.NewFlagSet("cmd1", flag.ExitOnError)
fs2 := flag.NewFlagSet("cmd2", flag.ExitOnError)
```

---

## References

### Official Documentation
- **Go pkg.go.dev**: https://pkg.go.dev/flag
- **Source Code**: https://cs.opensource.google/go/go/+/go1.25.5:src/flag/flag.go
- **Go by Example - Flags**: https://gobyexample.com/command-line-flags
- **Effective Go**: https://go.dev/doc/effective_go

### Additional Resources
- **Go Blog - Command Line Flags**: https://go.dev/blog/
- **Standard Library Tour**: https://pkg.go.dev/std
- **Go Community Forums**: https://groups.google.com/g/golang-nuts

### Alternative Libraries (When flag Isn't Enough)
- **cobra**: https://github.com/spf13/cobra - Complex CLIs with nested subcommands
- **cli**: https://github.com/urfave/cli - Simpler than cobra, more than flag
- **pflag**: https://github.com/spf13/pflag - POSIX/GNU-style flags

---

## Summary

### When to Use Global Flags
- Simple programs with one set of options
- No subcommands needed
- Quick scripts and utilities

### When to Use FlagSets
- Programs with subcommands (like git, docker)
- Different flags per command
- Need isolated flag namespaces

### Key Takeaways
1. **Always call Parse()** before accessing flags
2. **Flags return pointers** - dereference with `*`
3. **Validate values yourself** - flag only checks types
4. **Flags before arguments** - order matters
5. **Use FlagSets** for subcommands
6. **Print errors to stderr** - use `fmt.Fprintf(os.Stderr, ...)`
7. **Provide good defaults** - make flags optional when possible
8. **Write helpful usage text** - users will thank you

---
