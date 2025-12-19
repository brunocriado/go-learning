# Project 14: Custom Shell/REPL

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

Build a custom shell with REPL (Read-Eval-Print Loop), command parsing, job control, and pipeline support.

**Difficulty:** Intermediate  
**Estimated Time:** 25-35 hours

## What You'll Learn

- REPL implementation
- Command parsing and lexing
- Process execution
- Pipeline implementation (|)
- I/O redirection
- Job control (background jobs, fg/bg)
- Signal handling
- Shell builtins

## Core Features

### 1. Command Execution
- Parse command line
- Execute external commands
- Environment variables
- PATH resolution
- Exit codes

### 2. Pipelines
- Pipe operator (|)
- Multiple commands
- Standard streams
- Error handling

### 3. Builtins
- cd, pwd, exit
- export, unset
- history
- alias
- jobs, fg, bg

### 4. Job Control
- Background execution (&)
- Foreground/background switching
- Job status
- Signal forwarding

## Implementation Guide

```go
package main

import (
    "bufio"
    "fmt"
    "os"
    "os/exec"
    "strings"
)

type Shell struct {
    commands map[string]func([]string) error
    env      map[string]string
    history  []string
    jobs     []*Job
}

type Job struct {
    ID      int
    Command string
    Cmd     *exec.Cmd
    Status  string
}

func NewShell() *Shell {
    sh := &Shell{
        commands: make(map[string]func([]string) error),
        env:      make(map[string]string),
    }
    
    // Register builtins
    sh.commands["cd"] = sh.cd
    sh.commands["pwd"] = sh.pwd
    sh.commands["exit"] = sh.exit
    sh.commands["export"] = sh.export_
    
    return sh
}

func (sh *Shell) Run() {
    reader := bufio.NewReader(os.Stdin)
    
    for {
        fmt.Print("$ ")
        line, _ := reader.ReadString('\n')
        line = strings.TrimSpace(line)
        
        if line == "" {
            continue
        }
        
        sh.history = append(sh.history, line)
        
        // Parse and execute
        if err := sh.Execute(line); err != nil {
            fmt.Fprintln(os.Stderr, err)
        }
    }
}

func (sh *Shell) Execute(line string) error {
    // Check for pipeline
    if strings.Contains(line, "|") {
        return sh.executePipeline(line)
    }
    
    // Parse command
    parts := strings.Fields(line)
    if len(parts) == 0 {
        return nil
    }
    
    cmd := parts[0]
    args := parts[1:]
    
    // Check for builtin
    if fn, ok := sh.commands[cmd]; ok {
        return fn(args)
    }
    
    // Execute external command
    return sh.executeExternal(cmd, args)
}

func (sh *Shell) executePipeline(line string) error {
    commands := strings.Split(line, "|")
    
    var cmds []*exec.Cmd
    for i, cmdStr := range commands {
        parts := strings.Fields(strings.TrimSpace(cmdStr))
        cmd := exec.Command(parts[0], parts[1:]...)
        
        if i > 0 {
            // Connect stdout of previous to stdin of current
            cmd.Stdin, _ = cmds[i-1].StdoutPipe()
        }
        
        if i == len(commands)-1 {
            cmd.Stdout = os.Stdout
        }
        
        cmd.Stderr = os.Stderr
        cmds = append(cmds, cmd)
    }
    
    // Start all commands
    for _, cmd := range cmds {
        if err := cmd.Start(); err != nil {
            return err
        }
    }
    
    // Wait for all commands
    for _, cmd := range cmds {
        if err := cmd.Wait(); err != nil {
            return err
        }
    }
    
    return nil
}

func (sh *Shell) executeExternal(cmd string, args []string) error {
    command := exec.Command(cmd, args...)
    command.Stdin = os.Stdin
    command.Stdout = os.Stdout
    command.Stderr = os.Stderr
    
    return command.Run()
}

func (sh *Shell) cd(args []string) error {
    if len(args) == 0 {
        return os.Chdir(os.Getenv("HOME"))
    }
    return os.Chdir(args[0])
}

func (sh *Shell) pwd(args []string) error {
    wd, err := os.Getwd()
    if err != nil {
        return err
    }
    fmt.Println(wd)
    return nil
}

func (sh *Shell) exit(args []string) error {
    os.Exit(0)
    return nil
}

func (sh *Shell) export_(args []string) error {
    for _, arg := range args {
        parts := strings.SplitN(arg, "=", 2)
        if len(parts) == 2 {
            os.Setenv(parts[0], parts[1])
        }
    }
    return nil
}

func main() {
    shell := NewShell()
    shell.Run()
}
```

## Project Structure

```
custom-shell/
├── main.go
├── shell/
│   ├── shell.go
│   ├── parser.go
│   ├── executor.go
│   └── builtins.go
├── job/
│   └── control.go
└── README.md
```

## Next Steps

- Add tab completion
- Implement aliases
- Command history with arrow keys
- Move to [Project 15: Packet Sniffer](project-15-packet-sniffer.md)

---

[← Back to Intermediate Projects](README.md) | [↑ Back to Index](../../projects-index.md)
