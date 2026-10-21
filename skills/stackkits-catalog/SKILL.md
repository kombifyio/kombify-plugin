---
name: stackkits-catalog
description: Use when browsing or evaluating StackKits definitions, kits, and catalog facts through the selected local StackKits connector.
---

# Browse the StackKits catalog

StackKits owns its CUE catalog and the `stackkit` MCP contract: ask the local connector for the current catalog, never infer kits from this skill. Call `tools/list` and use only returned names. Read-only catalog and docs tools (`docs`/`local`/`server` modes): `stackkit_docs_search`, `stackkit_api_overview`, `stackkit_api_endpoint`, `stackkit_get_openapi_spec`, `stackkit_config_get`, `stackkit_status`, `stackkit_validate_spec`, `stackkit_generate_preview`.

- List definitions with these tools before recommending one; report the returned version, definition identity and evidence.
- Never call write tools (`stackkit_init`, `stackkit_apply`, `stackkit_remove`, `stackkit_upgrade`, `stackkit_backup`, `stackkit_restore`, `stackkit_resolve`, `stackkit_generate`, `stackkit_config_set`); they belong to `$stackkits-operations` after explicit owner approval.
- Without the local connector, explain that `stackkit-mcp` or the StackKits-generated client configuration is required.
