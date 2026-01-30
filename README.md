# claude-todo

A TODO management plugin for Claude Code. Track tasks with priorities and tags in a `TODO.md` file, with completed items archived to `DONE.md`.

## Features

- **Priority levels**: `!!!` (critical), `!!` (medium), `!` (low)
- **Tags**: `[backend]`, `[auth]`, etc. for categorization
- **Archive**: Completed tasks preserved in `DONE.md` with timestamps
- **Context-efficient**: Uses Haiku subagent for CRUD operations, keeping main context clean
- **Integrated workflow**: `/todo:do` leverages Claude's planning for task execution

## Installation

```bash
# Step 1: Add the marketplace
claude plugins add-marketplace sjoeboo/claude-todo

# Step 2: Install the plugin
claude plugins install todo@claude-todo
```

Or if you prefer a one-liner using the GitHub URL:
```bash
claude plugins add-marketplace https://github.com/sjoeboo/claude-todo && claude plugins install todo@claude-todo
```

## Commands

| Command | Description |
|---------|-------------|
| `/todo:add <task>` | Add a new TODO item (with optional priority/tags) |
| `/todo:list [tag]` | Show all TODO items (optionally filter by tag) |
| `/todo:complete <item>` | Mark as done and archive to DONE.md |
| `/todo:remove <item>` | Remove without archiving |
| `/todo:do <item>` | Work on a TODO (plan → execute → complete) |
| `/todo:help` | Show help for all commands |

## Usage

### Adding Tasks with Priority & Tags

```
/todo:add Implement user authentication
/todo:add !!! Fix critical security bug
/todo:add !! [backend] Add rate limiting
/todo:add [frontend][a11y] Improve keyboard navigation
```

### Priority Levels

| Marker | Level | Use Case |
|--------|-------|----------|
| `!!!` | Critical | Security issues, blocking bugs |
| `!!` | Medium | Important features, reviews |
| `!` | Low | Nice-to-haves, docs |
| (none) | Normal | Regular tasks |

### Viewing Tasks

```
/todo:list              # Show all tasks (sorted by priority)
/todo:list backend      # Show only [backend] tagged tasks
```

Output:
```
📋 TODO (5 pending)
═══════════════════════════════════════

Critical (2):
  1. !!! [auth] Fix security vulnerability
  2. !!! Deploy hotfix

Medium (1):
  3. !! [backend] Add rate limiting

Normal (2):
  4. [frontend] Update button styles
  5. Write documentation

───────────────────────────────────────
Tags: auth(1), backend(1), frontend(1)
```

### Completing Tasks

Tasks can be referenced by number or text match:

```
/todo:complete 1        # Complete task #1
/todo:complete auth     # Complete task containing "auth"
```

Completed tasks are archived to `DONE.md`:
```markdown
# Completed

- [x] 2026-01-30: !!! [auth] Fix security vulnerability
- [x] 2026-01-29: Write unit tests
```

### Working on Tasks

The `/todo:do` command provides a full workflow:

1. Selects the task
2. Explores the codebase for context
3. Enters plan mode to design implementation
4. Asks clarifying questions if needed
5. Executes the plan after approval
6. Archives the task to DONE.md

```
/todo:do 1
/todo:do auth
```

## Architecture

```
claude-todo/
├── .claude-plugin/
│   ├── marketplace.json  # Marketplace definition (for distribution)
│   └── plugin.json       # Plugin manifest
├── agents/
│   └── todo-manager.md   # Haiku subagent for CRUD operations
├── commands/
│   ├── add.md            # /todo:add
│   ├── list.md           # /todo:list
│   ├── complete.md       # /todo:complete
│   ├── remove.md         # /todo:remove
│   ├── do.md             # /todo:do (full workflow)
│   └── help.md           # /todo:help
├── LICENSE
└── README.md
```

### Why a Subagent?

The CRUD commands (`add`, `list`, `complete`, `remove`) delegate to a Haiku-powered subagent. This keeps the main conversation context clean for complex work while still providing quick task management.

## Storage

| File | Purpose |
|------|---------|
| `TODO.md` | Active tasks in current directory |
| `DONE.md` | Archived completed tasks with timestamps |

Both files use simple markdown checkbox format that's portable and human-readable.

## License

MIT
