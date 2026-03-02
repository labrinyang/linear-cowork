---
name: linear-cowork
description: Use when working on any project that uses Linear for issue tracking, or when the user mentions Linear issues, tickets, creating issues, updating issue status, linking commits to issues, or any Linear MCP interaction. Always activate this skill for issue creation, status updates, commit workflows, and project organization in Linear.
---

# Linear Cowork

Standardized Linear collaboration workflow for vibe coding teams.

## MCP Setup

Before using this skill, ensure the Linear MCP server is installed and authenticated.

**Quick setup for Claude Code:**
```bash
claude mcp add --transport http linear-server https://mcp.linear.app/mcp
```

**Quick setup for Codex:**
```bash
codex mcp add linear --url https://mcp.linear.app/mcp
```

For Cursor setup and detailed instructions for all tools, see `setup-guide.md` in this skill directory.

## Issue Conventions

### Naming Rule

All issue titles MUST follow this format:

```
[Type] Short description
```

**Valid types:**

| Type | When to use |
|------|-------------|
| `[Feature]` | New functionality |
| `[Bug]` | Bug fix |
| `[Chore]` | Maintenance, dependencies, config |
| `[Refactor]` | Code restructuring without behavior change |
| `[Docs]` | Documentation changes |

**Examples:**
- `[Feature] Add OAuth login flow`
- `[Bug] Fix crash on empty cart submission`
- `[Chore] Upgrade React to v19`

**Bad examples (DO NOT use):**
- `add login` — missing type prefix
- `[Feature] Login` — too vague, not descriptive
- `Feature: add login` — wrong format, must use brackets

### Description Template

Every issue description MUST include these two sections:

```markdown
## Background
[Why this issue exists. What problem it solves. Any relevant context.]

## Acceptance Criteria
- [ ] [Specific, testable criterion]
- [ ] [Another criterion]
```

**Do not skip Acceptance Criteria.** Even for small tasks, at least one criterion is required.

## Workflow Rules

### Default Assignment

When creating an issue via the Linear MCP, **always assign it to "me"** (the current authenticated user) unless the user explicitly specifies a different assignee.

### Subagent Delegation for Linear Operations

**CRITICAL: All Linear MCP read/write operations SHOULD be delegated to a lightweight subagent to save context.**

Linear data (issue lists, descriptions, comments) can be very verbose and wastes main conversation context.

**How to delegate (by tool):**
- **Claude Code:** Use the Task tool with `subagent_type="general-purpose"` and `model="haiku"`
- **Codex / Cursor:** If subagent spawning is available, use it. Otherwise, proceed with direct MCP calls but keep interactions concise — request only the fields you need.

**When to delegate:**
- Listing issues
- Reading issue details
- Creating new issues
- Updating issue status, assignee, or description
- Adding comments to issues
- Any other Linear MCP operation

**Exception:** If the user is actively discussing a specific issue and needs real-time back-and-forth, you may use the MCP tools directly. But default to subagent delegation.

### Project Organization

- Use Linear **Projects** to group related issues by feature area or milestone
- Before creating issues, check if a relevant project exists
- If no project exists and the work spans 3+ issues, create a project first

## Pre-commit Checklist

**Before every commit, follow this flow:**

```
About to commit?
  ├─ Related to Linear issue?
  │   ├─ Unknown → Ask user for issue ID
  │   │   ├─ User confirms → Update status to completed, include ID in commit
  │   │   └─ No issue → Proceed with commit
  │   ├─ Yes, known → Update status to completed, include ID in commit
  │   └─ No → Proceed with commit
```

**Steps:**

1. Before committing, ask: *"Is this commit related to a Linear issue? If so, which one (e.g., ONE-123)?"*
2. If user provides an issue ID:
   - Use a **subagent** to update the issue status to a **completed state** (check the team's available statuses first if unsure — common names: "Done", "Completed", "Closed")
   - Include the issue ID in the commit message, e.g.: `[ONE-123] Fix cart crash on empty submission`
3. If user says no issue is related, proceed with the commit normally.

### Commit Message Format with Issue ID

```
[ISSUE-ID] commit message

# Examples:
[ONE-42] Add OAuth login flow
[ONE-15] Fix crash on empty cart submission
```

## Quick Reference

| Action | Rule |
|--------|------|
| Issue title | `[Type] Short description` |
| Issue description | Background + Acceptance Criteria sections |
| Assign issue | Default to "me" unless user specifies otherwise |
| Read/write Linear | Delegate to lightweight subagent |
| Before commit | Confirm issue ID, update status to completed |
| Commit message | `[ISSUE-ID] message` |
| Multiple related issues | Group under a Project |
