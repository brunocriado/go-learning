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

## 📋 Task Checklist

Use this checklist to guide your implementation. Check off tasks as you complete them. **Remember**: These are guidance tasks, not solutions. You'll need to research and figure out the implementation details yourself.

### Phase 1: Project Setup & Foundation
- [x] **Task 1.1**: Install Go and verify installation works (run `go version`)
- [x] **Task 1.2**: Create project directory and navigate into it
- [x] **Task 1.3**: Initialize Go module with `go mod init`
- [x] **Task 1.4**: Create three empty files: `main.go`, `todo.go`, `storage.go`
- [x] **Task 1.5**: Add package declarations to each file (`package main`)
- [x] **Task 1.6**: Research and understand what a Go struct is
- [x] **Task 1.7**: Research JSON struct tags and how they work

### Phase 2: Data Structures (`todo.go`)
- [x] **Task 2.1**: Define the `Todo` struct with all required fields (ID, Title, Description, etc.)
- [x] **Task 2.2**: Add JSON tags to each field in the `Todo` struct
- [x] **Task 2.3**: Make `CompletedAt` a pointer type (research why pointers allow null values)
- [x] **Task 2.4**: Define the `TodoList` struct containing a slice of `Todo`
- [x] **Task 2.5**: Research the difference between pointer receivers and value receivers
- [x] **Task 2.6**: Implement the `Add()` method - figure out how to generate unique IDs
- [x] **Task 2.7**: Test ID generation logic - what happens when adding multiple todos?
- [x] **Task 2.8**: Implement the `Complete()` method - how to find a todo by ID?
- [x] **Task 2.9**: Handle the case when a todo ID doesn't exist in `Complete()`
- [x] **Task 2.10**: Implement the `Delete()` method - research slice manipulation techniques
- [x] **Task 2.11**: Figure out how to remove an element from a slice without leaving gaps
- [x] **Task 2.12**: Implement `GetByID()` - consider what to return if ID not found
- [x] **Task 2.13**: Implement `Filter()` - research how to iterate over slices
- [x] **Task 2.14**: Test each method individually with dummy data

### Phase 3: Persistence (`storage.go`)
- [x] **Task 3.1**: Research the `encoding/json` package and how marshaling works
- [x] **Task 3.2**: Define a constant for the JSON filename (where will todos be stored?)
- [x] **Task 3.3**: Implement `SaveToFile()` - what does JSON marshaling return?
- [x] **Task 3.4**: Figure out the correct file permissions for `os.WriteFile()` (hint: 0644)
- [x] **Task 3.5**: Research `json.MarshalIndent()` vs `json.Marshal()` - which is better for debugging?
- [x] **Task 3.6**: Add error handling to `SaveToFile()` - what can go wrong during file writes?
- [x] **Task 3.7**: Implement `LoadFromFile()` - how do you check if a file exists?
- [x] **Task 3.8**: Handle the case when the JSON file doesn't exist yet (first run)
- [x] **Task 3.9**: Research `os.Stat()` and `os.IsNotExist()` for file checking
- [x] **Task 3.10**: Implement JSON unmarshaling - what type should you unmarshal into?
- [x] **Task 3.11**: Return an empty TodoList when file doesn't exist (not an error)
- [x] **Task 3.12**: Add error wrapping with context (research `fmt.Errorf` with `%w`)
- [x] **Task 3.13**: Test saving and loading with sample data manually

### Phase 4: Command-Line Interface (`main.go`)
- [x] **Task 4.1**: Research the `flag` package - how does it parse command-line arguments?
- [ ] **Task 4.2**: Research `flag.NewFlagSet()` - why use flag sets instead of global flags?
- [ ] **Task 4.3**: Design the command structure (what subcommands do you need?)
- [ ] **Task 4.4**: Implement argument validation - what if user provides no subcommand?
- [ ] **Task 4.5**: Create flag set for the `add` command with -title, -desc, -priority flags
- [ ] **Task 4.6**: Figure out how to parse flags from `os.Args[2:]` (why start at index 2?)
- [ ] **Task 4.7**: Create flag set for the `list` command with filtering options
- [ ] **Task 4.8**: Implement the `complete` command - how to get the ID from arguments?
- [ ] **Task 4.9**: Implement the `delete` command - similar to complete
- [ ] **Task 4.10**: Research `strconv.Atoi()` for converting string IDs to integers
- [ ] **Task 4.11**: Load existing todos at the start of main() - handle errors appropriately
- [ ] **Task 4.12**: Implement switch statement for routing subcommands
- [ ] **Task 4.13**: After each modifying operation (add/complete/delete), save the todos
- [ ] **Task 4.14**: Create `printUsage()` function - when should it be called?
- [ ] **Task 4.15**: Research `text/tabwriter` for formatted table output
- [ ] **Task 4.16**: Implement `displayTodos()` to show todos in a readable table format
- [ ] **Task 4.17**: Format dates nicely (research `time.Format()` with layouts)
- [ ] **Task 4.18**: Handle empty todo list case in display function

