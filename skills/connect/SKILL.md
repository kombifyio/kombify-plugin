---
name: connect
description: Check the agent's connection to kombify Cloud and report what it can reach. Use when the person runs /kombify:connect, asks "am I connected to kombify", "what can you do in my homelab", "which kombify tools do I have", or after signing in to the kombify connector.
argument-hint: "[area: homelab | paperwork | agents | knowledge]"
---

# Check the kombify connection

Produce a short connection report from live tool results. Read only; change nothing.

## Steps

1. **Connector.** Check the client's available connection status and current tool list. If the client reports sign-in is needed, use `/mcp` in Claude Code or the client's connector settings to guide sign-in. An empty tool list alone does not establish whether OAuth failed or the signed-in account has no offered rights. Report the observed status and any uncertainty.
2. **Identity.** If `agent.whoami` is listed, call it. Report the agent handle, the owner it acts for and the equipment it holds. If absent, say identity is not offered in this run without inferring the profile or reason.
3. **Reach per area.** Group the listed tools by prefix and report one line per area that is present. Tools are listed in host-safe form (`techstack_list_servers` for `techstack.list_servers`): match the prefixes below with `_` instead of `.` and call the listed name.
   - `techstack.*`: homelab servers. If offered, call `techstack.list_servers` with `limit` 5. Report names and count for that page, not a total unless the result establishes it. Follow the cursor only when needed for the request.
   - `paperwork.*`: Paperwork (mail, documents, lists). Do not read content for this report.
   - `agent.*`: agent identity, inbox and owner notifications.
   - `knowledge.*`: kombify documentation and reviewed fixes.
   - `cloud.*`, `wallet.*`, `supplydock.*`, `kombifyme.*`: account, Wallet references, connectors, kombify Me service access.
   - Anything else: name the prefix.
   With an argument, report only that area in more depth (for `homelab` also call `techstack.server_health` for the first server).
4. **Local StackKits.** Use a relevant StackKits status tool only if the client lists it. Otherwise report that no such tool was offered, without inferring installation state.
5. **Gaps.** For an area the person expected but that is missing, explain that the owner equips it in the kombify app under **External agents**; the agent cannot equip itself.

## Report

A heading line with the observed connection status, then the identity line, one line per area and the gaps. No raw JSON, no ids the person did not ask for, no secrets. Relay a structured denial with its reason and guidance instead of retrying. Answer in the person's language.
