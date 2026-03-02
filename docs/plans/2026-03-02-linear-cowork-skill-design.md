# Linear Cowork Skill Design

## Problem

Teams using vibe coding tools (Claude Code, Codex, Cursor) need a standardized way to collaborate via Linear. Without conventions, issues are inconsistently named, descriptions lack structure, and there's no automated link between code commits and issue status.

## Requirements

1. **MCP Setup Guide** for Claude Code, Codex, and Cursor
2. **Issue naming**: `[Type] Short description` format
3. **Issue description**: Background + Acceptance Criteria template
4. **Default assignment**: Issues created by agent are assigned to "me"
5. **Haiku subagent**: All Linear read/write operations use haiku model to save context
6. **Pre-commit flow**: Before committing, confirm associated issue and auto-update status to Done

## Design

### Skill Structure

```
linear-cowork/
├── package.json           # npm package metadata for npx skills
├── SKILL.md               # Main skill file (installed by npx skills add)
├── setup-guide.md         # Detailed MCP install guide per tool
├── README.md              # GitHub project documentation
```

### SKILL.md Sections

1. **Overview** — What this skill does
2. **MCP Setup** — References setup-guide.md for per-tool install instructions
3. **Issue Conventions** — Naming rules, type list, description template
4. **Workflow Rules** — Default assignment, haiku subagent usage
5. **Pre-commit Checklist** — Steps to confirm issue linkage and update status

### Issue Types

- `[Feature]` — New functionality
- `[Bug]` — Bug fix
- `[Chore]` — Maintenance, deps, config
- `[Refactor]` — Code restructuring
- `[Docs]` — Documentation changes

### Issue Description Template

```markdown
## Background
[Why this issue exists, context]

## Acceptance Criteria
- [ ] [Criterion 1]
- [ ] [Criterion 2]
```

### Haiku Subagent Rule

When reading or updating Linear issues, always use:
```
Task tool with subagent_type="general-purpose", model="haiku"
```
This prevents expensive context consumption in the main conversation.

### Pre-commit Flow

1. Before committing, check if current work relates to a Linear issue
2. Prompt user to confirm the issue ID (e.g., ONE-123)
3. On confirmation, use haiku subagent to update issue status to "Done"
4. Include issue ID in commit message

### Distribution

- Hosted on GitHub as `labrinyang/linear-cowork`
- Install: `npx skills add labrinyang/linear-cowork`
- Supports global (`-g`) and project-level installation

## Approach

Single SKILL.md with setup-guide.md as supporting reference file. This keeps the skill lightweight while providing detailed setup instructions for each tool without bloating the main file.
