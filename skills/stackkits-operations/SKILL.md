---
name: stackkits-operations
description: "Use when operating a local StackKits installation through its MCP tools: install, validate, plan, apply, verify, status, or safe recovery."
---

# Operate StackKits safely

StackKits is the product authority for local definitions, generated artifacts,
runtime state, and evidence. The `stackkit` MCP exposes the same contract as
the CLI; the plugin does not implement or simulate StackKits operations.

## Normal sequence

For a new or changed installation, follow the product's boundary:

1. inspect the current status and workspace;
2. validate the desired StackSpec;
3. generate and inspect a plan;
4. ask for explicit owner approval before any write or destructive action;
5. apply the approved plan;
6. verify and report the resulting evidence.

Use the MCP tool's returned plan hash, generation receipt, and verification
result. Never claim success from a requested call alone.

## Safety

- Do not replace an existing StackSpec without the expected-spec hash.
- Do not invent inventory, provider identity, credentials, or server state.
- If a write tool is unavailable, disabled, or denied, stop and relay the
  structured guidance. Never bypass the product gate with a shell command.
- Keep local credentials in the product's supported custody mechanism; this
  plugin ships none.
