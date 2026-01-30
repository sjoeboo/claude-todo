---
name: todo:complete
description: Mark a TODO item as complete and archive it to DONE.md
argument-hint: <task description or number>
allowed-tools:
  - Task
---

# Complete TODO Item

Mark a task as done, remove it from TODO.md, and archive it to DONE.md.

## Process

**Delegate to the `todo-manager` agent** with this prompt:

```
Complete and archive the following task:

Identifier: $ARGUMENTS

1. Find the task in TODO.md (by number or text match)
2. Remove it from TODO.md
3. Add it to DONE.md with today's date
4. Confirm completion with celebration and remaining count
```

Use the Task tool with:
- `subagent_type`: `todo-manager`
- `model`: `haiku` (for efficiency)

## Syntax Examples

```
/todo:complete 1        # Complete task #1
/todo:complete auth     # Complete task containing "auth"
/todo:complete security # Complete task containing "security"
```

## Archive Format

Completed tasks are moved to `DONE.md`:

```markdown
# Completed

- [x] 2026-01-30: !!! [auth] Fix security vulnerability
- [x] 2026-01-29: Write unit tests
```

## Output

```
✅ Completed: Fix security vulnerability
   Archived to DONE.md

   Remaining TODOs: 4
```
