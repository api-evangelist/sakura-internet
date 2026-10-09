---
name: sakura-internet-send-a-notification
description: Send a message through a SAKURA Simple Notification destination group
  and check delivery
api: openapi/sakura-internet-simple-notification-openapi.yml
operations:
- listCommonServiceItems
- sendNotification
- listNotificationHistories
- readNotificationHistory
---

# Send a message through a SAKURA Simple Notification destination group and check delivery

API: シンプル通知 API — base URL `https://secure.sakura.ad.jp/cloud/zone/is1a/api/cloud/1.1`.

## Steps

1. `listCommonServiceItems` — `GET /commonserviceitem`. Find the notification group (common service item) to send through.
2. `sendNotification` — `POST /commonserviceitem/{id}/simplenotification/message`. Send the message to that group.
3. `listNotificationHistories` — `GET /commonserviceitem/simplenotification/history`. List send history and find the request.
4. `readNotificationHistory` — `GET /commonserviceitem/simplenotification/history/{request_id}`. Read the delivery result for one request.

## Rules

- Auth: SAKURA Cloud API key (access token / secret) as HTTP Basic — the spec declares no scheme; see overlays/sakura-internet-simple-notification-overlay.yaml.
- No idempotency key is documented in the spec: do not blindly retry create/send calls after a timeout — read state first.
- Use the request/response schemas in `openapi/sakura-internet-simple-notification-openapi.yml` as the source of truth; the overlay in `overlays/sakura-internet-simple-notification-overlay.yaml` lists our enhancements.
