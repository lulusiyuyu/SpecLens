---
status: draft
maps_to: "internal/"
lang: en
---

# internal/ — Index

## Overview

The `internal/` directory contains all of OpenCode's implementation, following Go's standard project layout convention. It includes the application core, TUI, LLM agent system, database layer, session/message management, and supporting utilities. Nothing in `internal/` is importable by external packages.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| app | `internal/app/` | Application initialization and LSP setup |
| tui | `internal/tui/` | Bubble Tea terminal user interface |
| llm | `internal/llm/` | LLM agent, providers, tools, and prompts |
| session | `internal/session/` | Conversation session management |
| message | `internal/message/` | Chat message storage and retrieval |
| history | `internal/history/` | Conversation history management |
| db | `internal/db/` | SQLite database layer (sqlc-generated) |
| config | `internal/config/` | Application configuration loading |
| pubsub | `internal/pubsub/` | Internal event publish/subscribe system |
| lsp | `internal/lsp/` | Language Server Protocol client |
| permission | `internal/permission/` | User permission management for tool execution |
| diff | `internal/diff/` | File change diff tracking and visualization |
| format | `internal/format/` | Text formatting utilities |
| fileutil | `internal/fileutil/` | File system utility helpers |
| logging | `internal/logging/` | Logging configuration |

## Module Relationships

- **app** initializes all services and launches **tui**
- **tui** depends on **llm**, **session**, **message** for user interactions
- **llm/agent** orchestrates **llm/provider** and **llm/tools** in a loop
- **session** and **message** depend on **db** for persistence
- **pubsub** is used across layers for event-driven updates
- **permission** gates tool execution on user approval
