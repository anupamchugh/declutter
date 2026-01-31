# Declutter

Detect workspace bloat and auto-generate `.claudeignore` for Claude Code.

## Problem

Claude Code freezes on large workspaces because it indexes everything:
- 938MB log files
- 1GB+ node_modules
- 500MB Python venvs
- Database files, build caches, coverage reports

## Solution

One command to find bloat, estimate wasted tokens, and create `.claudeignore`:

```
@declutter              # Scan workspace, show report
@declutter --fix        # Scan + create .claudeignore
```

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

## What Gets Detected

| Marker | Type | Ignores |
|--------|------|---------|
| requirements.txt | Python | .venv/, __pycache__/, *.pyc |
| package.json | Node | node_modules/, .next/, dist/ |
| Package.swift | Swift | .build/, DerivedData/ |
| Cargo.toml | Rust | target/ |
| go.mod | Go | vendor/ |

Plus: *.log, *.db, *.parquet, htmlcov/

## Installation

### As Claude Code Plugin

```bash
claude plugins add anupamchugh/declutter
```

### Manual

Copy `skills/declutter/SKILL.md` to `~/.claude/skills/declutter/`

### With MCP (Power Users)

For faster scanning, install the optional MCP server:

```bash
pip install fastmcp
# Add to ~/.claude/mcp_servers.json:
{
  "declutter": {
    "command": "fastmcp",
    "args": ["run", "path/to/mcp/server.py"]
  }
}
```

## Token Math

```
Tokens wasted ≈ bloat_bytes / 4

Example:
5GB bloat = 1.25 billion tokens that could be used for actual code
```

## License

MIT
