# linear-cowork

Standardized Linear collaboration skill for vibe coding teams.

## Prerequisites

- A [Linear](https://linear.app) account
- One of: [Claude Code](https://claude.ai/code), [Codex](https://openai.com/codex), [Cursor](https://cursor.com), VS Code, Windsurf, or Zed

## Install

```bash
npx skills add labrinyang/linear-cowork
```

Or install globally:

```bash
npx skills add labrinyang/linear-cowork -g
```

## What This Skill Does

- Guides Linear MCP setup for Claude Code, Codex, Cursor, VS Code, Windsurf, and Zed
- Enforces issue naming: `[Type] Short description`
- Enforces issue description template: Background + Acceptance Criteria
- Auto-assigns issues to the current user with "Todo" status
- Delegates Linear operations to lightweight subagents (saves context)
- Pre-commit check: confirms issue linkage and auto-updates status to completed

## Usage

Once installed, just type `/linear-cowork` in your AI coding tool to activate the skill. Then work as usual — the skill handles the rest automatically:

```
/linear-cowork          ← activate the skill
Create an issue for...  ← issues follow naming & description conventions
Fix the bug in...       ← before commit, skill confirms issue linkage
```

**That's it.** The skill will:
- Format issue titles as `[Type] Description` and fill in Background + Acceptance Criteria
- Assign issues to you with "Todo" status
- Prompt you to link commits to issues and auto-update status to "Done"

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
