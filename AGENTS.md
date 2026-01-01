# AI Agent Guide for Golang Learning Projects

This document provides critical information for AI coding agents (GitHub Copilot, Claude, ChatGPT, Cursor, etc.) working with this codebase.

---

## 📋 Project Overview

**Repository**: Golang Learning Projects - Complete Mastery Path  
**Total Projects**: 54 production-ready projects  
**Structure**: Organized by difficulty level (Basic → Expert → Specialized → Bonus)  
**Purpose**: Comprehensive Go learning path covering roadmap.sh/golang and roadmap.sh/system-design

---

## 🗂️ Repository Structure

```
go-learning/
├── golang-learning-projects.md    # Master guide (19,464 lines, all project details)
├── golang-learning-projects-improvements.md  # Enhancement ideas
├── check-later.txt                 # Notes and todos
├── projects/                       # Extracted project files
│   ├── 01-basic/                  # Projects 1-6
│   │   ├── README.md
│   │   ├── project-01-cli-todo.md
│   │   ├── project-02-url-shortener.md
│   │   ├── project-03-file-organizer.md
│   │   ├── project-04-process-monitor.md
│   │   ├── project-05-log-analyzer.md
│   │   └── project-06-system-monitor.md
│   ├── 02-intermediate/           # Projects 7-18
│   │   ├── README.md
│   │   ├── project-07.md
│   │   ├── ...
│   │   └── project-18.md
│   ├── 03-advanced/               # Projects 19-21
│   │   ├── README.md
│   │   ├── project-19.md
│   │   ├── project-20.md
│   │   └── project-21.md
│   ├── 04-expert/                 # Projects 22-30
│   │   ├── README.md
│   │   ├── project-22.md
│   │   ├── ...
│   │   └── project-30.md
│   ├── 05-specialized/            # Projects 31-36
│   │   ├── README.md
│   │   ├── project-31.md
│   │   ├── ...
│   │   └── project-36.md
│   └── 06-bonus/                  # Projects 37-54
│       ├── README.md
│       ├── project-37.md
│       ├── ...
│       └── project-54.md
├── implementations/                # Separate Git repos for actual code
│   ├── README.md
│   ├── project-01-todo-cli/       # Individual Git repository
│   ├── project-02-url-shortener/  # Individual Git repository
│   └── ...                        # Each project is its own Git repository
├── documentation/                  # Package documentation guides
│   ├── go-flag-package-complete-guide.md
│   ├── go-tabwriter-package-complete-guide.md
│   └── go-net-http-package-complete-guide.md
├── guides/
│   └── getting-started.md
├── README.md                       # Main navigation hub
├── MASTER-INDEX.md                # Complete project catalog
├── FILE-ORGANIZATION.md           # Structure documentation
└── AGENTS.md                      # This file
```

---

## 🎯 Agent Responsibilities & Constraints

### When Extracting/Creating Project Files

**DO:**
- ✅ Extract complete implementation details from `golang-learning-projects.md`
- ✅ Include: Overview, Prerequisites, What You'll Learn, Core Features, Implementation Guide, Code Examples, Project Structure
- ✅ Preserve all code blocks, explanations, and technical depth
- ✅ Add navigation links (← Back to Level README | ↑ Back to Index)
- ✅ Reference line numbers in source file for full details
- ✅ Maintain consistent formatting across all project files

**DON'T:**
- ❌ Create placeholder files with only titles (user explicitly rejected this)
- ❌ Summarize or omit implementation details
- ❌ Reference source file instead of extracting content
- ❌ Create "summary files" - all files must have substantial content
- ❌ Use scripts to batch-create files - extract content manually

### Quality Standards

Each project file must contain **300-800 lines** including:
1. **Overview section**: Difficulty, time estimate, prerequisites
2. **What You'll Learn**: Specific skills and concepts
3. **Core Features**: 4-8 key features with descriptions
4. **Implementation Guide**: Step-by-step with code examples
5. **Project Structure**: Directory tree showing file organization
6. **Best Practices**: Do's and don'ts
7. **Full Details Reference**: Line numbers in source file for complete implementation
8. **Task Checklist**: Detailed, actionable tasks WITHOUT solutions (see Task Checklist Standards below)

