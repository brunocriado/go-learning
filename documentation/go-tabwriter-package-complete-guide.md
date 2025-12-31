# The Complete Guide to Go's `text/tabwriter` Package

**Last Updated:** December 25, 2025  
**Go Version:** 1.19+ (Compatible with 1.25.5)  
**Official Documentation:** https://pkg.go.dev/text/tabwriter  
**Algorithm:** Elastic Tabstops - http://nickgravgaard.com/elastictabstops/index.html

---

## Table of Contents

1. [Introduction](#introduction)
2. [Core Concepts](#core-concepts)
3. [Basic Usage](#basic-usage)
4. [Creating a Writer](#creating-a-writer)
5. [Parameters Explained](#parameters-explained)
6. [Formatting Flags](#formatting-flags)
7. [Writing and Flushing](#writing-and-flushing)
8. [Cell Delimiters](#cell-delimiters)
9. [Alignment and Padding](#alignment-and-padding)
10. [Advanced Features](#advanced-features)
11. [Common Patterns](#common-patterns)
12. [Real-World Examples](#real-world-examples)
13. [Best Practices](#best-practices)
14. [Troubleshooting](#troubleshooting)
15. [Performance Considerations](#performance-considerations)

---

## Introduction

The `text/tabwriter` package provides automatic column alignment for tabular text output. It's a **write filter** that transforms tab-separated input into beautifully aligned columns.

**What tabwriter does:**
- Aligns text into columns automatically
- Handles variable-width content
- Supports multiple alignment and padding options
- Works with any `io.Writer` (stdout, files, buffers)
- Uses the Elastic Tabstops algorithm for intelligent spacing

**What tabwriter does NOT do:**
- Parse CSV or structured data formats
- Add borders or grid lines (though you can add `|` separators)
- Format numbers (use `fmt` for that first)
- Handle ANSI color codes (they'll break alignment)

**When to use tabwriter:**
- Displaying tables in CLI applications
- Formatting lists with multiple columns
- Creating aligned reports
- Pretty-printing structured data to terminal

---

## Core Concepts

### The Writer Filter

```
Input (tabs separate columns):
Name\tAge\tCity
Alice\t30\tNew York
Bob\t25\tLA

↓ (tabwriter processes)

Output (aligned columns):
Name   Age  City
Alice  30   New York
Bob    25   LA
```

### Key Components

1. **Writer**: The main type that does the formatting
2. **Cells**: Text segments separated by tabs (`\t`)
3. **Columns**: Vertical alignment of cells with same position
4. **Lines**: Rows of data terminated by newline (`\n`)
5. **Padding**: Spaces added to make columns align

### How It Works

```go
// 1. Create a Writer
w := tabwriter.NewWriter(os.Stdout, ...)

// 2. Write tab-separated data
fmt.Fprintln(w, "Name\tAge\tCity")
fmt.Fprintln(w, "Alice\t30\tNew York")

// 3. Flush to output aligned text
w.Flush()
```

The Writer **buffers** input until `Flush()` is called, then calculates optimal column widths and outputs aligned text.

---

## Basic Usage

### Minimal Example

```go
package main

import (
    "fmt"
    "os"
    "text/tabwriter"
)

func main() {
    // Create a tabwriter
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
    
    // Write tab-separated content
    fmt.Fprintln(w, "Name\tAge\tCity")
    fmt.Fprintln(w, "Alice\t30\tNew York")
    fmt.Fprintln(w, "Bob\t25\tLos Angeles")
    fmt.Fprintln(w, "Charlie\t35\tChicago")
    
    // Flush to display
    w.Flush()
}
```

**Output:**
```
Name     Age  City
Alice    30   New York
Bob      25   Los Angeles
Charlie  35   Chicago
```

### With Headers

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

// Header
fmt.Fprintln(w, "ID\tProduct\tPrice\tStock")
fmt.Fprintln(w, "---\t-------\t-----\t-----")

// Data
fmt.Fprintln(w, "1\tApple\t$1.20\t150")
fmt.Fprintln(w, "2\tBanana\t$0.50\t200")
fmt.Fprintln(w, "3\tOrange\t$1.50\t80")

w.Flush()
```

**Output:**
```
ID  Product  Price  Stock
---  -------  -----  -----
1    Apple    $1.20  150
2    Banana   $0.50  200
3    Orange   $1.50  80
```

---

## Creating a Writer

### Method 1: NewWriter (Recommended)

```go
func NewWriter(output io.Writer, minwidth, tabwidth, padding int, 
               padchar byte, flags uint) *Writer
```

**Example:**
```go
w := tabwriter.NewWriter(
    os.Stdout,  // output destination
    0,          // minwidth
    8,          // tabwidth
    1,          // padding
    ' ',        // padchar
    0,          // flags
)
```

### Method 2: Init (Reuse Existing Writer)

```go
var w tabwriter.Writer
w.Init(os.Stdout, 0, 8, 1, ' ', 0)
```

**Use Init when:**
- You want to reuse a Writer with different settings
- You're allocating Writer on the stack
- You need to reset a Writer

**Use NewWriter when:**
- Creating a new Writer (most common case)
- You want a pointer right away

---

## Parameters Explained

### Parameter Breakdown

```go
w := tabwriter.NewWriter(output, minwidth, tabwidth, padding, padchar, flags)
```

| Parameter | Type | Description | Common Values |
|-----------|------|-------------|---------------|
| `output` | `io.Writer` | Where aligned text goes | `os.Stdout`, `&bytes.Buffer{}` |
| `minwidth` | `int` | Minimum cell width | `0` (auto), `8`, `10` |
| `tabwidth` | `int` | Tab character width | `8` (standard), `4`, `0` |
| `padding` | `int` | Extra spaces between columns | `1`, `2`, `3` |
| `padchar` | `byte` | Character for padding | `' '` (space), `'.'`, `'\t'` |
| `flags` | `uint` | Formatting options | `0`, `tabwriter.AlignRight` |

---

### 1. output (io.Writer)

Where the aligned text is written.

```go
// Write to stdout
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

// Write to a file
file, _ := os.Create("output.txt")
defer file.Close()
w := tabwriter.NewWriter(file, 0, 0, 2, ' ', 0)

// Write to a buffer
var buf bytes.Buffer
w := tabwriter.NewWriter(&buf, 0, 0, 2, ' ', 0)
fmt.Fprintln(w, "Name\tAge")
w.Flush()
fmt.Println(buf.String())

// Write to stderr
w := tabwriter.NewWriter(os.Stderr, 0, 0, 2, ' ', 0)
```

---

### 2. minwidth (int)

Minimum width for each column (excluding padding).

```go
// minwidth = 0 (auto-size based on content)
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
fmt.Fprintln(w, "A\tBB\tCCC")
w.Flush()
// Output: A  BB  CCC

// minwidth = 10 (all columns at least 10 chars)
w := tabwriter.NewWriter(os.Stdout, 10, 0, 2, ' ', 0)
fmt.Fprintln(w, "A\tBB\tCCC")
w.Flush()
// Output: A           BB          CCC
```

**When to use:**
- `0` - Most common, auto-sizes to content
- `>0` - When you want uniform column widths

---

### 3. tabwidth (int)

Width of tab characters in the output (if `padchar` is `\t`).

```go
// tabwidth = 8 (standard terminal tab width)
w := tabwriter.NewWriter(os.Stdout, 0, 8, 1, '\t', 0)

// tabwidth = 4 (smaller tabs)
w := tabwriter.NewWriter(os.Stdout, 0, 4, 1, '\t', 0)

// tabwidth = 0 (when using spaces, this is ignored)
w := tabwriter.NewWriter(os.Stdout, 0, 0, 1, ' ', 0)
```

**Important:** This only matters when `padchar = '\t'`. If using space padding, set to `0`.

---

### 4. padding (int)

Number of padding characters added **between** columns.

```go
// padding = 0 (no space between columns)
w := tabwriter.NewWriter(os.Stdout, 0, 0, 0, ' ', 0)
fmt.Fprintln(w, "Name\tAge")
fmt.Fprintln(w, "Alice\t30")
w.Flush()
// Output: NameAge
//         Alice30

// padding = 2 (2 spaces between columns)
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
fmt.Fprintln(w, "Name\tAge")
fmt.Fprintln(w, "Alice\t30")
w.Flush()
// Output: Name   Age
//         Alice  30

// padding = 4 (more spacing)
w := tabwriter.NewWriter(os.Stdout, 0, 0, 4, ' ', 0)
// Output: Name     Age
//         Alice    30
```

**Recommended:** `1` to `3` for most use cases.

---

### 5. padchar (byte)

Character used for padding between columns.

```go
// Space padding (most common)
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
// Output: Name   Age   City

// Dot padding (for visual guides)
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, '.', 0)
// Output: Name...Age...City

// Tab padding (use actual tabs)
w := tabwriter.NewWriter(os.Stdout, 0, 8, 1, '\t', 0)
// Output: Name\tAge\tCity (actual tabs in output)

// Underscore padding
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, '_', 0)
// Output: Name___Age___City
```

**Common Uses:**
- `' '` - Normal tables (99% of cases)
- `'.'` - Table of contents, price lists
- `'\t'` - When output will be processed by another program

---

### 6. flags (uint)

Formatting control flags (can be combined with `|`).

Available flags:
- `tabwriter.FilterHTML`
- `tabwriter.StripEscape`
- `tabwriter.AlignRight`
- `tabwriter.DiscardEmptyColumns`
- `tabwriter.TabIndent`
- `tabwriter.Debug`

See [Formatting Flags](#formatting-flags) section for details.

---

## Formatting Flags

### Available Flags

```go
const (
    FilterHTML          uint = 1 << iota  // Ignore HTML tags
    StripEscape                            // Remove escape sequences
    AlignRight                             // Right-align cells
    DiscardEmptyColumns                    // Remove empty columns
    TabIndent                              // Use tabs for indentation
    Debug                                  // Show column boundaries with |
)
```

### Using Flags

```go
// Single flag
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', tabwriter.AlignRight)

// Multiple flags
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 
    tabwriter.AlignRight | tabwriter.Debug)
```

---

### FilterHTML

Ignores HTML tags when calculating widths.

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', tabwriter.FilterHTML)

fmt.Fprintln(w, "Name\tStatus")
fmt.Fprintln(w, "<b>Alice</b>\t<span style='color:red'>Active</span>")
w.Flush()

// HTML tags don't affect column width calculation
// Output: <b>Alice</b>  <span style='color:red'>Active</span>
```

**Use when:**
- Outputting HTML with aligned columns
- Tags should be ignored for alignment

---

### StripEscape

Removes escape sequences from output.

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', tabwriter.StripEscape)

// \xff is the escape character
fmt.Fprintf(w, "Name\tCode\n")
fmt.Fprintf(w, "Tab\t\xff\t\xff\n")  // Escaped tab won't create column
w.Flush()

// Escape characters are stripped
```

**Use when:**
- You have escape sequences for special formatting
- You want to remove them from final output

---

### AlignRight

Right-aligns cell content instead of left-align.

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', tabwriter.AlignRight)

fmt.Fprintln(w, "Product\tPrice\tQty")
fmt.Fprintln(w, "Apple\t1.20\t10")
fmt.Fprintln(w, "Banana\t0.50\t25")
w.Flush()
```

**Output:**
```
Product  Price  Qty
  Apple   1.20   10
 Banana   0.50   25
```

**Use when:**
- Aligning numbers (prices, quantities)
- Right-to-left languages

---

### DiscardEmptyColumns

Removes columns that are entirely empty (vertical tabs only).

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', tabwriter.DiscardEmptyColumns)

fmt.Fprintln(w, "A\t\tC")    // Middle column is empty (vertical tab)
fmt.Fprintln(w, "1\t\t3")
w.Flush()

// Output: A  C
//         1  3
// (middle column discarded)
```

**Note:** Only works with **vertical tabs** (`\v`), not horizontal tabs (`\t`).

---

### TabIndent

Uses tabs for leading indentation, regardless of `padchar`.

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', tabwriter.TabIndent)

fmt.Fprintln(w, "\t\tName\tAge")  // Two leading tabs
fmt.Fprintln(w, "\t\tAlice\t30")
w.Flush()

// Leading tabs are preserved as tabs, columns use padchar
```

**Use when:**
- Need consistent indentation with tabs
- Outputting to files that will be edited with tabs

---

### Debug

Shows column boundaries with `|` characters.

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', tabwriter.Debug)

fmt.Fprintln(w, "Name\tAge\tCity")
fmt.Fprintln(w, "Alice\t30\tNYC")
w.Flush()
```

**Output:**
```
Name   | Age | City
Alice  | 30  | NYC
```

**Use when:**
- Debugging alignment issues
- Visualizing column boundaries
- Testing column layout

---

## Writing and Flushing

### The Write-Flush Pattern

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

// Write data (buffered internally)
fmt.Fprintln(w, "Header1\tHeader2")
fmt.Fprintln(w, "Data1\tData2")

// Flush to output
w.Flush()  // MUST call this!
```

**Critical:** Always call `Flush()` or output won't appear!

---

### Writing Methods

#### Using fmt.Fprintf

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

fmt.Fprintf(w, "Name\tAge\tCity\n")
fmt.Fprintf(w, "%s\t%d\t%s\n", "Alice", 30, "NYC")
fmt.Fprintf(w, "%s\t%d\t%s\n", "Bob", 25, "LA")

w.Flush()
```

#### Using fmt.Fprintln

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

fmt.Fprintln(w, "Name\tAge\tCity")  // Adds \n automatically
fmt.Fprintln(w, "Alice\t30\tNYC")

w.Flush()
```

#### Using w.Write() Directly

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

data := []byte("Name\tAge\n")
w.Write(data)

w.Flush()
```

---

### Flush Behavior

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

fmt.Fprintln(w, "Name\tAge")
fmt.Fprintln(w, "Alice\t30")

// Nothing appears yet (buffered)

w.Flush()  // NOW output appears

// Can continue writing after flush
fmt.Fprintln(w, "Bob\t25")
w.Flush()  // Flush again for new data
```

**What Flush does:**
1. Calculates column widths from buffered data
2. Adds padding to align columns
3. Writes aligned text to output
4. Clears internal buffer

---

### Defer Pattern (Recommended)

```go
func printTable(data [][]string) {
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
    defer w.Flush()  // Ensures Flush even if panic occurs
    
    for _, row := range data {
        fmt.Fprintln(w, strings.Join(row, "\t"))
    }
}
```

---

## Cell Delimiters

### Horizontal Tabs (\t)

Creates a new cell (column).

```go
fmt.Fprintln(w, "Col1\tCol2\tCol3")
                   ↑     ↑
                   tabs create cells
```

---

### Vertical Tabs (\v)

Creates a "soft" column break (can be discarded).

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', tabwriter.DiscardEmptyColumns)

fmt.Fprintln(w, "A\vB\vC")  // Vertical tabs
fmt.Fprintln(w, "1\v\v3")   // Middle column empty

w.Flush()
// Output: A  C
//         1  3
// (B column discarded because it's empty and using \v)
```

**Key Difference:**
- `\t` (horizontal tab) - "Hard" column, always present
- `\v` (vertical tab) - "Soft" column, can be discarded if empty

---

### Newlines (\n)

Terminates a line.

```go
fmt.Fprintln(w, "Line1\tData1")  // \n added by Fprintln
fmt.Fprintln(w, "Line2\tData2")
```

---

### Formfeed (\f)

Acts like newline BUT also terminates all columns (forces flush).

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

fmt.Fprintln(w, "Group1\tData1")
fmt.Fprintln(w, "Group1\tData2")
fmt.Fprintf(w, "\f")  // Formfeed

fmt.Fprintln(w, "Group2\tData3")  // Starts new column alignment

w.Flush()
```

**Use when:**
- You want to output aligned sections separately
- Need to "reset" column alignment mid-output

---

## Alignment and Padding

### Column Width Calculation

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

fmt.Fprintln(w, "Short\tMediumLength\tX")
fmt.Fprintln(w, "A\tB\tLongerValue")
w.Flush()
```

**Output:**
```
Short  MediumLength  X
A      B             LongerValue
```

**How widths are calculated:**
1. Find widest cell in each column
2. Set column width to widest cell
3. Add padding between columns

**Column 1:** `max("Short", "A")` = 5 chars + 2 padding = 7  
**Column 2:** `max("MediumLength", "B")` = 12 chars + 2 padding = 14  
**Column 3:** `max("X", "LongerValue")` = 11 chars (last column, no padding)

---

### Left Alignment (Default)

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

fmt.Fprintln(w, "Name\tScore")
fmt.Fprintln(w, "Alice\t95")
fmt.Fprintln(w, "Bob\t100")
w.Flush()
```

**Output:**
```
Name   Score
Alice  95
Bob    100
```

---

### Right Alignment

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', tabwriter.AlignRight)

fmt.Fprintln(w, "Name\tScore")
fmt.Fprintln(w, "Alice\t95")
fmt.Fprintln(w, "Bob\t100")
w.Flush()
```

**Output:**
```
 Name  Score
Alice     95
  Bob    100
```

---

### Custom Padding

```go
// Tight spacing (padding = 1)
w := tabwriter.NewWriter(os.Stdout, 0, 0, 1, ' ', 0)
fmt.Fprintln(w, "A\tB\tC")
w.Flush()
// Output: A B C

// Generous spacing (padding = 4)
w := tabwriter.NewWriter(os.Stdout, 0, 0, 4, ' ', 0)
fmt.Fprintln(w, "A\tB\tC")
w.Flush()
// Output: A    B    C
```

---

## Advanced Features

### Escape Sequences

Bracket text with `\xff` to exclude it from width calculations.

```go
const Escape = '\xff'

w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

fmt.Fprintf(w, "Name\tCode\n")
fmt.Fprintf(w, "Tab\t%cActual\tTab%c\n", Escape, Escape)
//                  ↑ escaped text ↑

w.Flush()
```

The `\t` between escape characters is **not** treated as a column delimiter.

**Use cases:**
- ANSI color codes (though they'll still appear in output)
- Embedded tabs that shouldn't create columns
- Special formatting that shouldn't affect alignment

---

### Mixing Content

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

// Header
fmt.Fprintln(w, "Product\tPrice\tQty")
fmt.Fprintln(w, "-------\t-----\t---")

// Data rows
fmt.Fprintln(w, "Apple\t$1.20\t10")
fmt.Fprintln(w, "Banana\t$0.50\t25")

// Separator
fmt.Fprintln(w, "-------\t-----\t---")

// Total row (different formatting)
fmt.Fprintln(w, "Total\t$17.00\t35")

w.Flush()
```

---

### Nested Tables (Not Recommended)

Tabwriter doesn't support nested tables well. For complex layouts, use multiple writers:

```go
// Outer table
outer := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

// Inner table to buffer
var buf bytes.Buffer
inner := tabwriter.NewWriter(&buf, 0, 0, 1, ' ', 0)
fmt.Fprintln(inner, "Sub1\tSub2")
inner.Flush()

// Include inner table in outer
fmt.Fprintf(outer, "Main\t%s\n", buf.String())
outer.Flush()
```

---

## Common Patterns

### Pattern 1: Simple Data Table

```go
func displayUsers(users []User) {
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 3, ' ', 0)
    defer w.Flush()
    
    fmt.Fprintln(w, "ID\tName\tEmail\tRole")
    fmt.Fprintln(w, "--\t----\t-----\t----")
    
    for _, u := range users {
        fmt.Fprintf(w, "%d\t%s\t%s\t%s\n", 
            u.ID, u.Name, u.Email, u.Role)
    }
}
```

---

### Pattern 2: Right-Aligned Numbers

```go
func displayPrices(items []Item) {
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
    defer w.Flush()
    
    fmt.Fprintln(w, "Item\tQty\tPrice\tTotal")
    
    for _, item := range items {
        total := float64(item.Qty) * item.Price
        // Right-align numbers with padding
        fmt.Fprintf(w, "%s\t%d\t%.2f\t%.2f\n",
            item.Name, item.Qty, item.Price, total)
    }
}
```

---

### Pattern 3: Columnar Lists

```go
func listFiles(files []FileInfo) {
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
    defer w.Flush()
    
    for _, f := range files {
        fmt.Fprintf(w, "%s\t%d bytes\t%s\n", 
            f.Name, f.Size, f.ModTime.Format("2006-01-02"))
    }
}
```

---

### Pattern 4: Status Reports

```go
func showStatus(services []Service) {
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 3, ' ', 0)
    defer w.Flush()
    
    fmt.Fprintln(w, "Service\tStatus\tUptime\tMemory")
    
    for _, s := range services {
        status := "✓ Running"
        if !s.IsRunning {
            status = "✗ Stopped"
        }
        
        fmt.Fprintf(w, "%s\t%s\t%s\t%dMB\n",
            s.Name, status, s.Uptime, s.MemoryMB)
    }
}
```

---

### Pattern 5: Dot Leaders (Table of Contents)

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 1, '.', 0)
defer w.Flush()

fmt.Fprintln(w, "Chapter 1\tIntroduction\t1")
fmt.Fprintln(w, "Chapter 2\tGetting Started\t15")
fmt.Fprintln(w, "Chapter 3\tAdvanced Topics\t42")
```

**Output:**
```
Chapter 1.Introduction.....1
Chapter 2.Getting Started.15
Chapter 3.Advanced Topics.42
```

---

### Pattern 6: Conditional Formatting

```go
func displayWithColors(items []Item) {
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
    defer w.Flush()
    
    for _, item := range items {
        status := "OK"
        if item.Stock < 10 {
            status = "LOW"
        }
        
        fmt.Fprintf(w, "%s\t%d\t%s\n", 
            item.Name, item.Stock, status)
    }
}
```

---

## Real-World Examples

### Example 1: Process List

```go
package main

import (
    "fmt"
    "os"
    "text/tabwriter"
)

type Process struct {
    PID    int
    Name   string
    CPU    float64
    Memory int
    User   string
}

func main() {
    processes := []Process{
        {1234, "chrome", 15.3, 512, "alice"},
        {5678, "code", 8.2, 1024, "alice"},
        {9012, "spotify", 2.1, 256, "alice"},
    }
    
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 3, ' ', 0)
    defer w.Flush()
    
    // Header
    fmt.Fprintln(w, "PID\tNAME\tCPU%\tMEM(MB)\tUSER")
    fmt.Fprintln(w, "---\t----\t----\t-------\t----")
    
    // Data
    for _, p := range processes {
        fmt.Fprintf(w, "%d\t%s\t%.1f%%\t%d\t%s\n",
            p.PID, p.Name, p.CPU, p.Memory, p.User)
    }
}
```

---

### Example 2: Git-Style Log

```go
func printCommits(commits []Commit) {
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
    defer w.Flush()
    
    for _, c := range commits {
        // Short hash, date, author, message
        fmt.Fprintf(w, "%s\t%s\t%s\t%s\n",
            c.Hash[:7],
            c.Date.Format("2006-01-02"),
            c.Author,
            c.Message)
    }
}
```

---

### Example 3: Database Query Results

```go
func displayQueryResults(rows *sql.Rows) error {
    columns, err := rows.Columns()
    if err != nil {
        return err
    }
    
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
    defer w.Flush()
    
    // Print header
    fmt.Fprintln(w, strings.Join(columns, "\t"))
    
    // Print separator
    seps := make([]string, len(columns))
    for i := range seps {
        seps[i] = "---"
    }
    fmt.Fprintln(w, strings.Join(seps, "\t"))
    
    // Print rows
    values := make([]interface{}, len(columns))
    valuePtrs := make([]interface{}, len(columns))
    for i := range values {
        valuePtrs[i] = &values[i]
    }
    
    for rows.Next() {
        rows.Scan(valuePtrs...)
        
        strVals := make([]string, len(values))
        for i, v := range values {
            strVals[i] = fmt.Sprintf("%v", v)
        }
        
        fmt.Fprintln(w, strings.Join(strVals, "\t"))
    }
    
    return rows.Err()
}
```

---

### Example 4: Configuration Display

```go
func showConfig(config map[string]string) {
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 4, ' ', 0)
    defer w.Flush()
    
    fmt.Fprintln(w, "Setting\tValue")
    fmt.Fprintln(w, "-------\t-----")
    
    // Sort keys for consistent output
    keys := make([]string, 0, len(config))
    for k := range config {
        keys = append(keys, k)
    }
    sort.Strings(keys)
    
    for _, k := range keys {
        fmt.Fprintf(w, "%s\t%s\n", k, config[k])
    }
}
```

---

## Best Practices

### 1. Always Flush

```go
// ✅ Good - defer ensures flush
func printTable() {
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
    defer w.Flush()
    
    fmt.Fprintln(w, "Data\tHere")
}

// ❌ Bad - forgot to flush
func printTable() {
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
    fmt.Fprintln(w, "Data\tHere")
    // Nothing appears!
}
```

---

### 2. Consistent Column Count

```go
// ✅ Good - same number of columns
fmt.Fprintln(w, "A\tB\tC")
fmt.Fprintln(w, "1\t2\t3")

// ❌ Bad - inconsistent columns
fmt.Fprintln(w, "A\tB\tC")
fmt.Fprintln(w, "1\t2")      // Only 2 columns!
```

---

### 3. Use Proper Delimiters

```go
// ✅ Good - use \t for tabs
fmt.Fprintf(w, "%s\t%d\t%s\n", name, age, city)

// ❌ Bad - using spaces
fmt.Fprintf(w, "%s %d %s\n", name, age, city)
// Won't align properly!
```

---

### 4. Format Before Writing

```go
// ✅ Good - format numbers first
fmt.Fprintf(w, "%.2f\t%d\n", price, quantity)

// ✅ Good - format dates first
fmt.Fprintf(w, "%s\t%s\n", name, date.Format("2006-01-02"))
```

---

### 5. Appropriate Padding

```go
// ✅ Good - reasonable padding (1-3)
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

// ❌ Bad - excessive padding
w := tabwriter.NewWriter(os.Stdout, 0, 0, 20, ' ', 0)
// Wastes space, hard to read
```

---

### 6. Consider Terminal Width

```go
// For wide tables, check terminal width
import "golang.org/x/term"

func printWideTable() {
    width, _, _ := term.GetSize(int(os.Stdout.Fd()))
    
    if width < 120 {
        // Use abbreviated column names or fewer columns
    }
    
    w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
    defer w.Flush()
    // ... print table
}
```

---

### 7. Use Debug for Development

```go
// During development, use Debug flag
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', tabwriter.Debug)

// Shows column boundaries:
// Name   | Age | City
// Alice  | 30  | NYC

// Remove for production
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
```

---

## Troubleshooting

### Problem: Nothing Appears

```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
fmt.Fprintln(w, "Data\tHere")
// Nothing printed!
```

**Solution:** Call `Flush()`
```go
w.Flush()
```

---

### Problem: Columns Not Aligning

**Cause 1:** Using spaces instead of tabs
```go
// ❌ Wrong
fmt.Fprintln(w, "Name Age City")
```

**Solution:** Use `\t`
```go
// ✅ Correct
fmt.Fprintln(w, "Name\tAge\tCity")
```

**Cause 2:** Inconsistent column counts
```go
// ❌ Wrong
fmt.Fprintln(w, "A\tB\tC")
fmt.Fprintln(w, "1\t2")     // Missing column!
```

**Solution:** Same number of tabs per row

---

### Problem: Text is Cut Off

**Cause:** Using fixed `minwidth` too small for content

```go
// ❌ Problem
w := tabwriter.NewWriter(os.Stdout, 5, 0, 2, ' ', 0)
fmt.Fprintln(w, "VeryLongColumnName\tData")
```

**Solution:** Use `minwidth = 0` for auto-sizing
```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
```

---

### Problem: Extra Blank Columns

**Cause:** Trailing tabs or extra `\t`

```go
// ❌ Trailing tab creates empty column
fmt.Fprintln(w, "Name\tAge\t")
```

**Solution:** Remove trailing tabs
```go
fmt.Fprintln(w, "Name\tAge")
```

---

### Problem: ANSI Colors Break Alignment

ANSI color codes have width but are invisible:

```go
// ❌ Colors mess up width calculation
fmt.Fprintf(w, "\033[31mRed\033[0m\tData\n")
```

**Solution:** Use escape sequences or strip colors
```go
// Remove colors before printing
// OR use escape sequences (advanced)
```

---

## Performance Considerations

### Memory Usage

Tabwriter **buffers all input** until `Flush()` is called.

```go
// ⚠️ For huge tables, this uses lots of memory
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
for i := 0; i < 1000000; i++ {
    fmt.Fprintf(w, "%d\tData\n", i)
}
w.Flush()  // All million rows buffered!
```

**Solutions for large datasets:**

1. **Flush periodically:**
```go
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
for i, row := range hugeDataset {
    fmt.Fprintln(w, formatRow(row))
    
    if i%1000 == 0 {
        w.Flush()  // Flush every 1000 rows
    }
}
w.Flush()  // Final flush
```

2. **Pre-calculate widths and use printf directly:**
```go
// Calculate max widths first
maxWidths := calculateWidths(data)

// Print with fixed widths
for _, row := range data {
    fmt.Printf("%-*s  %-*s\n", 
        maxWidths[0], row[0],
        maxWidths[1], row[1])
}
```

---

### When NOT to Use Tabwriter

**Don't use for:**
- Real-time streaming output (buffers everything)
- Single-row output (overhead not worth it)
- Pre-formatted data (already aligned)
- HTML/XML output (use templating instead)

**Use alternatives:**
- Single row: `fmt.Printf("%-20s %10d\n", ...)`
- Streaming: Calculate widths first, then print
- HTML: `html/template`

---

## References

### Official Documentation
- **Go pkg.go.dev**: https://pkg.go.dev/text/tabwriter
- **Source Code**: https://cs.opensource.google/go/go/+/go1.25.5:src/text/tabwriter/tabwriter.go
- **Elastic Tabstops Algorithm**: http://nickgravgaard.com/elastictabstops/index.html

### Additional Resources
- **Go by Example - Text Formatting**: https://gobyexample.com/
- **Standard Library Tour**: https://pkg.go.dev/std
- **io.Writer Interface**: https://pkg.go.dev/io#Writer

### Related Packages
- **text/template**: For more complex formatting
- **fmt**: For basic formatting and printing
- **golang.org/x/term**: Terminal size detection

---

## Summary

### Quick Reference

```go
// Basic usage
w := tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)
defer w.Flush()

fmt.Fprintln(w, "Col1\tCol2\tCol3")
fmt.Fprintln(w, "Data1\tData2\tData3")
```

### Common Configurations

```go
// Standard table
tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', 0)

// Right-aligned numbers
tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', tabwriter.AlignRight)

// Dot leaders
tabwriter.NewWriter(os.Stdout, 0, 0, 1, '.', 0)

// Debug mode
tabwriter.NewWriter(os.Stdout, 0, 0, 2, ' ', tabwriter.Debug)
```

### Key Takeaways

1. **Always flush** - Use `defer w.Flush()`
2. **Use tabs** - `\t` for column delimiters, not spaces
3. **Consistent columns** - Same number per row
4. **Buffering** - Data is buffered until Flush
5. **Simple is best** - Start with: `NewWriter(os.Stdout, 0, 0, 2, ' ', 0)`
6. **Format first** - Format data before writing to tabwriter
7. **Watch memory** - Flush periodically for huge datasets

---

**Document Version:** 1.0  
**Last Updated:** December 25, 2025  
**Maintained By:** Bruno's Go Learning Repository
