---
status: draft
lang: en
---

# OpenCode — Spec ↔ Source Mapping

## Mapping Table

| Spec File | Source File(s) | Status | Notes |
|-----------|---------------|--------|-------|
| `00_overview.md` | (project-wide) | draft | Project overview |
| `01_architecture.md` | (project-wide) | draft | Architecture decisions |
| `02_data_flow.md` | (project-wide) | draft | Data flow paths |
| `internal/_index.md` | `internal/` | draft | Internal package index |
| `internal/llm/_index.md` | `internal/llm/` | draft | LLM subsystem index |
| `internal/llm/agent.md` | `internal/llm/agent/` | skeleton | LLM agent loop |
| `internal/llm/provider.md` | `internal/llm/provider/` | skeleton | LLM provider interface |
| `internal/llm/tools.md` | `internal/llm/tools/` | skeleton | Tool implementations |
| `internal/tui/_index.md` | `internal/tui/` | draft | TUI index |
| `internal/session.md` | `internal/session/` | skeleton | Session service |
| `internal/message.md` | `internal/message/` | skeleton | Message service |
| `internal/db.md` | `internal/db/` | skeleton | Database layer |
| `internal/config.md` | `internal/config/` | skeleton | Configuration |
| `internal/pubsub.md` | `internal/pubsub/` | skeleton | Pub/sub system |

## Unmapped Source Files

| Source File | Reason |
|------------|--------|
| `main.go` | Simple entry point, delegates to cmd/ |
| `cmd/schema/` | Schema generation utility |
| `internal/format/` | Text formatting utilities |
| `internal/fileutil/` | File utility helpers |
| `internal/logging/` | Logging configuration |
| `internal/version/` | Version string |
| `internal/completions/` | Shell completions |
| `install/` | Installation scripts |
| `scripts/` | Build scripts |
