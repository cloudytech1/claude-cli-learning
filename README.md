# Claude Code CLI - Getting Started Guide

A practical guide to mastering Claude Code, your AI-powered coding companion for the terminal.

## Table of Contents

1. [Installation](#installation)
2. [Authentication](#authentication)
3. [Essential Commands](#essential-commands)
4. [Your First Session](#your-first-session)
5. [Project Configuration (CLAUDE.md)](#project-configuration-claudemd)
6. [Best Practices](#best-practices)
7. [Common Workflows](#common-workflows)
8. [Managing Sessions & Context](#managing-sessions--context)
9. [Advanced Features](#advanced-features)
10. [Keyboard Shortcuts](#keyboard-shortcuts)

---

## Installation

### Recommended: Native Installation

Native installations auto-update in the background.

**macOS and Linux:**
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**Windows PowerShell:**
```powershell
irm https://claude.ai/install.ps1 | iex
```

### Alternative: Homebrew (macOS)

```bash
brew install --cask claude-code
```

> Note: Homebrew requires manual updates via `brew upgrade claude-code`

### Verify Installation

```bash
claude doctor
```

---

## Authentication

### First Launch

```bash
cd /path/to/your/project
claude
```

You'll be prompted to log in with either:

| Option | Best For |
|--------|----------|
| **Claude Pro/Max** | Personal use with flat monthly rate |
| **Claude Console** | API users with pay-per-token billing |

### Switch Accounts Later

```
> /login
```

---

## Essential Commands

Type `/` in Claude to see all commands. Here are the most important:

### Daily Use

| Command | Purpose |
|---------|---------|
| `/help` | Show all available commands |
| `/clear` | Clear conversation history |
| `/exit` | Exit Claude Code (or Ctrl+C) |
| `/cost` | Show token usage and costs |
| `/status` | Show version, model, account info |

### Session Management

| Command | Purpose |
|---------|---------|
| `/resume [name]` | Resume a previous conversation |
| `/rename <name>` | Name the current session |
| `/compact` | Compress context to free up space |
| `/context` | Visualize context window usage |

### Configuration

| Command | Purpose |
|---------|---------|
| `/init` | Create CLAUDE.md for your project |
| `/config` | Open settings interface |
| `/model` | Select a different AI model |
| `/memory` | Edit CLAUDE.md memory files |

---

## Your First Session

### Understand Your Codebase

```
> what does this project do?
> explain the folder structure
> what technologies does this use?
```

### Make a Change

```
> add a hello world function to main.py
```

Claude will:
1. Show you the proposed changes
2. Ask for your approval
3. Apply the changes once confirmed

### Exit

```
> /exit
```
Or press `Ctrl+C`

---

## Project Configuration (CLAUDE.md)

The `CLAUDE.md` file stores instructions Claude reads automatically on startup.

### Create One

```
> /init
```

### Example CLAUDE.md

```markdown
# Project Memory

## Tech Stack
- Frontend: React 18 with TypeScript
- Backend: Node.js with Express
- Database: PostgreSQL

## Key Commands
- `npm run dev` - Start development server
- `npm test` - Run unit tests
- `npm run build` - Production build

## Code Style
- Use 2-space indentation
- Prefer async/await over callbacks
- Include JSDoc comments for public functions

## Architecture Notes
- API routes in /src/routes
- Database queries in /src/db
- React components in /src/components
```

### Import Other Files

Reference other documentation in your CLAUDE.md:

```markdown
See @README for project overview.
See @docs/architecture.md for system design.
```

---

## Best Practices

### 1. Be Specific

**Instead of:**
```
> fix the bug
```

**Try:**
```
> fix the login bug where users see a blank screen after wrong credentials
```

### 2. Break Down Complex Tasks

```
> 1. create a database table for user profiles
> 2. create an API endpoint to get/update profiles
> 3. build a form for users to edit their info
```

### 3. Let Claude Explore First

Before making changes:
```
> analyze the database schema
> find where user authentication happens
```

### 4. Name Your Sessions

```
> /rename auth-refactor
```

Resume later:
```bash
claude --resume auth-refactor
```

### 5. Use Plan Mode for Risky Changes

Start in read-only analysis mode:
```bash
claude --permission-mode plan
```

Or toggle with `Shift+Tab` during a session.

### 6. Keep CLAUDE.md Updated

Document decisions as you make them:
- New architectural patterns
- Important dependencies
- Team conventions

### 7. Test Before Committing

```
> run the test suite and fix any failures
```

---

## Common Workflows

### Fixing Bugs

```
> I'm seeing this error: [paste error]
> suggest ways to fix it
> apply the recommended fix
> run tests to verify
```

### Code Review

```
> review my changes for potential issues
> focus on security and performance
```

### Git Operations

```
> what files have I changed?
> commit with a descriptive message
> create a PR for these changes
```

### Writing Tests

```
> write unit tests for the calculator functions
> add edge cases
> run tests and fix failures
```

### Refactoring

```
> find deprecated API usage
> refactor utils.js to use modern JavaScript
> ensure tests still pass
```

### Unix Pipes

Use Claude in scripts:
```bash
cat code.py | claude -p "check for bugs" > review.txt
cat data.csv | claude -p "convert to JSON" > data.json
```

---

## Managing Sessions & Context

### Resume Conversations

**Continue most recent session:**
```bash
claude --continue
```

**Resume by name:**
```bash
claude --resume auth-refactor
```

**Show session picker:**
```bash
claude --resume
```

### Context Window

Your conversation has limited memory. Check usage:
```
> /context
```

Shows a colored grid:
- Green = available space
- Used blocks = conversation history

### Free Up Space

```
> /compact
```

Or with focus:
```
> /compact focus on the authentication changes
```

### Auto-Compaction

Claude automatically compacts at ~95% capacity. Override this:
```bash
export CLAUDE_AUTOCOMPACT_PCT_OVERRIDE=50
```

---

## Advanced Features

### Hooks

Automate actions on tool events. Open the interface:
```
> /hooks
```

**Example:** Auto-format after edits
- Event: `PostToolUse`
- Matcher: `Edit` or `Write`
- Command: `npx prettier --write`

### MCP Servers

Connect Claude to external tools:

```bash
# Add GitHub integration
claude mcp add --transport http github https://api.githubcopilot.com/mcp/

# Add a database
claude mcp add --transport stdio db -- npx -y @bytebase/dbhub \
  --dsn "postgresql://user:pass@localhost/mydb"

# Check status
> /mcp
```

### Extended Thinking

Enable deep analysis for complex problems:
- Toggle: `Option+T` (macOS) or `Alt+T` (Windows/Linux)
- See thinking: `Ctrl+O` for verbose mode

### IDE Integration

**VS Code:** Install the Claude extension from marketplace

**JetBrains:** Install from IDE marketplace

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+C` | Exit Claude Code |
| `Ctrl+O` | Toggle verbose mode (show thinking) |
| `Option+T` / `Alt+T` | Toggle thinking mode |
| `Shift+Tab` | Cycle permission modes |
| `Tab` | Command completion |
| `↑` / `↓` | Command history |
| `?` | Show all shortcuts |

---

## File Locations

### User Settings
```
~/.claude/settings.json     # Personal settings
~/.claude/CLAUDE.md         # Personal memory (all projects)
```

### Project Settings
```
.claude/settings.json       # Project settings (shared)
.claude/settings.local.json # Personal overrides (gitignored)
.claude/CLAUDE.md           # Project memory
CLAUDE.md                   # Alternative location
```

---

## Quick Reference Card

```
Starting:     claude                    # Start in current directory
              claude --continue         # Resume last session
              claude --resume name      # Resume named session

During:       /help                     # Show commands
              /clear                    # Clear history
              /compact                  # Free up context
              /cost                     # Show usage

Sessions:     /rename my-task           # Name this session
              /resume                   # Switch sessions

Config:       /init                     # Create CLAUDE.md
              /config                   # Open settings

Exiting:      /exit or Ctrl+C           # Exit Claude
```

---

## Next Steps

1. Run `/init` in your project to create a CLAUDE.md
2. Try asking Claude to explain your codebase
3. Make a small change and commit it
4. Name your session with `/rename`
5. Explore `/help` for more commands

Happy coding!
