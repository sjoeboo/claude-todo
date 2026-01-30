---
name: todo:do
description: Work on a TODO item - enters plan mode, clarifies requirements, executes, and marks complete
argument-hint: <task description or number>
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - Task
  - AskUserQuestion
  - EnterPlanMode
---

# Do TODO Item

Pick a TODO item and work on it through a complete workflow: plan, clarify, execute, and complete.

## Process

### Step 1: Find the Task

1. **Read TODO.md** to get the list of pending tasks
2. **Match the argument** to find the specific task:
   - If a number is provided, use that position (1-indexed)
   - If text is provided, find the matching task
   - If no argument, show the list and ask which one to work on

### Step 2: Understand the Task

1. **Display the selected task** clearly
2. **Explore the codebase** if needed to understand context:
   - Use `codebase-locator` or `Explore` agents to find relevant files
   - Read related code to understand the current state

### Step 3: Enter Plan Mode

1. **Use EnterPlanMode** to create an implementation plan
2. In plan mode:
   - Analyze what needs to be done
   - Identify files to modify or create
   - Consider edge cases and testing
   - Write a clear plan for user approval

### Step 4: Clarify (if needed)

If the task is ambiguous, use **AskUserQuestion** to clarify:
- Scope boundaries
- Implementation preferences
- Acceptance criteria

### Step 5: Present the Plan

Present a clear plan to the user including:
- What will be changed
- How it will be implemented
- Any risks or considerations

Wait for user approval before proceeding.

### Step 6: Execute

Upon approval:
1. Implement the changes as planned
2. Run any relevant tests
3. Verify the implementation works

### Step 7: Complete

After successful implementation and user acceptance:
1. Remove the task from TODO.md (same as `/todo:complete`)
2. Celebrate the completion!

## Example Flow

```
User: /todo:do 1

Claude: 📋 Selected task: "Implement user authentication"

Let me explore the codebase to understand the current state...
[uses Explore agent to find auth-related files]

I'll now enter plan mode to design the implementation.
[enters plan mode, creates plan]

Here's my plan:
1. Create auth middleware in src/middleware/auth.ts
2. Add login/logout routes in src/routes/auth.ts
3. ...

Shall I proceed with this plan?

User: Yes

[implements changes]

✅ Completed: Implement user authentication

Remaining TODOs: 2
```

## Important

- Always get user approval before making changes
- Use plan mode for non-trivial implementations
- Ask clarifying questions early, not during implementation
- Mark complete only after user accepts the work
