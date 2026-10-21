---
name: knowledge-usage
description: Use when answering questions about Kombify products, concepts, or documented procedures through the authenticated read-only Knowledge MCP.
---

# Use Kombify Knowledge

Authenticated, read-only MCP at `https://api.kombify.io/v1/mcp/knowledge`; separate from the anonymous HTTP knowledge route, which only retrieves public documentation.

## Discipline

1. Discover tools with `tools/list`.
2. Search before answering a platform question; never fill gaps from memory.
3. Pass source identifiers and freshness/index evidence on to the user.
4. Keep tenant and entitlement boundaries: a denied or empty result is no reason to retry with another identity or infer protected data.
5. Read operations only; changes, publishing and review belong to the owning product workflow.

## Search to source

Pass a `search_knowledge` result's `sourceId` unchanged to `get_source`:

```json
{
  "name": "get_source",
  "arguments": {
    "sourceId": "<search_knowledge result.sourceId>"
  }
}
```

Never substitute the chunk `id`, `sourceUri` or an invented reference; `ref` is only a deprecated alias for older clients.

Both tools default to the public product corpus. A `search_knowledge` call with `"audience": "internal"` needs the same audience on `get_source`; internal search and reads need the developer knowledge tier. Relay structured denials and not-found reasons as returned, without retrying by chunk ID or another identity. Missing OAuth yields an authentication challenge; entitlement, tenant, freshness or provider policy blocks come with a structured reason and guidance to relay.
