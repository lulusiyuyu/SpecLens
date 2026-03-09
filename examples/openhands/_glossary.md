---
status: draft
lang: en
---

# OpenHands — Glossary

## Terms

| Term | Definition | Also Known As |
|------|-----------|---------------|
| Agent | An AI entity that can plan and execute software engineering tasks autonomously | — |
| AgentHub | The registry/collection of all available agent implementations | Agent registry |
| CodeAct Agent | The primary agent that can write and execute code via function calls | — |
| Browsing Agent | An agent specialized in web browsing tasks | — |
| Action | A command the agent wants to execute (e.g., run shell command, edit file) | — |
| Observation | The result/output of an executed action | — |
| Event | A recorded action or observation in the event stream | — |
| Event Stream | The append-only log of all events in a conversation | Event log |
| Runtime | The sandboxed execution environment (Docker container) where agent actions run | Sandbox |
| Controller | The orchestrator that manages agent lifecycle and execution loop | AgentController |
| State | The current status of an agent session (running, paused, completed, etc.) | Agent state |
| Stuck Detection | Logic that detects when an agent is repeating actions without progress | — |
| Condenser | A strategy for compressing conversation history to fit within LLM context limits | Memory compressor |
| Memory | The module managing conversation context and history compression | Context memory |
| LiteLLM | An open-source library providing a unified interface to multiple LLM providers | — |
| MCP | Model Context Protocol — a standard for connecting AI models to external tools | — |
| Resolver | Automated system for resolving GitHub issues and PRs | Issue resolver |
| Session | A user's interaction session with the server | — |
| Conversation | A single agent task execution within a session | Thread |
| Microagent | Small, specialized agent prompts for specific tasks | — |

## Abbreviations

| Abbreviation | Full Form |
|-------------|-----------|
| LLM | Large Language Model |
| MCP | Model Context Protocol |
| GCS | Google Cloud Storage |
| API | Application Programming Interface |
| CLI | Command Line Interface |
| GUI | Graphical User Interface |
| WS | WebSocket |
| PR | Pull Request |
