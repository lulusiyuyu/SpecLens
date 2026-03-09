---
status: draft
maps_to: "plugins/"
lang: en
---

# plugins/ — Index

## Overview

The `plugins/` directory contains all official claude-code plugins. Each plugin is a self-contained directory with a README, and optionally `agents/`, `commands/`, `skills/`, and hooks configuration. Plugins are declarative — defined in Markdown and JSON — and extend claude-code's capabilities without writing runtime code.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| code-review | `plugins/code-review/` | Automated PR review with 5 parallel specialized agents |
| feature-dev | `plugins/feature-dev/` | 7-phase feature development workflow with explorer, architect, and reviewer agents |
| plugin-dev | `plugins/plugin-dev/` | Comprehensive toolkit for developing new claude-code plugins |
| commit-commands | `plugins/commit-commands/` | Git workflow automation: commit, push, and create PRs |
| security-guidance | `plugins/security-guidance/` | PreToolUse hook monitoring 9 security patterns |
| hookify | `plugins/hookify/` | Create custom hooks to prevent unwanted behaviors |
| frontend-design | `plugins/frontend-design/` | Auto-invoked skill for production-grade frontend design |
| pr-review-toolkit | `plugins/pr-review-toolkit/` | 6 specialized PR review agents (comments, tests, errors, types, code, simplify) |
| agent-sdk-dev | `plugins/agent-sdk-dev/` | Development kit for Claude Agent SDK applications |
| claude-opus-4-5-migration | `plugins/claude-opus-4-5-migration/` | Migration tool from Sonnet/Opus 4.x to Opus 4.5 |
| explanatory-output-style | `plugins/explanatory-output-style/` | Educational insights about implementation choices |
| learning-output-style | `plugins/learning-output-style/` | Interactive learning mode with user code contributions |
| ralph-wiggum | `plugins/ralph-wiggum/` | Self-referential AI loops for iterative development |

## Module Relationships

- All plugins are independent and can be installed/used separately
- `plugin-dev` is a meta-plugin for creating other plugins
- `code-review` and `pr-review-toolkit` serve similar but complementary purposes
- `hookify` enables creation of custom hooks similar to `security-guidance`
- Plugins can reference each other but are not interdependent
