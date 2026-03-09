---
status: draft
lang: en
---

# OpenHands — Spec ↔ Source Mapping

## Mapping Table

| Spec File | Source File(s) | Status | Notes |
|-----------|---------------|--------|-------|
| `00_overview.md` | (project-wide) | draft | Project overview |
| `01_architecture.md` | (project-wide) | draft | Architecture decisions |
| `02_data_flow.md` | (project-wide) | draft | Data flow paths |
| `openhands/_index.md` | `openhands/` | draft | Core package index |
| `openhands/core/_index.md` | `openhands/core/` | draft | Core module index |
| `openhands/core/main.md` | `openhands/core/main.py` | skeleton | CLI entry + main loop |
| `openhands/core/loop.md` | `openhands/core/loop.py` | skeleton | Agent execution loop |
| `openhands/controller/_index.md` | `openhands/controller/` | draft | Controller index |
| `openhands/controller/agent_controller.md` | `openhands/controller/agent_controller.py` | skeleton | Agent controller |
| `openhands/agenthub/_index.md` | `openhands/agenthub/` | draft | Agent implementations index |
| `openhands/agenthub/codeact_agent.md` | `openhands/agenthub/codeact_agent/` | skeleton | CodeAct agent |
| `openhands/events/_index.md` | `openhands/events/` | draft | Event system index |
| `openhands/events/stream.md` | `openhands/events/stream.py` | skeleton | Event stream |
| `openhands/llm/_index.md` | `openhands/llm/` | draft | LLM layer index |
| `openhands/llm/llm.md` | `openhands/llm/llm.py` | skeleton | Core LLM interface |
| `openhands/runtime/_index.md` | `openhands/runtime/` | draft | Runtime index |
| `openhands/runtime/base.md` | `openhands/runtime/base.py` | skeleton | Base runtime |
| `openhands/memory/_index.md` | `openhands/memory/` | draft | Memory index |
| `openhands/server/_index.md` | `openhands/server/` | draft | Server index |
| `openhands/storage/_index.md` | `openhands/storage/` | draft | Storage index |

## Unmapped Source Files

| Source File | Reason |
|------------|--------|
| `openhands/version.py` | Simple version string, trivial |
| `openhands/py.typed` | PEP 561 marker file |
| `openhands/linter/` | Internal linting utilities |
| `openhands/utils/` | General utility functions |
| `tests/` | Test files (not part of spec mirroring) |
| `frontend/` | React frontend (separate concern) |
| `containers/` | Docker configuration files |
| `scripts/` | Build/dev scripts |
