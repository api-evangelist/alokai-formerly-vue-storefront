---
name: Invalidate Alokai Cloud CDN cache
description: Invalidate a cached URI on an Alokai Cloud instance's CDN, or flush an instance's cache entirely.
api: openapi/alokai-formerly-vue-storefront-cloud-openapi.json
operations:
- "DELETE /cdn_cache/{instance}/path/{path}"
- "DELETE /cdn_cache/{instance}/host/{host}/path/{path}"
- "DELETE /flush_cache/{project}"
---

# Invalidate Alokai Cloud CDN cache

Operating instructions for an agent using the Alokai Cloud ("farmer") API
(`https://farmer.vuestorefront.cloud`).

## Auth
Send both headers on every request (see `authentication/`):
- `X-Api-Key: <api key>`
- `X-User-Id: <user id>`

## Steps
1. **Invalidate a single path** — `DELETE /cdn_cache/{instance}/path/{path}` to purge one URI from the instance CDN.
2. **Scope to a host** (multi-domain instances) — `DELETE /cdn_cache/{instance}/host/{host}/path/{path}` to purge the URI on a specific host.
3. **Flush everything** (last resort) — `DELETE /flush_cache/{project}` to flush the whole instance cache.

## Conventions & errors
- Errors return plain `application/json`; a `500` indicates an error occurred during invalidation. See `errors/alokai-formerly-vue-storefront-problem-types.yml`.
- These are destructive cache operations — confirm `instance`/`project` before flushing.
