---
status: draft
maps_to: "openhands/runtime/"
lang: en
---

# runtime/ — Index

## Overview

The `runtime/` module provides sandboxed execution environments where agent actions are safely executed. The primary implementation uses Docker containers to isolate code execution, file operations, and shell commands. It includes an action execution server that runs inside the container and communicates with the host.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| base | `openhands/runtime/base.py` | Abstract base Runtime class defining the execution interface |
| action_execution_server | `openhands/runtime/action_execution_server.py` | Server running inside Docker handling action execution |
| file_viewer_server | `openhands/runtime/file_viewer_server.py` | File viewing service in the runtime |
| runtime_status | `openhands/runtime/runtime_status.py` | Runtime lifecycle status tracking |

## Module Relationships

- **base** defines the interface implemented by Docker and other runtime backends
- **action_execution_server** runs inside the sandbox, receiving actions via HTTP
- Controller communicates with runtime through the base interface
- Runtime uses **storage** for file persistence
