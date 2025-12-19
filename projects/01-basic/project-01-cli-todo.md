# Project 1: CLI Todo Application

**Level**: Basic | **Estimated Time**: 8-12 hours | **Prerequisites**: None (Start here!)

Build a command-line todo list manager that persists tasks to a JSON file. This project teaches fundamental Go concepts through a practical tool you can actually use daily.

---

## 📚 What You'll Learn

- **Structs & Methods**: Define custom data types and attach behavior
- **File I/O**: Read from and write to files using `os` and `io/ioutil`
- **JSON Encoding/Decoding**: Marshal and unmarshal data structures
- **Flag Parsing**: Handle command-line arguments with `flag` package
- **Error Handling**: Go's explicit error handling pattern
- **Slices**: Dynamic arrays and slice operations
- **Time Package**: Work with dates and timestamps

---

## 🎯 Core Features

1. Add new tasks with description and priority
2. List all tasks (pending/completed)
3. Mark tasks as complete
4. Delete tasks
5. Filter by status or priority
6. Persistent storage in JSON file

---

## 📋 Prerequisites & Requirements

### Before Starting

**System Requirements:**
- **OS**: macOS, Linux, or Windows
- **Disk Space**: ~50MB for Go installation + project
- **RAM**: 2GB minimum (4GB recommended)
- **Terminal**: Bash, Zsh, PowerShell, or Command Prompt

**Knowledge Prerequisites:**
- **Must Know**:
  - How to declare variables and constants
  - Basic types: int, string, bool
  - How to write and call functions
  - Basic package imports
- **Should Know** (will learn if not):
  - Structs (will be thoroughly explained)
  - Slices vs arrays
  - Error handling with `if err != nil`
  - JSON concepts (objects, arrays)
- **Nice to Have**:
  - Used command-line flags before (like `ls -la`)
  - Read JSON format
  - Basic file operations concepts

**External Dependencies:**
- **None!** Uses only Go standard library
- All packages included: `encoding/json`, `flag`, `os`, `time`, `fmt`

**Estimated Time Breakdown:**
- Setup: 15-30 minutes
- Implementation: 3-6 hours (first time)
- Testing & debugging: 1-2 hours
- **Total**: 5-9 hours

---

## 🛠️ Setup

### Install Go

```bash
# macOS (using Homebrew)
brew install go

# Linux (Ubuntu/Debian)
sudo apt update
sudo apt install golang-go

# Windows
# Download installer from golang.org

# Verify installation
go version  # Should show version 1.19+

# Check Go environment
go env GOPATH  # Your Go workspace path
go env GOROOT  # Where Go is installed
```

### Initialize Project

```bash
# Create project directory
mkdir -p ~/projects/todo-cli
cd ~/projects/todo-cli

# Initialize Go module
go mod init github.com/yourusername/todo-cli

# This creates go.mod file (like package.json for Node.js)
```

---

## 📁 Project Structure

```
todo-cli/
├── main.go           # Entry point and CLI handling
├── todo.go           # Todo struct and methods
├── storage.go        # File operations
├── go.mod            # Module definition
└── todos.json        # Data file (created at runtime)
```

**Files You'll Create:**
- `main.go` - 100-150 lines
- `todo.go` - 80-120 lines  
- `storage.go` - 40-60 lines
- `go.mod` - Auto-generated
- `todos.json` - Created at runtime

---

## 💻 Implementation Guide

### Step 1: Define the Todo Structure (`todo.go`)

**Key Concepts:**
- **Structs**: User-defined types that group related data
- **Tags**: Metadata for struct fields (used for JSON serialization)
- **Methods**: Functions associated with a type

**What you need to create:**
- A `Todo` struct with fields: ID, Title, Description, Completed, Priority, CreatedAt, CompletedAt
  - Use JSON tags for each field
  - CompletedAt should be a pointer to allow null values
- A `TodoList` struct that holds a slice of todos
- Methods on `TodoList`:
  - `Add(title, description, priority)` - Create and add a new todo
  - `Complete(id)` - Mark a todo as done (set Completed=true and CompletedAt)
  - `Delete(id)` - Remove a todo from the slice
  - `GetByID(id)` - Find and return a specific todo
  - `Filter(completed)` - Return only pending or completed todos

**Learning Notes:**
- **Pointer Receivers (`*TodoList`)**: Use when method needs to modify the struct or when struct is large
- **Value Receivers (`TodoList`)**: Use when method only reads data and struct is small
- **Error Handling**: Go returns errors explicitly, no exceptions
- **nil**: Go's zero value for pointers, meaning "no value"
- **Slice Manipulation**: Use `append()` to add, slice tricks like `append(slice[:i], slice[i+1:]...)` to remove

**Hints:**
- To generate unique IDs, loop through existing todos and find max ID + 1
- Use `time.Now()` to get current timestamp
- For Delete, you'll need to reconstruct the slice without the deleted item
- Methods that modify data should use pointer receivers: `func (tl *TodoList) Add(...)`

---

### Step 2: Implement Storage (`storage.go`)

**Key Concepts:**
- **JSON Marshaling**: Convert Go objects to JSON
- **File Operations**: Read/write files safely
- **Error Propagation**: Handling and passing errors up the call stack

