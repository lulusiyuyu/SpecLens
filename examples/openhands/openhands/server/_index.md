---
status: draft
maps_to: "openhands/server/"
lang: en
---

# server/ — Index

## Overview

The `server/` module contains the FastAPI web application that serves the OpenHands GUI. It provides REST API routes, WebSocket (Socket.IO) for real-time agent communication, session and conversation management, authentication middleware, and static file serving for the React frontend.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| app | `openhands/server/app.py` | FastAPI application setup and configuration |
| listen | `openhands/server/listen.py` | HTTP request handlers and Socket.IO event listeners |
| routes | `openhands/server/routes/` | REST API route definitions |
| middleware | `openhands/server/middleware.py` | Request/response middleware (auth, CORS, etc.) |
| session | `openhands/server/session/` | Session management |
| conversation_manager | `openhands/server/conversation_manager/` | Conversation lifecycle management |
| dependencies | `openhands/server/dependencies.py` | FastAPI dependency injection |
| user_auth | `openhands/server/user_auth/` | User authentication and authorization |
| services | `openhands/server/services/` | Backend services |
| data_models | `openhands/server/data_models/` | API request/response data models |
| settings | `openhands/server/settings.py` | Server configuration settings |

## Module Relationships

- **app** is the FastAPI entry point that mounts all routes and middleware
- **listen** handles WebSocket events for real-time agent interaction
- **conversation_manager** creates and manages agent conversations
- **session** tracks user sessions and authentication state
- Server delegates to **controller** for actual agent execution
