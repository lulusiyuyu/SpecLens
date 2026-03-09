---
status: skeleton
maps_to: "internal/llm/agent/"
last_expanded: ""
dependencies:
  - internal/llm/provider.md
  - internal/llm/tools.md
spec_type: feature
lang: en
---

# LLM Agent

## One-line Summary

The agent loop that orchestrates the cycle of sending messages to an LLM provider, parsing tool calls from responses, executing tools, and feeding results back until the task is complete.
