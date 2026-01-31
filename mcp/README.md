# Declutter MCP Server (Optional)

For power users who want faster scanning.

## Install

```bash
pip install fastmcp
```

## Configure

Add to `~/.claude/mcp_servers.json`:

```json
{
  "declutter": {
    "command": "fastmcp",
    "args": ["run", "/path/to/declutter/mcp/server.py"]
  }
}
```

## Usage

The skill will automatically use the MCP tool if available:

```python
mcp__declutter__declutter(path="/path/to/project")
mcp__declutter__declutter(path="/path/to/project", fix=True)
```

## Why MCP?

- Faster than running bash commands each time
- Consistent output format
- Better error handling
- ~200 token footprint
