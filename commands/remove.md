---
name: todo:remove
description: Remove a TODO item without archiving (use complete to archive)
argument-hint: <task description or number>
allowed-tools:
  - Task
---

# Remove TODO Item

Remove a task from TODO.md without archiving it. Use `/todo:complete` instead if you finished the task.

## Process

**Delegate to the `todo-manager` agent** with this prompt:

```
Remove the following task from TODO.md (do NOT archive):

Identifier: $ARGUMENTS

1. Find the task in TODO.md (by number or text match)
2. If multiple matches, list them and ask which to remove
3. Remove the task permanently (no archive)
4. Confirm removal with remaining count
```

Use the Task tool with:
- `subagent_type`: `todo-manager`
- `model`: `haiku` (for efficiency)

## Syntax Examples

```
/todo:remove 3          # Remove task #3
/todo:remove old        # Remove task containing "old"
```

## When to Use

- **`/todo:remove`**: Task is no longer relevant, was a duplicate, or was added by mistake
- **`/todo:complete`**: Task was actually finished (archives to DONE.md)

## Output

```
🗑️ Removed: Old task that's no longer needed

   Remaining TODOs: 3
```
