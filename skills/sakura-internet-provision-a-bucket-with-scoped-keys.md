---
name: sakura-internet-provision-a-bucket-with-scoped-keys
description: Create an Object Storage bucket and issue a bucket-scoped access key
api: openapi/sakura-internet-objectstorage-openapi.yml
operations:
- listClusters
- createBucket
- createPermission
- createPermissionKey
---

# Create an Object Storage bucket and issue a bucket-scoped access key

API: さくらのオブジェクトストレージ APIドキュメント — base URL `https://secure.sakura.ad.jp/cloud/zone/is1a/api/objectstorage/1.0/isk01/v2`.

## Steps

1. `listClusters` — `GET /clusters`. Pick the site (cluster) — each site has its own server URL.
2. `createBucket` — `PUT /buckets/{name}`. Create the bucket.
3. `createPermission` — `POST /permissions`. Create a permission granting access to the bucket.
4. `createPermissionKey` — `POST /permissions/{id}/keys`. Issue an access key for that permission (the secret is shown once).

## Rules

- Auth: HTTP Basic (`BasicAuth`) with a SAKURA Cloud API key.
- No idempotency key is documented in the spec: do not blindly retry create/send calls after a timeout — read state first.
- Use the request/response schemas in `openapi/sakura-internet-objectstorage-openapi.yml` as the source of truth; the overlay in `overlays/sakura-internet-objectstorage-overlay.yaml` lists our enhancements.
