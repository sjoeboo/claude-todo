---
name: work-tracker
description: "Automatically track work as GitHub Issues. Use when user mentions: 'add a todo', 'mark as done', 'what are my todos', 'start working on', 'finished', 'block', 'unblock'."
---

# Automatic Work Tracker

Track work using GitHub Issues in a centralized repository.

## Environment

- GH_HOST is set to ghe.spotify.net (use gh commands directly)
- Repo: mnicholson/claude-todos
- Project number: 1

## Get Current Project

```bash
gh repo view --json nameWithOwner -q '.nameWithOwner' 2>/dev/null | sed 's|.*/||'
```

If empty, use "personal".

## Actions

### Add TODO

Triggers: "add a todo for X", "todo: X", "need to X", "remember to X"

```bash
# Create label if needed
gh label create "project:PROJECT" --repo mnicholson/claude-todos --color 0366d6 2>/dev/null || true

# Create issue
gh issue create --repo mnicholson/claude-todos --title "TITLE" --label "project:PROJECT" --body "From: PROJECT"

# Add to board
gh project item-add 1 --owner mnicholson --url "URL"
```

Output: ✅ Added: #N TITLE

### List TODOs

Triggers: "what are my todos", "show todos", "list tasks", "open issues"

```bash
gh issue list --repo mnicholson/claude-todos --state open --label "project:PROJECT" --json number,title --limit 30
```

### Complete TODO

Triggers: "mark X as done", "finished X", "close X", "complete X"

```bash
gh issue close N --repo mnicholson/claude-todos
```

Output: ✅ Completed: #N TITLE

### Start Working

Triggers: "start working on X", "begin X"

```bash
# Get item ID
ITEM=$(gh project item-list 1 --owner mnicholson --format json --jq ".items[] | select(.content.number == N) | .id")

# Set to In Progress
gh project item-edit --project-id MDk6UHJvamVjdFYyNjUw --id "$ITEM" --field-id MDI2OlByb2plY3RWMlNpbmdsZVNlbGVjdEZpZWxkODE4OQ== --single-select-option-id 47fc9ee4
```

Output: 🚀 Started: #N TITLE

### Block

Triggers: "blocked on X", "stuck on X"

Get Blocked option ID from field-list, then item-edit with that option.

### Unblock

Triggers: "unblock X", "resume X"

Same as Start (moves to In Progress).

## Auto-Tracking

When user requests substantial work (implement, fix, add feature):

1. Create issue if none exists
2. Move to In Progress when implementing
3. Close when done

Be lightweight - inform, don't prompt.