**Example Quality Benchmarks:**
- Project 1 (CLI Todo): ~500 lines with file I/O, JSON examples, 60+ task checklist items
- Project 7 (REST API): ~400 lines with PostgreSQL, JWT, middleware
- Project 19 (Container Runtime): ~500 lines with namespaces, cgroups
- Project 28 (gRPC): ~450 lines with protobuf, streaming examples

### Task Checklist Standards

**CRITICAL**: Task checklists guide learners WITHOUT providing solutions. Follow these rules:

**DO:**
- ✅ Break work into small, checkable tasks (5-15 tasks per phase)
- ✅ Organize tasks into logical phases (Setup, Implementation, Testing, Refinement)
- ✅ Ask guiding questions that promote research and discovery
- ✅ Point to concepts learners need to research (e.g., "Research what a mutex is")
- ✅ Identify edge cases and error scenarios to consider
- ✅ Include debugging questions that promote critical thinking
- ✅ Make tasks specific enough to be actionable (not vague)
- ✅ Include validation/testing tasks after implementation tasks

**DON'T:**
- ❌ Provide code solutions or pseudocode
- ❌ Give away the answer (e.g., "Use `sync.RWMutex`" - instead say "Research how to make maps thread-safe")
- ❌ Write tasks that are too broad (e.g., "Implement the feature")
- ❌ Skip challenging aspects - guide through them with questions
- ❌ Provide complete function signatures or implementations
- ❌ Tell exactly which library/package to use (let them discover)

**Task Checklist Structure:**

```markdown
## 📋 Task Checklist

### Phase 1: Project Setup & Foundation
- [ ] **Task 1.1**: [Setup action - specific and measurable]
- [ ] **Task 1.2**: [Research task - what concept to learn]
- [ ] **Task 1.3**: [Implementation task - what to build, not how]

### Phase 2: Core Implementation
- [ ] **Task 2.1**: [Feature task - guides what, not how]
- [ ] **Task 2.2**: [Research question - investigate technique]
- [ ] **Task 2.3**: [Edge case - scenario to handle]

### Phase 3: Testing & Validation
- [ ] **Task 3.1**: [Test scenario to verify]
- [ ] **Task 3.2**: [Edge case testing]

### Phase 4: Refinement
- [ ] **Task 4.1**: [Improvement or optimization]

### Bonus Challenges (Optional)
- [ ] **Bonus 1**: [Advanced feature suggestion]

## 🤔 Debugging Questions to Ask Yourself

**[Category Name]:**
- Why [design decision question]?
- What happens if [edge case scenario]?
- How does [concept] work under the hood?
- When should you [technique A] vs [technique B]?
```

**Example Good Tasks** (from Project 1):
- ✅ "Research `json.MarshalIndent()` vs `json.Marshal()` - which is better for debugging?"
- ✅ "Figure out how to remove an element from a slice without leaving gaps"
- ✅ "Handle the case when the JSON file doesn't exist yet (first run)"
- ✅ "Test edge cases: deleting non-existent ID, completing already completed todo"

**Example Bad Tasks** (too solution-oriented):
- ❌ "Use `sync.RWMutex` to make the map thread-safe"
- ❌ "Implement using the following code: [code block]"
- ❌ "Call `json.MarshalIndent(data, "", "  ")` for pretty printing"

**Task Naming Convention:**
- Use format: `**Task X.Y**: [Action verb] [specific goal]`
- Bonus tasks: `**Bonus X**: [Challenge description]`
- Number phases sequentially (Phase 1, 2, 3...)
- Number tasks within phases (1.1, 1.2, 1.3...)

**Phases to Include** (adjust per project complexity):
1. **Phase 1**: Project Setup & Foundation (5-10 tasks)
2. **Phase 2-4**: Implementation phases based on project structure (10-20 tasks each)
3. **Phase N**: Testing & Debugging (10-15 tasks)
4. **Phase N+1**: Refinement & Polish (5-10 tasks)
5. **Bonus Challenges**: Optional advanced features (5-10 items)

**Target Task Count:**
- **Basic Projects (1-6)**: 50-70 tasks total
- **Intermediate Projects (7-18)**: 60-90 tasks total
- **Advanced Projects (19-21)**: 80-120 tasks total
- **Expert/Specialized (22-36)**: 70-100 tasks total
- **Bonus Projects (37-54)**: 40-60 tasks total (more focused)

### When Creating Documentation Guides

