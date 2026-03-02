# linear-cowork

Standardized Linear collaboration skill for vibe coding teams using Claude Code, Codex, and Cursor.

## Prerequisites

- Node.js >= 18
- A [Linear](https://linear.app) account
- One of: [Claude Code](https://claude.ai/code), [Codex](https://openai.com/codex), or [Cursor](https://cursor.com)

## Install

```bash
npx skills add labrinyang/linear-cowork
```

Or install globally:

```bash
npx skills add labrinyang/linear-cowork -g
```

## What This Skill Does

- Guides Linear MCP setup for Claude Code, Codex, and Cursor
- Enforces issue naming: `[Type] Short description`
- Enforces issue description template: Background + Acceptance Criteria
- Auto-assigns issues to the current user
- Delegates Linear operations to lightweight subagents (saves context)
- Pre-commit check: confirms issue linkage and auto-updates status to completed

## Manual Install

Copy `SKILL.md` and `setup-guide.md` to your skills directory:

**Claude Code:**
```bash
mkdir -p ~/.claude/skills/linear-cowork && cp SKILL.md setup-guide.md ~/.claude/skills/linear-cowork/
```

**Codex:**
```bash
mkdir -p ~/.codex/skills/linear-cowork && cp SKILL.md setup-guide.md ~/.codex/skills/linear-cowork/
```

**Cursor:**
```bash
mkdir -p ~/.cursor/skills/linear-cowork && cp SKILL.md setup-guide.md ~/.cursor/skills/linear-cowork/
```

## License

MIT
