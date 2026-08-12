# kombify-plugin

The official **Kombify plugin** in the vendor-neutral
[Agent Plugins](https://agent-plugins.org/) v1.0.0 format: connect any
compatible AI agent client (Claude, Cursor, the Kombify Workbench, and
others) to the Kombify platform through the public Kombify MCP connector at
`https://api.kombify.io/mcp`, plus curated usage skills for the platform's
capability bundles.

## What you get

- `plugin.json` — Agent Plugins v1.0.0 manifest.
- `mcp.json` — one remote MCP server entry (`streamable-http`,
  `https://api.kombify.io/mcp`, client-managed OAuth; the plugin never
  contains credentials).
- `skills/` — usage skills for the Kombify connector: getting started,
  platform knowledge, TechStack inventory, Paperwork mail and documents,
  StackKits catalog, and account/entitlement reads.

## Releases

This repository is the **release home** of the plugin. Development happens in
the Kombify platform monorepos; every release synced here passes a mandatory
manual artifact review and the Agent Plugins conformance checks (schema
validation, path containment, no secrets, public-safety) before it is
published. The first public release ships with the general availability of
the Kombify MCP connector.

## License

[Apache-2.0](LICENSE) — © Kombiverse Labs.
