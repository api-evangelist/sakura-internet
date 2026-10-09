---
name: sakura-internet-answer-questions-over-documents
description: Upload documents to SAKURA AI Engine RAG and ask questions over them
api: openapi/sakura-internet-ai-engine-rag-openapi.yml
operations:
- documents_upload
- documents_retrieve
- documents_query
- documents_chat
---

# Upload documents to SAKURA AI Engine RAG and ask questions over them

API: Sakura AI Engine RAG API — base URL `https://api.ai.sakura.ad.jp`.

## Steps

1. `documents_upload` — `POST /v1/documents/upload/`. Upload a document.
2. `documents_retrieve` — `GET /v1/documents/{id}/`. Read the document back to check it has been processed.
3. `documents_query` — `POST /v1/documents/query/`. Run a semantic query to retrieve matching chunks.
4. `documents_chat` — `POST /v1/documents/chat/`. Ask a question answered from the uploaded documents.

## Rules

- Auth: Bearer token (`BearerAuth`).
- No idempotency key is documented in the spec: do not blindly retry create/send calls after a timeout — read state first.
- Use the request/response schemas in `openapi/sakura-internet-ai-engine-rag-openapi.yml` as the source of truth; the overlay in `overlays/sakura-internet-ai-engine-rag-overlay.yaml` lists our enhancements.
