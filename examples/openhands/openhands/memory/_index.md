---
status: draft
maps_to: "openhands/memory/"
lang: en
---

# memory/ — Index

## Overview

The `memory/` module manages conversation context for agents. As conversations grow beyond LLM context windows, the Memory module uses Condenser strategies to compress older events into summaries while preserving the most relevant context. This is critical for long-running agent sessions.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| memory | `openhands/memory/memory.py` | Main Memory class managing conversation context |
| conversation_memory | `openhands/memory/conversation_memory.py` | Conversation-level memory management |
| condenser | `openhands/memory/condenser/` | Strategies for compressing conversation history |
| view | `openhands/memory/view.py` | Memory view/query interface |

## Module Relationships

- **memory** is the main interface used by the agent controller
- **condenser** implements various compression strategies (summarization, truncation, etc.)
- Memory reads from the **event stream** and provides condensed context back to agents
