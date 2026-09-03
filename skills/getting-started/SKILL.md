---
name: getting-started
description: Use when setting up the public Kombify plugin, selecting its Knowledge, OpenWiki, Paperwork, or StackKits connector, completing OAuth, or diagnosing a connector that is unavailable or denied.
---

# Getting started with Kombify

This plugin offers independently selectable connectors:

- `kombify` is the central customer MCP at `https://api.kombify.io/mcp`.
  It uses the client's OAuth flow and exposes the tools permitted for that
  signed-in account. Discover the available tools before choosing an action.
- `kombify-knowledge` is a read-only, cloud-hosted MCP at
  `https://api.kombify.io/v1/mcp/knowledge`. It uses the client's OAuth flow
  and Kombify entitlement policy.
- `kombify-openwiki` is a focused read-only MCP at
  `https://api.kombify.io/v1/mcp/openwiki`. It exposes only OpenWiki
  search, source reading, and freshness evidence from the governed SHA-bound
  knowledge corpus. It does not expose an MCP App or UI state.
- `kombify-paperwork` is the product-owned Paperwork MCP at
  `https://paperwork.kombify.io/mcp`. Paperwork owns its tools and tenant
  boundary; the connector uses the client's OAuth flow and never accepts
  credentials in tool arguments.
- `stackkit` is a local MCP process supplied by the StackKits product. It is
  enabled only after `stackkit-mcp` is installed or the product's generator
  has written a local configuration.

Installing the plugin does not sign in, start a process, or grant a tool. A
client may enable each connector independently.

## Setup rules

1. Select only the connectors the user intends to use.
2. Let the client perform OAuth for the cloud connectors; never request or
   store credentials in a skill or tool argument.
3. For StackKits, run the product's documented installation/self-check first.
   The standard local command is `stackkit-mcp --mode docs,local,server`.
4. If a connector is missing, disable only that connector and report the
   product installation or authentication step needed to restore it.

## Diagnose from the tools

Call `tools/list` before making claims about availability. A structured denial
is an answer: relay its reason and user guidance instead of retrying blindly.
Knowledge and OpenWiki data must come from their read-only MCP tools, Paperwork
state from Paperwork tools, and local StackKits state from StackKits tools,
never from this document or memory.
