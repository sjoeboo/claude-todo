---
name: todo:add
description: Add a new TODO item to the project's TODO.md file
argument-hint: "[!!!|!!|!] [tag] <description>"
allowed-tools:
  - Task
---

# Add TODO Item

Add a new task to the `TODO.md` file using the todo-manager subagent.

## Process

**Delegate to the `todo-manager` agent** with this prompt:

```
Add the following task to TODO.md:

Task: $ARGUMENTS

Parse any priority markers (!!!, !!, !) and tags ([tagname]) from the input.
Create TODO.md if it doesn't exist.
Confirm the addition with priority and tags displayed.
```

Use the Task tool with:
- `subagent_type`: `todo-manager`
- `model`: `haiku` (for efficiency)

## Syntax Examples

```
/todo:add Implement user authentication
/todo:add !!! Fix critical security bug
/todo:add !! [backend] Add rate limiting
/todo:add [frontend][a11y] Improve keyboard navigation
```

## Priority Levels

- `!!!` = Critical/High priority
- `!!` = Medium priority
- `!` = Low priority
- (none) = Normal priority

## Tags

- `[tag]` = Category (e.g., `[auth]`, `[frontend]`, `[bugfix]`)
- Multiple tags: `[auth][security]`