**Documentation Philosophy**: Teach the **why** and **how**, not just the **what**.

**DO:**
- ✅ **Provide theoretical foundations**: Explain underlying concepts before showing code
- ✅ **Add historical context**: Why does this feature exist? What problem does it solve?
- ✅ **Explain design decisions**: Why did Go choose this approach over alternatives?
- ✅ **Include visual explanations**: Memory layouts, byte sequences, data flow diagrams
- ✅ **Show the reasoning**: Why does this solution work? What happens under the hood?
- ✅ **Compare alternatives**: When to use X vs Y, with detailed trade-offs
- ✅ **Provide real-world context**: Where is this used in actual applications?
- ✅ **Explain common pitfalls**: Why do they happen? What's the underlying cause?

**DON'T:**
- ❌ Only provide code examples without explanation
- ❌ Skip the "why" and jump to "how"
- ❌ Assume concepts are self-evident from code alone
- ❌ Omit historical or design context
- ❌ Provide shallow explanations ("it works this way because it does")

**Example Quality Standard:**

Instead of:
```markdown
## Rune Type
A rune is an int32 representing a Unicode code point.
```

Provide:
```markdown
## Rune Type

**Definition**: A rune is an alias for int32 that represents a Unicode code point.

**Why 32 bits?** Unicode defines 1,112,064 possible code points:
- uint8: only 256 values ❌
- uint16: only 65,536 values ❌  
- int32: 2+ billion values ✅

**Why signed (int32) vs unsigned (uint32)?**
Historical compatibility with C's wchar_t...

**What problem does this solve?**
Before Unicode, ASCII only supported 128 characters (English only)...
```

**Documentation Targets:**
- **Length**: 700-1,500 lines for comprehensive package guides
- **Theory-to-example ratio**: 40% theory/context, 60% examples/patterns
- **Depth**: Explain 2-3 levels deep (not just surface concepts)

---

## 📖 Source Material

### Primary Source
**File**: `golang-learning-projects.md`  
**Size**: 19,464 lines  
**Content Distribution**:
- Lines 1-1500: Introduction, Basic Projects 1-6
- Lines 1500-8000: Intermediate Projects 7-18
- Lines 8000-10000: Advanced Projects 19-21
- Lines 10000-12500: Expert Projects 22-30
- Lines 12500-14000: Specialized Projects 31-36
- Lines 14000-19464: Bonus Projects 37-54 + Guides

### Content Sections
1. **Project Definitions**: Detailed specs for all 54 projects
2. **Observability Guide**: Logging, metrics, tracing (Prometheus, Grafana, OpenTelemetry)
3. **12-Factor App Integration**: How to apply 12-factor principles
4. **Design Patterns**: Complete GoF patterns + Go-specific concurrency patterns
5. **Additional Topics**: Testing, CGO, Modules, Build Tags, Assembly, Generics, Embed

---

## 🔍 Project Categories & Coverage

### Difficulty Levels

**Basic (1-6)**: CLI tools, file I/O, simple HTTP servers  
**Intermediate (7-18)**: REST APIs, databases, WebSockets, system utilities  
**Advanced (19-21)**: FUSE, eBPF, KVM hypervisor  
**Expert (22-30)**: Design patterns, testing, message queues, caching, load balancer, context, gRPC, tracing, auth  
**Specialized (31-36)**: CI/CD, Kubernetes operators, profiling, payments, cloud storage, reflection  
**Bonus (37-54)**: Generics, embed, build tags, CGO, modules, assembly, Saga, CQRS, patterns

### Topic Coverage

**Language Features**: All Go 1.18+ features (generics, fuzzing, workspaces, embed)  
**Backend**: REST, gRPC, WebSockets, databases (SQL, NoSQL), caching, sessions  
**Systems**: Filesystems, networking, processes, kernel (eBPF), virtualization  
**Distributed**: Microservices, message queues, distributed cache, load balancing, service mesh  
**DevOps**: CI/CD, Docker, Kubernetes, monitoring, tracing, logging  
**Security**: JWT, OAuth, RBAC, encryption, rate limiting  
**Patterns**: GoF patterns, CQRS, Saga, Circuit Breaker, Bulkhead, Sidecar, Strangler Fig

---

## 🛠️ Common Agent Tasks

### Task 1: Extracting Project Content

