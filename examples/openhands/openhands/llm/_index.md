---
status: draft
maps_to: "openhands/llm/"
lang: en
---

# llm/ — Index

## Overview

The `llm/` module provides a unified abstraction over multiple LLM providers (OpenAI, Anthropic, Google, AWS Bedrock, etc.) via LiteLLM. It handles API calls with retry logic, streaming responses, token metrics tracking, function call format conversion, and model capability detection.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| llm | `openhands/llm/llm.py` | Core LLM class wrapping LiteLLM for synchronous calls |
| async_llm | `openhands/llm/async_llm.py` | Async variant of the LLM interface |
| streaming_llm | `openhands/llm/streaming_llm.py` | Streaming response support |
| retry_mixin | `openhands/llm/retry_mixin.py` | Retry logic with exponential backoff |
| debug_mixin | `openhands/llm/debug_mixin.py` | Debug logging for LLM calls |
| fn_call_converter | `openhands/llm/fn_call_converter.py` | Converts between native and LLM function call formats |
| metrics | `openhands/llm/metrics.py` | Token usage and cost tracking |
| model_features | `openhands/llm/model_features.py` | Model capability detection (vision, function calling, etc.) |
| bedrock | `openhands/llm/bedrock.py` | AWS Bedrock-specific handling |
| llm_registry | `openhands/llm/llm_registry.py` | Registry of available LLM configurations |
| llm_utils | `openhands/llm/llm_utils.py` | Shared LLM utilities |
| tool_names | `openhands/llm/tool_names.py` | Standard tool name definitions |

## Module Relationships

- **llm** is the primary interface consumed by all agents
- **retry_mixin** and **debug_mixin** are mixed into the LLM class
- **fn_call_converter** handles format differences between LLM providers
- **metrics** collects usage data for cost/budget tracking
- **model_features** determines what capabilities a model supports
