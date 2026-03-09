---
status: draft
maps_to: "openhands/storage/"
lang: en
---

# storage/ — Index

## Overview

The `storage/` module provides pluggable file storage backends for persisting events, session data, and artifacts. It defines an abstract interface implemented by local filesystem, Amazon S3, and Google Cloud Storage backends. This allows OpenHands to run locally (file-based) or in cloud deployments without code changes.

## Modules

| Module | Source Path | One-line Description |
|--------|-----------|---------------------|
| files | `openhands/storage/files.py` | Abstract FileStore interface |
| local | `openhands/storage/local.py` | Local filesystem storage backend |
| s3 | `openhands/storage/s3.py` | Amazon S3 storage backend |
| google_cloud | `openhands/storage/google_cloud.py` | Google Cloud Storage backend |
| memory | `openhands/storage/memory.py` | In-memory storage (for testing) |
| locations | `openhands/storage/locations.py` | Standard storage path conventions |
| web_hook | `openhands/storage/web_hook.py` | Webhook notification on storage events |
| batched_web_hook | `openhands/storage/batched_web_hook.py` | Batched webhook notifications |

## Module Relationships

- **files** defines the abstract `FileStore` interface
- **local**, **s3**, **google_cloud**, and **memory** implement `FileStore`
- **locations** standardizes path naming conventions
- Storage is consumed by **events** (event persistence), **server** (session data), and **memory**
