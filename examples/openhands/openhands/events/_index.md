---
status: draft
maps_to: "openhands/events/"
lang: en
---

# events/ — Index

## Overview

The `events/` module implements the event-sourced communication backbone of OpenHands. All agent actions and observations are recorded as events in an append-only stream. This module defines the event types (actions and observations), the event stream, event serialization, filtering, and storage.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| event | `openhands/events/event.py` | Base Event class and common event types |
| stream | `openhands/events/stream.py` | EventStream — append-only event log |
| event_store | `openhands/events/event_store.py` | Persistent event storage |
| event_store_abc | `openhands/events/event_store_abc.py` | Abstract base for event stores |
| action | `openhands/events/action/` | Action event types (shell, file, browse, etc.) |
| observation | `openhands/events/observation/` | Observation event types (command output, file content, etc.) |
| serialization | `openhands/events/serialization/` | Event serialization/deserialization |
| event_filter | `openhands/events/event_filter.py` | Filtering events by type or criteria |
| tool | `openhands/events/tool.py` | Tool-related event utilities |

## Module Relationships

- **event** is the base type extended by all actions and observations
- **stream** is the central event bus consumed by controller, memory, and storage
- **action/** and **observation/** define the vocabulary of agent interactions
- **serialization** enables persistence and transmission of events
- **event_store** persists events using **storage** backends
