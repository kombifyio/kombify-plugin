---
name: stackkits-catalog
description: Use when browsing or evaluating StackKits definitions, kits, and catalog facts through the selected local StackKits connector.
---

# Browse the StackKits catalog

StackKits owns its CUE catalog and the `stackkit` MCP contract. Ask the local
connector for the current catalog; do not infer available kits from this skill.

## Rules

- Use read-only catalog tools to list definitions before recommending one.
- Report the returned version, definition identity, and evidence when present.
- Do not turn catalog facts into an apply, install, or provider action. Those
  operations require the StackKits product flow and explicit owner approval.
- If the local connector is not installed, explain that `stackkit-mcp` or the
  StackKits-generated client configuration is required.
