---
name: knowledge-usage
description: Use when answering questions about Kombify products, concepts, or documented procedures through the authenticated read-only Knowledge MCP.
---

# Use Kombify Knowledge

The Knowledge connector is the authenticated, read-only MCP surface at
`https://api.kombify.io/v1/mcp/knowledge`. It is separate from the anonymous
HTTP knowledge route, which remains limited to public documentation retrieval.

## Retrieval discipline

1. Discover the available tools with `tools/list`.
2. Search before answering a platform question; do not fill gaps from memory.
3. Pass source identifiers and freshness/index evidence through to the user.
4. Keep tenant and entitlement boundaries intact. A denied or empty result is
   not permission to retry with another identity or to infer protected data.
5. Use only read operations. Changes, publishing, or review belong to the
   product workflow that owns them.

If OAuth is missing, expect an authentication challenge. If entitlement,
tenant, freshness, or provider policy blocks a result, relay the structured
reason and its user guidance.
