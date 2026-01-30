---
name: todo:help
description: Show help for TODO management commands
allowed-tools: []
---

# TODO Management Help

Display usage information for all TODO commands.

## Output

```
📋 TODO Management Commands
═══════════════════════════════════════════════════════════════

/todo:add <task>        Add a new TODO item
/todo:list [tag]        Show all TODO items (optionally filter by tag)
/todo:complete <item>   Mark as done and archive to DONE.md
/todo:remove <item>     Remove without archiving
/todo:do <item>         Work on a TODO (plan → execute → complete)
/todo:help              Show this help message

───────────────────────────────────────────────────────────────

PRIORITY LEVELS
  !!!  Critical/High    e.g., /todo:add !!! Fix security bug
  !!   Medium           e.g., /todo:add !! Review PR
  !    Low              e.g., /todo:add ! Update docs
  (none) Normal         e.g., /todo:add Write tests

TAGS
  [tag]  Category       e.g., /todo:add [auth] Implement login
  Multiple tags         e.g., /todo:add [api][security] Add auth

ITEM SELECTORS
  Number    Position    e.g., /todo:complete 1
  Text      Fuzzy match e.g., /todo:complete auth

───────────────────────────────────────────────────────────────

FILES
  TODO.md   Active tasks in current directory
  DONE.md   Archived completed tasks

EXAMPLES
  /todo:add !!! [backend] Fix database connection leak
  /todo:list backend
  /todo:complete 1
  /todo:do auth
  /todo:remove "old task"
```
