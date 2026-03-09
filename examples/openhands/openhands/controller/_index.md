---
status: draft
maps_to: "openhands/controller/"
lang: en
---

# controller/ — Index

## Overview

The `controller/` module orchestrates agent execution. The `AgentController` manages the agent lifecycle — starting, stepping, pausing, and stopping agents. It maintains the agent's state, handles action parsing, detects when agents get stuck in loops, and manages replay of previous sessions.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| agent_controller | `openhands/controller/agent_controller.py` | Main controller orchestrating agent step execution |
| agent | `openhands/controller/agent.py` | Base Agent class definition |
| state | `openhands/controller/state/` | Agent state management |
| action_parser | `openhands/controller/action_parser.py` | Parsing LLM responses into Action objects |
| stuck | `openhands/controller/stuck.py` | Detection of stuck/looping agent behavior |
| replay | `openhands/controller/replay.py` | Session replay functionality |

## Module Relationships

- **agent_controller** is the central orchestrator, used by core/loop and server
- **agent** defines the interface that all agenthub agents implement
- **state** tracks execution progress and is checked by stuck detection
- **action_parser** converts raw LLM output into structured Actions
