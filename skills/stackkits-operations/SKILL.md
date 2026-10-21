---
name: stackkits-operations
description: "Use when operating a local StackKits installation through its MCP tools: validate, plan, apply, verify, status, or safe recovery."
---

# Operate StackKits safely

StackKits is the authority for local definitions, generated artifacts, runtime state and evidence; the `stackkit` MCP exposes the CLI's contract and the plugin simulates nothing. Call `tools/list` first: write tools register only with `STACKKIT_MCP_ALLOW_WRITE=true` (or `stackkit-server --mcp-allow-write`).

## Sequence

1. Inspect: `stackkit_status`, `stackkit_self_check_plan`.
2. Validate: `stackkit_validate` or `stackkit_validate_spec`.
3. Plan: `stackkit_plan` or `stackkit_generate_preview`.
4. Get explicit owner approval before any write or destructive action.
5. Apply the approved plan: `stackkit_apply` (write mode).
6. Verify: `stackkit_verify`; report evidence from `structuredContent`.

Use the returned plan hash, generation receipt and verification result; a requested call alone is not success. Other write tools when listed: `stackkit_init`, `stackkit_resolve`, `stackkit_generate`, `stackkit_config_set`, `stackkit_backup`, `stackkit_restore`, `stackkit_upgrade`, `stackkit_remove` (needs one exact `workload_ref`).

## Safety

- Replace an existing StackSpec only with `expected_spec_hash`.
- Invent no inventory, provider identity, credentials or server state.
- A write tool that is unavailable, disabled or denied stops the work: relay the structured guidance (`stackkit.actionable-error/v1` when present); never bypass the gate with a shell command.
- Local credentials stay in the product's custody mechanism; this plugin ships none.
