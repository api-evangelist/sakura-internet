---
name: sakura-internet-deploy-an-apprun-application
description: Deploy a container to AppRun (shared) and shift traffic between versions
api: openapi/sakura-internet-apprun-shared-openapi.yml
operations:
- createApplication
- readApplicationStatus
- listApplicationVersions
- updateApplicationTraffic
---

# Deploy a container to AppRun (shared) and shift traffic between versions

API: AppRun共用型 APIドキュメント — base URL `https://secure.sakura.ad.jp/cloud/api/apprun/1.0/apprun/api`.

## Steps

1. `createApplication` — `POST /applications`. Create the application from a container image.
2. `readApplicationStatus` — `GET /applications/{id}/status`. Poll until the application is healthy.
3. `listApplicationVersions` — `GET /applications/{id}/versions`. List versions created by each change.
4. `updateApplicationTraffic` — `PUT /applications/{id}/traffics`. Split or move traffic between versions.

## Rules

- Auth: SAKURA Cloud API key as HTTP Basic — the spec declares no scheme; see overlays/sakura-internet-apprun-shared-overlay.yaml.
- No idempotency key is documented in the spec: do not blindly retry create/send calls after a timeout — read state first.
- Use the request/response schemas in `openapi/sakura-internet-apprun-shared-openapi.yml` as the source of truth; the overlay in `overlays/sakura-internet-apprun-shared-overlay.yaml` lists our enhancements.
