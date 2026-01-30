---
name: todo:list
description: List all TODO items from the project's TODO.md file
argument-hint: "[tag filter]"
allowed-tools:
  - Task
---

# List TODO Items

Display all tasks from the `TODO.md` file using the todo-manager subagent.

## Process

**Delegate to the `todo-manager` agent** with this prompt:

```
List all tasks from TODO.md.

Filter: $ARGUMENTS (if provided, filter by this tag)

Display tasks sorted by priority (highest first).
Show counts of pending tasks by priority level.
If a tag filter is provided, only show tasks with that tag.
```

Use the Task tool with:
- `subagent_type`: `todo-manager`
- `model`: `haiku` (for efficiency)

## Syntax Examples

```
/todo:list              # Show all tasks
/todo:list backend      # Show only [backend] tagged tasks
/todo:list auth         # Show only [auth] tagged tasks
```

## Output Format

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
