# Declutter (Archived)

> **Status:** SUNSET - This tool solved a problem that no longer exists.

## Why Archived

Claude Code 2.1.29+ handles large workspaces natively. The memory leak that inspired this tool was [fixed upstream](https://status.claude.com/incidents/rl6pphjrc2r4) on January 31, 2026.

## Historical Context

Built January 2026 when Claude Code would freeze on workspaces with:
- 938MB log files
- 1GB+ node_modules
- 500MB Python venvs

The tool detected bloat and auto-generated `.claudeignore` files.

## Original Functionality

```
@declutter              # Scan workspace, show report
@declutter --fix        # Scan + create .claudeignore
```

Detected: node_modules, .venv, target/, .build/, DerivedData/, *.log, *.db

## Lessons Learned

1. **Check GitHub issues first** - Before building a fix, check if a fix is already in progress
2. **Wait 48 hours** - Urgency is the enemy of durability
3. **Build for permanent problems** - Tools that fix temporary bugs die when the bug is fixed

## License

MIT

---

*Archived: 2026-02-01*
*Sunset reason: [Claude Code 2.1.29 fixed memory leak](https://status.claude.com/incidents/rl6pphjrc2r4)*