**What you need to create:**
- A constant for the data file name (e.g., "todos.json")
- `SaveToFile()` method on `TodoList`:
  - Marshal the TodoList to JSON with indentation
  - Write to file with appropriate permissions (0644)
  - Return errors if anything fails
- `LoadFromFile()` function that returns `(*TodoList, error)`:
  - Check if file exists (use `os.Stat`)
  - If doesn't exist, return empty TodoList
  - Read file contents
  - Unmarshal JSON into TodoList struct
  - Handle all errors appropriately

**Learning Notes:**
- **`json.MarshalIndent()`**: Makes JSON human-readable
- **`os.WriteFile()`**: One-step file writing
- **`os.ReadFile()`**: One-step file reading
- **`%w` Format Verb**: Wraps errors, preserving the error chain
- **File Permissions**: 0644 = owner can read/write, others can only read

**Hints:**
- Use `os.IsNotExist(err)` to check if file doesn't exist
- Wrap errors with context: `fmt.Errorf("error reading file: %w", err)`
- Initialize empty slice: `&TodoList{Todos: []Todo{}}`

---

### Step 3: Build the CLI (`main.go`)

**Key Concepts:**
- **Flag Package**: Parse command-line arguments
- **Switch Statements**: Multi-way conditional logic
- **Defer**: Ensure code runs at function exit (cleanup)

**What you need to create:**
- Use `flag.NewFlagSet()` to create separate flag sets for each command:
  - **add**: flags for -title, -desc, -priority
  - **list**: flags for -all, -pending, -completed
  - **complete**: takes ID as argument
  - **delete**: takes ID as argument
- Main function flow:
  1. Check if subcommand provided
  2. Load existing todos from file
  3. Switch on subcommand (add/list/complete/delete)
  4. For each command: parse flags, execute operation, save if modified
- Helper functions:
  - `displayTodos()` - Format and print todos in a table
  - `printUsage()` - Show help information

**Learning Notes:**
- **`flag.NewFlagSet`**: Creates independent flag sets for subcommands
- **`defer`**: Schedules function call to run when surrounding function returns
- **`text/tabwriter`**: Standard library package for aligned text output
- **`strconv.Atoi`**: Convert string to integer

**Hints:**
- Use `tabwriter.NewWriter()` for nice table formatting
- Check `os.Args[1]` for the subcommand name
- Parse flags with `flagSet.Parse(os.Args[2:])`
- Get positional arguments with `flagSet.Arg(0)`
- Always save after modifying todos

---

### Step 4: Build and Run

```bash
# Build the application
go build -o todo-cli

# Run examples
./todo-cli add -title "Learn Go" -desc "Complete basic projects" -priority 3
./todo-cli add -title "Buy groceries" -priority 2
./todo-cli list
./todo-cli complete 1
./todo-cli list --pending
./todo-cli delete 2
```

---

## 🚀 Challenge Yourself

Once you've built the basic version, try adding:

1. **Edit Command**: Modify existing todos
2. **Search**: Find todos by keyword
3. **Due Dates**: Add deadlines and sort by urgency
4. **Tags/Categories**: Organize todos with labels
5. **Color Output**: Use ANSI colors for priority levels (github.com/fatih/color)
6. **Export**: Generate HTML or markdown reports
7. **Undo**: Keep operation history and reverse last N operations

---

## ⚠️ Common Gotchas to Watch For

**Problem**: Changes don't persist  
**Why**: Forgot to call `SaveToFile()` after modifications  
**Fix**: Always save after add/complete/delete operations

**Problem**: "slice bounds out of range"  
**Why**: Accessing slice index without checking length  
**Fix**: Check `len(slice) > 0` before accessing, or use range loops

**Problem**: JSON file gets corrupted  
**Why**: Crash or error during write  
**Fix**: Write to temporary file first, then rename (atomic operation):
```go
tmpFile := dataFile + ".tmp"
os.WriteFile(tmpFile, data, 0644)
os.Rename(tmpFile, dataFile)
```

**Problem**: Can't find todo by ID  
**Why**: ID generation creates duplicates or IDs don't match  
**Fix**: Use consistent ID generation (max ID + 1)

---

## 📚 Key Takeaways

After completing this project, you should understand:

- ✅ How to structure a Go CLI application
- ✅ Working with structs and methods
- ✅ JSON encoding and decoding
- ✅ File I/O operations
- ✅ Command-line flag parsing
- ✅ Error handling patterns
- ✅ Slice operations and manipulation

---

## 🔗 Related Resources

- [Go by Example: Structs](https://gobyexample.com/structs)
- [Go by Example: JSON](https://gobyexample.com/json)
- [Go Flag Package](https://pkg.go.dev/flag)
- [Effective Go](https://go.dev/doc/effective_go)

---

## 📍 Navigation

- [← Back to Basic Projects](README.md)
- [→ Next: Project 2 - Weather CLI](project-02-weather-cli.md)
- [↑ Projects Index](../../projects-index.md)
- [↑ Getting Started](../../getting-started.md)

---

**Ready to build?** Create your project directory and start coding! Remember: it's okay to look things up, struggle is part of learning. Good luck! 🚀
