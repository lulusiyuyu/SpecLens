---
status: draft
maps_to: "internal/llm/"
lang: en
---

# llm/ — Index

## Overview

The `llm/` module is the core AI subsystem of OpenCode. It implements the agent loop (LLM calls → tool execution → repeat), manages multiple LLM providers, defines available tools, handles prompt construction, and tracks model configurations. This is the brain of the application.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| agent | `internal/llm/agent/` | Agent loop orchestrating LLM ↔ tool-call cycles |
| provider | `internal/llm/provider/` | LLM provider implementations (Anthropic, OpenAI, Gemini, etc.) |
| tools | `internal/llm/tools/` | Tool implementations (bash, file ops, search, LSP) |
| prompt | `internal/llm/prompt/` | System prompt construction |
| models | `internal/llm/models/` | Model configuration and capability definitions |

## Module Relationships

- **agent** is the top-level orchestrator, calling **provider** for LLM inference and **tools** for execution
- **provider** implementations each wrap a specific LLM SDK
- **tools** implement the `Tool` interface for the agent to invoke
- **prompt** constructs the system message consumed by all providers
- **models** defines available models and their capabilities per provider
