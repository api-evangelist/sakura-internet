---
name: sakura-internet-encrypt-data-with-kms
description: Create a KMS key and encrypt/decrypt data with it
api: openapi/sakura-internet-security-encryption-openapi.yml
operations:
- createKey
- readKey
- encryptDataWithKey
- decryptDataWithKey
---

# Create a KMS key and encrypt/decrypt data with it

API: KMS/SecretManager/CloudHSM API — base URL `https://secure.sakura.ad.jp/cloud/zone/is1a/api/cloud/1.1`.

## Steps

1. `createKey` — `POST /kms/keys`. Create a key.
2. `readKey` — `GET /kms/keys/{resource_id}`. Confirm the key exists and is active.
3. `encryptDataWithKey` — `POST /kms/keys/{resource_id}/encrypt`. Encrypt plaintext with the key.
4. `decryptDataWithKey` — `POST /kms/keys/{resource_id}/decrypt`. Decrypt ciphertext with the same key.

## Rules

- Auth: HTTP Basic (`basicAuth`) with a SAKURA Cloud API key.
- No idempotency key is documented in the spec: do not blindly retry create/send calls after a timeout — read state first.
- Use the request/response schemas in `openapi/sakura-internet-security-encryption-openapi.yml` as the source of truth; the overlay in `overlays/sakura-internet-security-encryption-overlay.yaml` lists our enhancements.
