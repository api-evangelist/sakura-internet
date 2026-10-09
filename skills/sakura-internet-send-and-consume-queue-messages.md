---
name: sakura-internet-send-and-consume-queue-messages
description: Send, receive, extend and acknowledge messages on a SAKURA Simple MQ
  queue
api: openapi/sakura-internet-simplemq-openapi.yml
operations:
- sendMessage
- receiveMessage
- extendMessageTimeout
- deleteMessage
---

# Send, receive, extend and acknowledge messages on a SAKURA Simple MQ queue

API: シンプルMQ API — base URL `https://simplemq.tk1b.api.sacloud.jp`.

## Steps

1. `sendMessage` — `POST /v1/queues/{queueName}/messages`. Post a message to the queue.
2. `receiveMessage` — `GET /v1/queues/{queueName}/messages`. Receive messages; each is hidden until its visibility timeout ends.
3. `extendMessageTimeout` — `PUT /v1/queues/{queueName}/messages/{messageId}`. Extend the timeout while still processing.
4. `deleteMessage` — `DELETE /v1/queues/{queueName}/messages/{messageId}`. Delete the message once processed — undeleted messages are redelivered.

## Rules

- Auth: Queue API key as a Bearer token (`ApiKeyAuth`).
- No idempotency key is documented in the spec: do not blindly retry create/send calls after a timeout — read state first.
- Use the request/response schemas in `openapi/sakura-internet-simplemq-openapi.yml` as the source of truth; the overlay in `overlays/sakura-internet-simplemq-overlay.yaml` lists our enhancements.
