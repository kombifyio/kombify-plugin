---
name: getting-started
description: Use when setting up the kombify plugin, connecting an agent to kombify Cloud, completing the kombify sign-in, choosing what the agent may do, reading a file on an equipped device, or diagnosing a kombify tool that is missing, unavailable or denied.
---

# Getting started with kombify

The plugin ships two connectors. Each is enabled and signed in on its own:

| Connector | Endpoint | What it reaches |
| --- | --- | --- |
| `kombify` | `https://api.kombify.io/mcp` | The one door to kombify Cloud through the kombify Gateway: homelab servers, Cloud account, Paperwork, Wallet references, Supply Dock, agent inbox and kombify knowledge. Which tools appear depends on the signed-in account and what its owner equipped. |
| `stackkit` | local process `stackkit-mcp` | A StackKits installation on this machine. Enabled once `stackkit-mcp` is installed. |

Installing the plugin signs in nothing, starts nothing on a server and grants nothing.

## Connect to kombify Cloud

1. Let the client run the sign-in for `kombify` (in Claude Code: `/mcp`, select `kombify`, authenticate). The person signs in with their kombify account in the browser; never ask for a password, token or authorization header in chat or in a tool argument.
2. Run the `connect` skill (`/kombify:connect`) to confirm who the agent acts as and what it can reach.
3. If tools the person expects are missing, explain where they are switched on: in the kombify app, the owner equips this agent host under **External agents** (which definitions it may use, for example homelab inventory, Paperwork mail read or Supply Dock read) and switches the client on. The agent cannot equip itself.

## What the agent can and cannot do

- A freshly connected host gets the owner's External agents template: agent identity and inbox, owner notes, web search and a browser, plus the public read-only tools. More appears only after the owner equips it (`supply-dock` explains the template).
- Changes that leave the account, cost money or destroy data wait for the owner: the first call answers `external_agent_owner_confirmation_pending` with a `decision_id`, the owner decides in the kombify Companion inbox, and the same call with the same `idempotency_key` then runs once.
- No tool reveals a secret value; secrets are passed as Wallet item ids.
- Tools that change what agents may do (grant, share, reveal) are refused for outside agents (`external_agent_self_elevation_denied`, `external_agent_secret_reveal_denied`). Relay that the person does it in the kombify app.

Tool names appear in host-safe form: dots become underscores (`techstack.list_servers` is listed as `techstack_list_servers`). Skills write the dotted name; call the listed one.

## Diagnose from the tools

Read [connector discovery and connection custody](references/connector-discovery.md) to pick a connector or explain a missing connection (in hosts that cannot open files, read `./references/connector-discovery.md` through the host's skill-file reader).

Call `tools/list` before claiming availability. A structured denial is an answer: relay its reason and guidance, do not retry blindly. Knowledge comes from the knowledge tools (`knowledge-usage`), servers from the homelab tools (`homelab-operations`, `techstack-inventory`), agent identity and inbox from the agent tools (`cloud-agents`), local StackKits state from StackKits tools; never from this document or memory.

## Files on an equipped device

When the run offers `device_files_read`, read [the device file-read guide](references/device-file-read.md) (reader path `./references/device-file-read.md`). The tool uses the run's selected device and current Files permission; installation assigns no device and grants no access. If the tool is absent, explain the missing device assignment or permission with the product's guidance. The tool's result is the evidence of the read.