### Phase 5: Testing & Debugging
- [ ] **Task 5.1**: Build the project with `go build` - fix any compilation errors
- [ ] **Task 5.2**: Test adding a single todo - does it create the JSON file?
- [ ] **Task 5.3**: Examine the created JSON file - is it properly formatted?
- [ ] **Task 5.4**: Test listing todos - does the table display correctly?
- [ ] **Task 5.5**: Test adding multiple todos - are IDs unique and incrementing?
- [ ] **Task 5.6**: Test completing a todo - does it update the Completed field and timestamp?
- [ ] **Task 5.7**: Test listing only pending todos - is filtering working?
- [ ] **Task 5.8**: Test listing only completed todos
- [ ] **Task 5.9**: Test deleting a todo - is it removed from the list?
- [ ] **Task 5.10**: Test edge cases: deleting non-existent ID, completing already completed todo
- [ ] **Task 5.11**: Test error handling: invalid priority, missing required flags
- [ ] **Task 5.12**: Test persistence: restart the app, are todos still there?
- [ ] **Task 5.13**: Deliberately corrupt the JSON file - does error handling work?
- [ ] **Task 5.14**: Test with no subcommand - does usage help appear?

### Phase 6: Refinement
- [ ] **Task 6.1**: Add helpful error messages for common mistakes
- [ ] **Task 6.2**: Improve table formatting - align columns nicely
- [ ] **Task 6.3**: Add color or symbols to distinguish pending vs completed todos
- [ ] **Task 6.4**: Validate priority values (e.g., 1-5 range)
- [ ] **Task 6.5**: Validate that title is not empty before adding
- [ ] **Task 6.6**: Add confirmation messages after successful operations
- [ ] **Task 6.7**: Consider adding a `clear` or `reset` command
- [ ] **Task 6.8**: Write comments explaining complex logic
- [ ] **Task 6.9**: Run `go fmt` to format your code properly
- [ ] **Task 6.10**: Review code for potential improvements

### Bonus Challenges (Optional)
- [ ] **Bonus 1**: Add an `edit` command to modify existing todos
- [ ] **Bonus 2**: Implement search functionality by keyword
- [ ] **Bonus 3**: Add due dates and sort by urgency
- [ ] **Bonus 4**: Add tags/categories to todos
- [ ] **Bonus 5**: Use ANSI colors for priority levels (research color libraries)
- [ ] **Bonus 6**: Export todos to HTML or Markdown format
- [ ] **Bonus 7**: Implement undo functionality for last operation
- [ ] **Bonus 8**: Add priority sorting when listing todos
- [ ] **Bonus 9**: Implement atomic file writes (write to temp file, then rename)
- [ ] **Bonus 10**: Add unit tests for core functions

---

## 🤔 Debugging Questions to Ask Yourself

As you work through the tasks, ask yourself these questions:

**Data Structures:**
- Why use a struct instead of just a map?
- What's the difference between `TodoList` and `*TodoList`?
- Why is `CompletedAt` a pointer but `CreatedAt` is not?
- How does appending to a slice work under the hood?

**File Operations:**
- What happens if two processes try to write the file simultaneously?
- How can you prevent data loss if the program crashes during save?
- Why use `MarshalIndent` instead of `Marshal`?
- What file permissions should a data file have and why?

**Command-Line Parsing:**
- Why create separate flag sets for each command?
- What's the difference between `flag.String()` and `flag.StringVar()`?
- How does `flag.Parse()` know where the arguments are?
- What if a user provides invalid flag values?

**Error Handling:**
- When should you return an error vs panic?
- How do you provide context when wrapping errors?
- What's the difference between `fmt.Errorf()` and `errors.New()`?
- Should you log errors or return them (or both)?

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
