# Declutter (Archived)

> **Status:** SUNSET - This tool solved a problem that no longer exists.

## Why Archived

Claude Code 2.1.29+ handles large workspaces natively. The memory leak that inspired this tool was [fixed upstream](https://status.claude.com/incidents/rl6pphjrc2r4) on January 31, 2026.

**Yegge Survival Score:** Below 1.0
- Insight Compression: Low (agents know ignore patterns)
- Broad Utility: Low (only Claude + large workspaces + freezing = triple-and)
- See full analysis: Applied Steve Yegge's Software Survival 3.0 framework

## Historical Context

Built January 2026 when Claude Code would freeze on workspaces with:
- 938MB log files
- 1GB+ node_modules
- 500MB Python venvs

The tool detected bloat and auto-generated `.claudeignore` files.

## What Survives (Pivot Ideas)

If resurrecting this concept, pivot to higher-survival alternatives:

| Pivot | Why It Survives |
|-------|-----------------|
| **@context-budget** | Token cost per file/directory for ANY LLM tool |
| **Universal .ignore** | Generate ignores for git, docker, cursor, copilot, etc. |
| **Codebase Tokenizer** | Compare two codebases for token efficiency |

These have broader utility than "Claude + large workspace + freezing."

## Original Functionality

```
@declutter              # Scan workspace, show report
@declutter --fix        # Scan + create .claudeignore
```

Detected: node_modules, .venv, target/, .build/, DerivedData/, *.log, *.db

## Architecture (Historical)

```
┌─────────────────────────────────┐
│         @declutter              │
│         (Skill)                 │
│  - Workflow orchestration       │
│  - User interaction             │
└───────────────┬─────────────────┘
                │
                ▼
┌─────────────────────────────────┐
│   mcp__declutter__declutter     │
│         (MCP Tool)              │
│  - Project detection            │
│  - .claudeignore generation     │
└─────────────────────────────────┘
```

## Lessons Learned

1. **Build for durability, not urgency** - Tools that fix temporary problems die when the problem is fixed
2. **Yegge's framework works** - "Crazy to re-synthesize" is the right bar
3. **Substrate efficiency alone isn't enough** - CPU file scanning is cheap, but narrow utility kills survival

## License

MIT

---

*Archived: 2026-02-01*
*Sunset reason: [Claude Code 2.1.29 fixed memory leak](https://status.claude.com/incidents/rl6pphjrc2r4)*
