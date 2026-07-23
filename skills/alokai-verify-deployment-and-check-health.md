---
name: Verify an Alokai Cloud deployment and check instance health
description: Confirm a tag is deployed to an Alokai Cloud instance, then inspect pods and pod logs to verify health.
api: openapi/alokai-formerly-vue-storefront-cloud-openapi.json
operations:
- "GET /deploy_check/{project}/{tag}"
- "GET /instance/{namespace}/exists"
- "GET /instance/{namespace}/pod"
- "GET /instance/{namespace}/pod/{pod}/log"
---

# Verify an Alokai Cloud deployment and check instance health

Operating instructions for an agent using the Alokai Cloud ("farmer") API
(`https://farmer.vuestorefront.cloud`).

## Auth
Every request sends both headers (see `authentication/`):
- `X-Api-Key: <api key>`
- `X-User-Id: <user id>`

## Steps
1. **Confirm the instance exists** — `GET /instance/{namespace}/exists`. Stop if it does not.
2. **Check the deploy** — `GET /deploy_check/{project}/{tag}` to confirm the target `tag` is deployed for the `project`.
3. **List pods** — `GET /instance/{namespace}/pod` to enumerate the running pods.
4. **Inspect logs** — for any unhealthy pod, `GET /instance/{namespace}/pod/{pod}/log` to fetch its logs.

## Conventions & errors
- Errors are plain `application/json` bodies (not RFC 9457). See `errors/alokai-formerly-vue-storefront-problem-types.yml`.
- `404` on a pod-log call means the pod was not found; `400` means a bad request.
- No pagination on list endpoints; collections return in full.
