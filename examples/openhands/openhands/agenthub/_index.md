---
status: draft
maps_to: "openhands/agenthub/"
lang: en
---

# agenthub/ — Index

## Overview

The `agenthub/` directory contains all agent implementations. Each agent is a subdirectory with its own logic for processing tasks. Agents implement a common `Agent` interface and are registered via the hub pattern. The primary agent is CodeAct, which uses code actions (function calls) for tool use.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| codeact_agent | `openhands/agenthub/codeact_agent/` | Primary agent using code/function-call actions for tasks |
| browsing_agent | `openhands/agenthub/browsing_agent/` | Agent specialized in web browsing and information retrieval |
| dummy_agent | `openhands/agenthub/dummy_agent/` | Minimal agent for testing and development |
| readonly_agent | `openhands/agenthub/readonly_agent/` | Agent that can only read, not modify |
| loc_agent | `openhands/agenthub/loc_agent/` | Location/code-search focused agent |
| visualbrowsing_agent | `openhands/agenthub/visualbrowsing_agent/` | Visual browsing agent with screenshot capabilities |

## Module Relationships

- All agents implement the base `Agent` class from `controller/agent.py`
- Agents are registered and discovered via `agenthub/__init__.py`
- **codeact_agent** is the default and most capable agent
- All agents use the **llm** module for AI inference and **events** for communication