```
User Request: "Fill with right information these missing projects"
Agent Action:
1. Read golang-learning-projects.md at relevant line range
2. Extract complete project specification
3. Format with sections: Overview, Prerequisites, What You'll Learn, etc.
4. Include code examples (minimum 3-5 blocks per project)
5. Add detailed task checklist (50-120 tasks depending on complexity)
6. Add debugging questions section
7. Add navigation links
8. Save to appropriate projects/XX-level/project-YY.md
```

### Task 2: Adding Task Checklists to Existing Projects

```
User Request: "Add task checklist to Project X"
Agent Action:
1. Read the existing project file completely
2. Understand the project's structure and implementation guide
3. Create task checklist based on:
   - Setup and prerequisites
   - Each implementation step broken into sub-tasks
   - Testing and validation tasks
   - Refinement and polish tasks
   - Bonus challenges
4. Add debugging questions section
5. Insert checklist BEFORE "Project Structure" section
6. Ensure tasks guide without solving
7. Count tasks to meet targets (50-120 based on level)
```

### Task 3: Updating Navigation Files

```
Files to update when adding/modifying projects:
- README.md (main hub)
- projects/XX-level/README.md (level index)
- projects-index.md (flat list)
- MASTER-INDEX.md (complete catalog)
```

### Task 4: Working with Implementations

```
Structure:
- Each implementation is a SEPARATE Git repository
- Located in: implementations/ directory
- GitHub repos: <username>/go-project-XX-<name>
- Main repo contains project descriptions only
- Implementation repos contain actual code

Git workflow:
1. Create project folder in implementations/
2. Initialize git: git init
3. Commit code: git add . && git commit -m "message"
4. Create GitHub repo (via UI or gh CLI)
5. Add remote: git remote add origin https://github.com/<username>/<repo-name>.git
6. Push: git push -u origin main (or master)

NOTE: Do NOT commit implementation folders to main repository
```

### Task 4: Ensuring Consistency

**Formatting Rules**:
- Markdown headers: # for title, ## for sections, ### for subsections
- Code blocks: Use ```go, ```yaml, ```bash, ```sql appropriately
- Lists: Use - for bullets, 1. for ordered lists
- Links: [Text](URL) for external, [Text](file.md) for internal
- Navigation: Always include [← Back] and [↑ Up] links

---

## ⚠️ Critical User Preferences

Based on conversation history, the user:

1. **Expects Complete Content**: No placeholders, summaries, or references-only files
2. **Demands Action**: "Do what is necessary what you have done before" - extract like Projects 1-18
3. **Rejects Scripts**: "Don't execute script for this" - manual extraction preferred
4. **Values Quality**: Projects 1-30 are fully populated with 300-800 lines each
5. **Low Tolerance for Excuses**: Deliver results, not explanations of what's missing

---

## 📊 Progress Tracking

### Completion Status (as of Dec 31, 2025)

**Fully Extracted (32/54 projects)**:
- ✅ Projects 1-6 (Basic): Complete with full implementation guides
- ✅ Projects 7-18 (Intermediate): Complete with code examples
- ✅ Projects 19-21 (Advanced): Complete with kernel-level details
- ✅ Projects 22-30 (Expert): Complete with patterns and systems
- ✅ Projects 31-32 (Specialized): CI/CD and K8s Operator complete

**Remaining (22/54 projects)**:
- ⏳ Projects 33-36 (Specialized): Profiling, Payments, Cloud, Reflection
- ⏳ Projects 37-54 (Bonus): Generics, Embed, Build Tags, CGO, Modules, Assembly, Patterns

**Documentation Completed**:
- ✅ `go-flag-package-complete-guide.md` (1427 lines)
- ✅ `go-tabwriter-package-complete-guide.md`
- ✅ `go-net-http-package-complete-guide.md` (1400+ lines)

**Implementations in Progress**:
- ✅ Project 1 (CLI Todo): Completed, Git repo created
- 🔨 Project 2 (URL Shortener): In progress

### File Statistics
- Total markdown files: 64+ files
- Navigation files: 7 (README, indexes, guides)
- Level README files: 6 (one per difficulty level)
- Project files: 48 (32 complete, 16 remaining)
- Documentation files: 3 (package guides)
- Implementation READMEs: 1+

---

## 🔄 Workflow for Remaining Projects

### Step-by-Step Process

