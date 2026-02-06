# claude-todo

Track TODOs as GitHub Issues with automatic project board integration.

## Features

- **GitHub Issues backend** - All TODOs stored in `ghe.spotify.net/mnicholson/claude-todos`
- **Project board** - Visual kanban at `ghe.spotify.net/users/mnicholson/projects/1`
- **Auto-tracking** - Natural language triggers issue creation/completion
- **Project context** - Auto-detects current repo for filtering

## Installation

```
/plugins marketplace add sjoeboo/claude-todo
/plugins install todo@claude-todo
```

## Usage

### Slash Command

```
/todo add Fix the login bug
/todo list
/todo complete 5
/todo start 3
```

### Natural Language

The `work-tracker` skill responds to natural phrases:

- "add a todo for X" → creates issue
- "what are my todos" → lists issues
- "mark #5 as done" → closes issue
- "start working on #3" → moves to In Progress

### Auto-Tracking

When you ask Claude to implement/fix something, it can automatically:
1. Create an issue for the work
2. Move to In Progress when starting
3. Close when complete

## Board Columns

| Column | Trigger |
|--------|---------|
| Todo | Issue created |
| In Progress | `/todo start N` |
| Blocked | `/todo block N` |
| Done | `/todo complete N` |

## Configuration

Required in `~/.claude/settings.json`:

```json
{
  "env": {
    "GH_HOST": "ghe.spotify.net",
    "CLAUDE_TODO_REPO": "mnicholson/claude-todos",
    "CLAUDE_TODO_PROJECT": "1"
  }
}
```

## License

MIT
