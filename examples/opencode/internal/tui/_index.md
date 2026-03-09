---
status: draft
maps_to: "internal/tui/"
lang: en
---

# tui/ — Index

## Overview

The `tui/` module implements OpenCode's terminal user interface using the Bubble Tea framework (Elm architecture). It contains the main TUI model, page layouts, reusable components (editor, message list, status bar), styling/theming, and utility helpers.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| tui | `internal/tui/tui.go` | Main TUI model and initialization |
| page | `internal/tui/page/` | Page-level views (chat, sessions, etc.) |
| components | `internal/tui/components/` | Reusable UI components (editor, messages, etc.) |
| layout | `internal/tui/layout/` | Layout management and positioning |
| styles | `internal/tui/styles/` | Styling constants and utilities |
| theme | `internal/tui/theme/` | Color themes (catppuccin, etc.) |
| image | `internal/tui/image/` | Image rendering in terminal |
| util | `internal/tui/util/` | TUI utility helpers |

## Module Relationships

- **tui.go** is the root model that delegates to **page** views
- **page** views compose **components** for rendering
- **layout** manages the overall screen structure
- **styles** and **theme** provide consistent visual styling
- Pages interact with services (LLM, session, message) for data
