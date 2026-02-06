---
name: todo
description: Manage TODOs via GitHub Issues - add, list, complete, start, block
argument-hint: "<action> [item]"
allowed-tools:
  - Bash
---

# TODO Manager

Handle TODO operations. Parse $ARGUMENTS for action and item.

## Actions

Detect from $ARGUMENTS:
- add/new/create → Add
- list/show/todos → List
- done/complete/close/finish → Complete
- start/begin/working → Start
- block/stuck → Block
- unblock/resume → Unblock

## Get Project

```bash
gh repo view --json nameWithOwner -q '.nameWithOwner' 2>/dev/null | sed 's|.*/||'
```

If empty, use "personal".

## Add

```bash
gh label create "project:PROJECT" --repo mnicholson/claude-todos --color 0366d6 2>/dev/null || true
URL=$(gh issue create --repo mnicholson/claude-todos --title "TITLE" --label "project:PROJECT" --body "From: PROJECT")
gh project item-add 1 --owner mnicholson --url "$URL"
```

## List

```bash
gh issue list --repo mnicholson/claude-todos --state open --label "project:PROJECT" --json number,title --limit 30
```

## Complete

```bash
gh issue close N --repo mnicholson/claude-todos
```

## Start

```bash
ITEM=$(gh project item-list 1 --owner mnicholson --format json --jq ".items[] | select(.content.number == N) | .id")
gh project item-edit --project-id MDk6UHJvamVjdFYyNjUw --id "$ITEM" --field-id MDI2OlByb2plY3RWMlNpbmdsZVNlbGVjdEZpZWxkODE4OQ== --single-select-option-id 47fc9ee4
```

## Block/Unblock

Get option IDs from `gh project field-list 1 --owner mnicholson --format json`, then item-edit.