1. **Read Source Material**
   ```
   read_file(filepath="/Users/bruno/go-learning/golang-learning-projects.md", 
             startLine=XXXX, endLine=YYYY)
   ```

2. **Extract Project Content**
   - Identify project number and title
   - Copy complete specification (Overview → Resources)
   - Format with proper Markdown
   - Include all code examples

3. **Create/Update File**
   ```
   replace_string_in_file(
     filePath="/Users/bruno/go-learning/projects/XX-level/project-YY.md",
     oldString="# Project YY",
     newString="[Full content with 300+ lines]"
   )
   ```

4. **Verify Quality**
   - Check line count (300-800 lines target)
   - Ensure code blocks are present
   - Verify navigation links
   - Confirm sections are complete

---

## 💡 Best Practices for Agents

### Content Extraction
- **Read in chunks**: Source file is 19,464 lines - read 1500-2000 lines at a time
- **Preserve formatting**: Maintain code blocks, lists, emphasis
- **Include context**: Don't just copy-paste, ensure explanations flow
- **Add value**: Format for readability in standalone files

### Batch Operations
- **Use multi_replace_string_in_file**: When updating multiple files
- **Parallelize reads**: Can read different sections of source simultaneously
- **Group by level**: Process all projects in one difficulty level together

### Error Handling
- **Check file existence**: Before replacing content
- **Validate markdown**: Ensure no broken syntax
- **Test navigation links**: Relative paths must be correct
- **Verify code blocks**: Ensure language identifiers are present

---

## 📝 File Templates

### Project File Template

```markdown
# Project XX: [Title]

[← Back to [Level] Projects](README.md) | [↑ Back to Index](../../projects-index.md)

## Overview

[2-3 sentence description]

**Difficulty:** [Basic/Intermediate/Advanced/Expert/Specialized]  
**Estimated Time:** [hours]  
**Prerequisites:** [Previous projects needed]

## What You'll Learn

- [Key concept 1]
- [Key concept 2]
- [Key concept 3]
- [...]

## Core Features

1. **[Feature 1]:**
   - [Sub-feature]
   - [Sub-feature]

2. **[Feature 2]:**
   - [Sub-feature]

[...]

## Implementation Guide

### Step 1: [Setup/Foundation]

[Explanation]

```go
// Code example
```

### Step 2: [Core Implementation]

[...]

## Project Structure

```
project-name/
├── main.go
├── [package]/
│   ├── [file].go
│   └── [file]_test.go
├── [config]/
└── README.md
```

## Best Practices

**DO:**
- ✅ [Best practice 1]

**DON'T:**
- ❌ [Anti-pattern 1]

## Full Details

Complete implementation in `golang-learning-projects.md` (search "Project XX" or around line XXXX-YYYY):
- [Additional detail 1]
- [Additional detail 2]

---

[← Back to [Level] Projects](README.md) | [↑ Back to Index](../../projects-index.md)
```

---

## 🎓 Educational Philosophy

This repository follows a **project-based learning** approach:

1. **Learn by Building**: Theory is introduced as needed, not upfront
2. **Progressive Difficulty**: Each project builds on previous knowledge
3. **Production Quality**: All projects use industry best practices
4. **Career Focused**: Skills map directly to job requirements
5. **Modular Path**: Pick projects matching your career goals

---

## 🔗 Key References

- **Go Roadmap**: https://roadmap.sh/golang
- **System Design Roadmap**: https://roadmap.sh/system-design
- **12-Factor App**: https://12factor.net/
- **Go Documentation**: https://go.dev/doc/
- **Go Blog**: https://go.dev/blog/

---

## 📞 Agent Support

**For Questions About**:
- **Structure**: See FILE-ORGANIZATION.md
- **Navigation**: See README.md and MASTER-INDEX.md
- **Content**: Search golang-learning-projects.md
- **Progress**: Check completion status above

**Common Issues**:
1. **Missing content in project file** → Extract from golang-learning-projects.md
2. **Broken navigation links** → Verify relative paths from file location
3. **Inconsistent formatting** → Follow template above
4. **Unclear requirements** → User wants Projects 1-30 quality (300-800 lines)

---

**Last Updated**: December 31, 2025  
**Agent Version Compatibility**: All modern AI coding assistants  
**Maintained By**: Human + AI collaboration
