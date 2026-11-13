---
name: gateway-api
description: Use when calling kombify tools or the kombify REST API through the kombify Gateway, choosing between a kombify MCP tool and the kombify REST API, handling a Gateway error, rate limit (429), audience mismatch or structured refusal, or writing a retry-safe change with an idempotency key.
---

# Reach kombify APIs through the Gateway

Every kombify product (Cloud, Techstack, Paperwork, AI, Wallet, Supply Dock, kombify Me) sits behind the kombify Gateway at `api.kombify.io`. For an agent the Gateway's door is the MCP endpoint `https://api.kombify.io/mcp`, the `kombify` connector: each tool there is the agent's face of one product API route, with the same checks the kombify apps go through (account, plan, permission, quota).

## Choose the path

| Need | Use |
| --- | --- |
| Read or change something in the person's kombify account | The matching `kombify` MCP tool. Discover it with `tools/list`; do not construct HTTP calls to kombify on the person's behalf. |
| A product area has no listed tool | Explain that the owner equips it under External agents in the kombify app, or that the action is app-only. |
| The person writes their own script or integration against the REST API | It needs a token for `https://api.kombify.io` from the person's own kombify sign-in. The connector's sign-in is bound to `/mcp` and is refused on REST routes with `audience_mismatch`. Point them to the kombify documentation (`https://docs.kombify.io`) for how to sign in their script. Never extract, copy or ask for tokens or keys. |
| Public status | `https://api.kombify.io/gateway/health` needs no sign-in. |

## Tool families

`techstack.*` homelab servers and stacks; `paperwork.*` mail, documents, lists; `cloud.*` account, domains, households, notifications, privacy requests; `wallet.*` secret references (never values); `supplydock.*` connectors and activations; `kombifyme.*` access to the person's kombify Me services; `speechkit.*` voice devices and preferences; `knowledge.*` documentation; `agent.*` the agent's own identity and inbox. `tools/list` decides what exists for this account; this list does not.

## Calling discipline

- **Arguments.** Use only parameters the tool's schema declares, and ids returned by an earlier result. Never invent an id, revision or parameter.
- **Idempotency.** Pass an `idempotency_key` (a fresh unique string per intended change) wherever the schema offers one. Reuse the same key only to repeat the same call after an owner decision or a lost answer.
- **Revisions.** A tool that takes `expected_inventory_revision`, `expected_etag` or a settings revision refuses when the state changed since the read. Read again and decide again; never force.
- **Rate limits.** A 429 carries `Retry-After` (seconds) and a body with `source: "gateway_throttle"` and `retry_after_ms`. Wait that long once, then retry; do not loop.
- **Refusals are answers.** `mcp_tool_not_public` (the tool is app-only for outside agents), `external_agent_denied` (the owner switched the client off or the profile is suspended), `external_agent_one_shot_required` and `external_agent_owner_confirmation_pending` (an owner decision is needed, see `cloud-agents`), missing entitlement or plan: relay the reason and its guidance. Retry unchanged only for a `503` marked retryable, such as `external_agent_authority_unavailable`, and only once after a short wait.
- **Results.** A queued change is not done. Read back the job, action card or new state before reporting success.

## Custom queries

`techstack.instant_monitor_query` runs one PromQL instant query against the metrics kombify collects from the person's server. Quote the single value it returns with its timestamp; do not paste raw series.

Answer in the person's language; report what ran, its evidence and anything refused.
