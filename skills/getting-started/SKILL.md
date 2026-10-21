---
name: getting-started
description: Use when setting up the public Kombify plugin, selecting a connector, reading a file on an equipped device, completing OAuth, or diagnosing access that is unavailable or denied.
---

# Getting started with Kombify

Independently selectable connectors:

| Connector | Endpoint | Notes |
| --- | --- | --- |
| `kombify` | `https://api.kombify.io/mcp` | Central customer MCP; client OAuth; exposes the tools permitted for the signed-in account |
| `kombify-knowledge` | `https://api.kombify.io/v1/mcp/knowledge` | Read-only, cloud-hosted; client OAuth and Kombify entitlement policy |
| `kombify-openwiki` | `https://api.kombify.io/v1/mcp/openwiki` | Read-only OpenWiki search, source reading and freshness evidence from the governed SHA-bound corpus; no MCP App or UI state |
| `kombify-paperwork` | `https://paperwork.kombify.io/mcp` | Paperwork owns its tools and tenant boundary; client OAuth; never takes credentials in tool arguments |
| `stackkit` | local process | From the StackKits product; enabled once `stackkit-mcp` is installed or the generator wrote a local configuration |

Installing the plugin signs in, starts and grants nothing; a client enables each connector independently.

## Setup

1. Select only the connectors the user intends to use.
2. Let the client do OAuth for cloud connectors; never request or store credentials in a skill or tool argument.
3. StackKits: run the product's installation/self-check first; the standard local command is `stackkit-mcp --mode docs,local,server`.
4. A missing connector is disabled alone; report the installation or authentication step that restores it.

## Diagnose from the tools

Read [connector discovery and connection custody](references/connector-discovery.md) to pick a connector or explain a missing connection (hosted agents: the bundled skill-file reader with this skill's ID and `./references/connector-discovery.md`).

Call `tools/list` before claiming availability. A structured denial is an answer: relay its reason and guidance, do not retry blindly. Knowledge and OpenWiki data come from their read-only tools, Paperwork state from Paperwork tools, local StackKits state from StackKits tools, never from this document or memory. Once `kombify-knowledge` is available, `knowledge-usage` holds the search-to-source contract and denial handling.

## Files on an equipped device

When the run offers `device_files_read`, read [the device file-read guide](references/device-file-read.md) (reader path `./references/device-file-read.md`). The tool uses the run's selected device and current Files permission; installation assigns no device and grants no access. If the tool is absent, explain the missing device assignment or permission with the product's guidance. The tool's result is the evidence of the read.
