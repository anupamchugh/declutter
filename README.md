# Declutter

Detect workspace bloat and auto-generate `.claudeignore` for Claude Code.

**Requires:** Skill + MCP server working together.

## Problem

Claude Code freezes on large workspaces because it indexes everything:
- 938MB log files
- 1GB+ node_modules
- 500MB Python venvs
- Database files, build caches, coverage reports

## Solution

A skill + MCP tool that scans for bloat, estimates wasted tokens, and creates `.claudeignore`:

```
@declutter              # Scan workspace, show report
@declutter --fix        # Scan + create .claudeignore
```

## Installation

### 1. Install MCP Server

```bash
pip install fastmcp
```

### 2. Add to Claude Config

Add to `~/.claude/mcp_servers.json`:

```json
{
  "declutter": {
    "command": "fastmcp",
    "args": ["run", "/path/to/declutter/mcp/server.py"]
  }
}
```

### 3. Install Skill

Copy `skills/declutter/SKILL.md` to `~/.claude/skills/declutter/`

Or install as plugin:
```bash
claude plugins add anupamchugh/declutter
```

### 4. Restart Claude Code

## Example

```
@declutter

Scanning workspace...

| Project | Type | Bloat | Status |
|---------|------|-------|--------|
| webapp | node | 1.2GB | ✗ needs fix |
| api | python | 400MB | ✓ exists |

1 project needs .claudeignore. Fix it?

> yes

✓ webapp/.claudeignore created (5 patterns)
Restart Claude to apply.
```

## MCP Tool

```python
mcp__declutter__declutter(path=".", fix=False)
```

| Param | Type | Default | Description |
|-------|------|---------|-------------|
| path | str | "." | Project path to scan |
| fix | bool | False | Create .claudeignore if True |

## What Gets Detected

| Marker | Type | Ignores |
|--------|------|---------|
| requirements.txt | Python | .venv/, __pycache__/, *.pyc |
| package.json | Node | node_modules/, .next/, dist/ |
| Package.swift | Swift | .build/, DerivedData/ |
| Cargo.toml | Rust | target/ |
| go.mod | Go | vendor/ |

Plus: *.log, *.db, *.parquet, htmlcov/

## Token Math

```
Tokens wasted ≈ bloat_bytes / 4

Example:
5GB bloat = 1.25 billion tokens that could be used for actual code
```

## Architecture

```
┌─────────────────────────────────┐
│         @declutter              │
│         (Skill)                 │
│  - Workflow orchestration       │
│  - User interaction             │
│  - Approval flow                │
└───────────────┬─────────────────┘
                │
                ▼
┌─────────────────────────────────┐
│   mcp__declutter__declutter     │
│         (MCP Tool)              │
│  - Project detection            │
│  - Size calculation             │
│  - .claudeignore generation     │
└─────────────────────────────────┘
```

## License

MIT
