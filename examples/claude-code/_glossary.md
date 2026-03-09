---
status: draft
lang: en
---

# claude-code — Glossary

## Terms

| Term | Definition | Also Known As |
|------|-----------|---------------|
| Plugin | An extension package that adds commands, agents, skills, or hooks to claude-code | Extension |
| Command | A user-invocable slash command (e.g., `/code-review`) defined in a plugin | Slash command |
| Agent | A specialized AI persona with focused instructions for a specific task | Sub-agent |
| Skill | An auto-invoked contextual guide that activates based on conversation context | — |
| Hook | A lifecycle event handler that intercepts agent actions (PreToolUse, PostToolUse, SessionStart, Stop) | Interceptor |
| MCP | Model Context Protocol — a standard for connecting AI models to external tools and data sources | — |
| MCP Server | An external server providing tools/context via the MCP protocol | — |
| Tool | A built-in capability (file read/write, bash, search, etc.) the agent can invoke | Function |
| Hookify | A plugin that helps create custom hooks from conversation patterns | — |
| PreToolUse | A hook type that fires before a tool is executed, can warn or block | — |
| PostToolUse | A hook type that fires after a tool is executed | — |
| SessionStart | A hook type that fires when a new conversation session begins | — |

## Abbreviations

| Abbreviation | Full Form |
|-------------|-----------|
| CLI | Command Line Interface |
| MCP | Model Context Protocol |
| PR | Pull Request |
| API | Application Programming Interface |
| npm | Node Package Manager |
| SDK | Software Development Kit |
