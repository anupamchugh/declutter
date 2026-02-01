# Declutter (Archived)

> **Status:** SUNSET - This tool solved a problem that no longer exists.

## Why Archived

Claude Code 2.1.29+ handles large workspaces natively. The memory leak that inspired this tool was [fixed upstream](https://status.claude.com/incidents/rl6pphjrc2r4) on January 31, 2026.

**Yegge Survival Score:** 0.8 (Below threshold)

| Lever | Score | Reason |
|-------|-------|--------|
| Insight Compression | Low | Agents already know ignore patterns |
| Substrate Efficiency | High | Pure CPU file scanning, no inference |
| Broad Utility | **Low** | Triple-AND: Claude + large workspace + freezing |
| Low Friction | Medium | Easy CLI, but why bother now? |
| Awareness | Low | Nobody knew it existed |
| Human Coefficient | Low | Solo project, no community |

**Killer:** Broad Utility. When the bug was fixed, 2/3 of the market vanished.

## Historical Context

Built January 2026 when Claude Code would freeze on workspaces with:
- 938MB log files
- 1GB+ node_modules
- 500MB Python venvs

The tool detected bloat and auto-generated `.claudeignore` files.

## What Survives (Pivot Ideas)

If resurrecting this concept, pivot to higher-survival alternatives:

### @context-budget — Token Cost Calculator

| Lever | Score | Why |
|-------|-------|-----|
| Insight Compression | **High** | "This folder costs 50k tokens" is novel |
| Substrate Efficiency | High | CPU tokenizer, no inference |
| Broad Utility | **High** | Works with ANY LLM tool (Claude, Cursor, Copilot, GPT) |
| Low Friction | High | Drop-in CLI or VS Code extension |
| **Yegge Score** | **1.4** | **SURVIVES** |

### Universal .ignore Generator

| Lever | Score | Why |
|-------|-------|-----|
| Insight Compression | Medium | Pattern libraries exist, but unified is new |
| Substrate Efficiency | High | Pure CPU pattern matching |
| Broad Utility | **High** | Git, Docker, Cursor, Copilot, Claude, Prettier... |
| Low Friction | High | One command, all ignores |
| **Yegge Score** | **1.2** | **SURVIVES** |

### Codebase Tokenizer (Diff Tool)

| Lever | Score | Why |
|-------|-------|-----|
| Insight Compression | **High** | "Repo A costs 2x more than Repo B" is actionable |
| Substrate Efficiency | High | CPU comparison |
| Broad Utility | Medium | Useful for LLM cost optimization |
| Low Friction | Medium | Needs two repos to compare |
| **Yegge Score** | **1.1** | **SURVIVES** |

All three survive because they solve *permanent* problems (token costs, ignore patterns) not *temporary* bugs.

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
