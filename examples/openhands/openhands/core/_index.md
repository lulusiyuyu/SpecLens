---
status: draft
maps_to: "openhands/core/"
lang: en
---

# core/ — Index

## Overview

The `core/` module contains the fundamental building blocks of OpenHands: the main entry point, the agent execution loop, configuration management, logging, and setup utilities. This is where the application starts and where the primary orchestration logic lives.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| main | `openhands/core/main.py` | CLI entry point and interactive agent session |
| loop | `openhands/core/loop.py` | Core agent execution loop (`run_agent_until_done`) |
| setup | `openhands/core/setup.py` | Initialization and configuration loading |
| logger | `openhands/core/logger.py` | Centralized logging configuration |
| exceptions | `openhands/core/exceptions.py` | Custom exception types |
| message | `openhands/core/message.py` | Message data structures |
| message_utils | `openhands/core/message_utils.py` | Message formatting and conversion utilities |
| download | `openhands/core/download.py` | File/artifact download utilities |

## Module Relationships

- **main** and **loop** are the primary entry points, consumed by CLI and server
- **setup** is called at startup to initialize configuration
- **logger** is used across all modules for consistent logging
- **exceptions** defines error types used throughout the codebase
