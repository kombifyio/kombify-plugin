---
name: techstack-inventory
description: Inspect a user's assigned Techstack or Homelab servers and services through the governed inventory tools. Use to establish current health, investigate an observed incident and plan the next diagnostic step from actual evidence.
---

# Read a Techstack inventory

Use the instance and resource the user assigned, offered through Kombify's governed customer connector or a qualified product-generated connector for a self-host instance. Discover the tools offered in this run; installing a skill grants no connection or server access. Switch no instance or account to work around a denial.

## Work order

1. Discover inventory tools. The customer surface offers `techstack.list_servers`, `techstack.server_health` and `techstack.list_services`; an instance may use its own names.
2. Establish the target. If server inventory is assigned and needed, call `techstack.list_servers` with the offered `limit`, following `cursor`; use the returned opaque IDs. A lease limited to one server may offer health and services without listing: use its assigned server ID and ask for nothing broader.
3. Read `techstack.server_health` for the `server_id`, then `techstack.list_services` for the same id, following pagination. A server-bound assignment never queries another server or an unbound inventory.
4. Compare health and service state; name evidence, observation time and affected service. Absent or stale freshness means unknown. A reported failure differs from a hypothesis about its cause; inventory does not prove a fix.
5. Give the next diagnostic step, using assigned curated knowledge to interpret products while grounding claims about this installation in its tool results. An installation's own domain or `*.kombify.me` address is its normal access path, local hardware included.

## Authority and outcomes

- These tools need current `techstack.inventory.read`. `server_health` and `list_services` can bind to a `techstack.server`; `list_servers` is unbound. A server binding does not grant every tool in the bundle.
- Not-found means not visible to this identity, not deleted. Follow structured denial guidance (missing connection, entitlement, assignment, expired lease, revocation); never retry an unchanged denial.
- Observation only: no restart, deploy, provision or delete. A repair stays a proposal until an offered tool runs it under its own rights and the new state is verified.
- Unassigning or revoking access ends inventory use; earlier results are history, not proof of current reachability.
- Answer in the user's language and share only the evidence the task needs.
