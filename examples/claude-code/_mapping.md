---
status: draft
lang: en
---

# claude-code — Spec ↔ Source Mapping

## Mapping Table

| Spec File | Source File(s) | Status | Notes |
|-----------|---------------|--------|-------|
| `00_overview.md` | (project-wide) | draft | Project overview |
| `01_architecture.md` | (project-wide) | draft | Architecture decisions |
| `02_data_flow.md` | (project-wide) | draft | Data flow paths |
| `plugins/_index.md` | `plugins/` | draft | Plugins directory index |
| `plugins/code-review.md` | `plugins/code-review/` | skeleton | Code review plugin |
| `plugins/feature-dev.md` | `plugins/feature-dev/` | skeleton | Feature dev plugin |
| `plugins/plugin-dev.md` | `plugins/plugin-dev/` | skeleton | Plugin development toolkit |
| `plugins/commit-commands.md` | `plugins/commit-commands/` | skeleton | Git workflow commands |
| `plugins/security-guidance.md` | `plugins/security-guidance/` | skeleton | Security hooks |
| `plugins/hookify.md` | `plugins/hookify/` | skeleton | Custom hook creation |

## Unmapped Source Files

| Source File | Reason |
|------------|--------|
| `Script/run_devcontainer_claude_code.ps1` | DevContainer utility script |
| `scripts/` | GitHub automation scripts (operational, not product code) |
| `examples/` | Example configurations |
| `CHANGELOG.md` | Release history |
| `LICENSE.md` | License file |
| `SECURITY.md` | Security policy |
