---
name: knowledge-usage
description: Use when answering questions about Kombify products, concepts, or documented procedures through the knowledge tools of the kombify connector.
---

# Use Kombify Knowledge

Knowledge search is the knowledge bundle on the `kombify` connector (`https://api.kombify.io/mcp`), read-only, with client OAuth. It is separate from the anonymous HTTP knowledge route, which only retrieves public documentation.

## Discipline

1. Discover the tools your account can call with `tools/list` (for example `knowledge_search_knowledge`, `knowledge_get_source`, `knowledge_search_code`, `knowledge_get_freshness`).
2. Search before answering a platform question; never fill gaps from memory.
3. Pass source identifiers and freshness evidence on to the user.
4. Keep tenant and entitlement boundaries: a denied or empty result is no reason to retry with another identity or infer protected data.
5. Read operations only; changes, publishing and review belong to the owning product workflow.

## Search to source

Pass a search result's `sourceId` unchanged to `knowledge_get_source`:

```json
{
  "name": "knowledge_get_source",
  "arguments": {
    "sourceId": "<knowledge_search_knowledge result.sourceId>"
  }
}
```

Never substitute the chunk `id`, `sourceUri` or an invented reference. Use `knowledge_get_freshness` to report how current the indexed source is.

Relay structured denials and not-found reasons as returned, without retrying by chunk ID or another identity. Missing OAuth yields an authentication challenge; entitlement, tenant, freshness or provider policy blocks come with a structured reason and guidance to relay.
