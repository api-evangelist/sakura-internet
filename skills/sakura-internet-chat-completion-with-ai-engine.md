---
name: sakura-internet-chat-completion-with-ai-engine
description: Generate a chat completion or embeddings with SAKURA AI Engine
api: openapi/sakura-internet-ai-engine-inference-openapi.yml
operations:
- createChatCompletion
- createEmbeddings
---

# Generate a chat completion or embeddings with SAKURA AI Engine

API: さくらの AI Engine Inference API — base URL `https://api.ai.sakura.ad.jp`.

## Steps

1. `createChatCompletion` — `POST /v1/chat/completions`. Send the model id and `messages` array to get a completion (OpenAI-compatible shape).
2. `createEmbeddings` — `POST /v1/embeddings`. Embed text for retrieval when building search over your own content.

## Rules

- Auth: Bearer token (`BearerAuth`) in the Authorization header.
- No idempotency key is documented in the spec: do not blindly retry create/send calls after a timeout — read state first.
- Use the request/response schemas in `openapi/sakura-internet-ai-engine-inference-openapi.yml` as the source of truth; the overlay in `overlays/sakura-internet-ai-engine-inference-overlay.yaml` lists our enhancements.
