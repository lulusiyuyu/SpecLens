---
status: draft
maps_to: "openhands/"
lang: en
---

# openhands/ — Index

## Overview

The `openhands/` package is the core Python library implementing the entire OpenHands AI agent framework. It contains the agent implementations, event system, LLM abstraction, sandboxed runtime, web server, and all supporting infrastructure. This is the primary source directory — everything outside it (frontend, tests, scripts, containers) is auxiliary.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| core | `openhands/core/` | Main loop, configuration, setup, and fundamental utilities |
| controller | `openhands/controller/` | Agent lifecycle orchestration, state management, stuck detection |
| agenthub | `openhands/agenthub/` | Collection of agent implementations (CodeAct, Browsing, etc.) |
| events | `openhands/events/` | Event system — actions, observations, stream, serialization |
| llm | `openhands/llm/` | LLM provider abstraction with retry, streaming, and metrics |
| runtime | `openhands/runtime/` | Sandboxed execution environments (Docker containers) |
| memory | `openhands/memory/` | Conversation memory management and context condensation |
| server | `openhands/server/` | FastAPI web server, REST API, WebSocket, session management |
| storage | `openhands/storage/` | Pluggable file storage backends (local, S3, GCS) |
| security | `openhands/security/` | Security policies and invariant enforcement |
| integrations | `openhands/integrations/` | External service integrations (GitHub, Slack, etc.) |
| mcp | `openhands/mcp/` | Model Context Protocol support |
| resolver | `openhands/resolver/` | Automated GitHub issue/PR resolution |
| microagent | `openhands/microagent/` | Specialized micro-agent prompts |
| io | `openhands/io/` | Input/output handling |
| critic | `openhands/critic/` | Agent output evaluation |
| app_server | `openhands/app_server/` | Application server utilities |

## Module Relationships

- **core** provides the main loop and configuration consumed by all modules
- **controller** orchestrates **agenthub** agents via the **events** stream
- **agents** use **llm** for AI calls and **runtime** for code execution
- **memory** consumes **events** to manage context for **agents**
- **server** exposes **controller** functionality via HTTP/WebSocket
- **storage** is the persistence backend used by **events**, **server**, and **memory**
