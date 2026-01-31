---
name: declutter
description: Scan workspace for bloat, show what's worth cleaning, ask before fixing. Use when workspaces are slow, Claude freezes, or periodic cleanup.
---

# Declutter

Finds bloated projects, shows the damage, asks before fixing.

## Usage

```
@declutter                    # Scan current workspace
@declutter /path/to/workspace # Scan specific workspace
@declutter --auto             # Fix all without asking
```

## MCP Tool

This skill uses the `mcp__declutter__declutter` tool:

```python
mcp__declutter__declutter(path=".", fix=False)
```

| Param | Type | Default | Description |
|-------|------|---------|-------------|
| path | str | "." | Project or workspace path |
| fix | bool | False | Create .claudeignore if True |

## Workflow

### Step 1: Identify Workspace

Use current directory or user-provided path.

### Step 2: Scan Each Project

For each top-level directory in workspace:

```python
mcp__declutter__declutter(path=f"{workspace}/{project}")
```

### Step 3: Build Report

Aggregate results into a table:

| Project | Type | Bloat | Tokens Wasted | Status |
|---------|------|-------|---------------|--------|
| my-app | node | 500MB | ~125M | ✗ needs fix |
| api | python | 200MB | ~50M | ✓ has .claudeignore |

### Step 4: Ask for Approval

> **Projects needing .claudeignore:**
> 1. my-app (500MB bloat)
> 2. old-project (300MB bloat)
>
> Fix all, fix specific, or skip?

### Step 5: Apply Fixes

For approved projects:

```python
mcp__declutter__declutter(path=f"{workspace}/{project}", fix=True)
```

### Step 6: Report Results

```
✓ my-app/.claudeignore created (8 patterns)
✓ old-project/.claudeignore created (5 patterns)

Total savings: ~175M tokens
Restart Claude for changes to take effect.
```

## What Gets Detected

| Marker | Type | Ignores |
|--------|------|---------|
| requirements.txt, pyproject.toml | Python | .venv/, __pycache__/, *.pyc |
| package.json | Node | node_modules/, .next/, dist/ |
| Package.swift, *.xcodeproj | Swift | .build/, DerivedData/ |
| Cargo.toml | Rust | target/ |
| go.mod | Go | vendor/ |

Plus: *.log, *.db, *.parquet, htmlcov/

## Example Session

**User:** @declutter

**Claude:**
```python
# Scanning workspace
mcp__declutter__declutter(path="/Users/dev/projects/webapp")
mcp__declutter__declutter(path="/Users/dev/projects/api")
```

```
| Project | Bloat | Status |
|---------|-------|--------|
| webapp | 1.2GB | ✗ needs fix |
| api | 400MB | ✓ exists |

1 project needs .claudeignore. Fix it?
```

**User:** yes

**Claude:**
```python
mcp__declutter__declutter(path="/Users/dev/projects/webapp", fix=True)
```

```
✓ webapp/.claudeignore created
Restart Claude to apply.
```

## Installation

Add MCP server to `~/.claude/mcp_servers.json`:

```json
{
  "declutter": {
    "command": "fastmcp",
    "args": ["run", "/path/to/declutter/mcp/server.py"]
  }
}
```

Requires: `pip install fastmcp`
