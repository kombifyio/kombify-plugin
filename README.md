# kombify plugin

Connect the agent you already use to kombify Cloud. With this plugin, Claude (and other agents that read Agent Plugins) can read, diagnose and change your own homelab servers, reach your kombify account, Paperwork and agent inbox through the kombify Gateway, look up kombify documentation and reviewed fixes, and work with a local StackKits installation.

kombify is a platform for running your own homelab and self-hosted services, with access from anywhere. Learn more at [kombify.io](https://kombify.io).

## What you get

| Part | What it does |
| --- | --- |
| Connector `kombify` | Remote MCP server `https://api.kombify.io/mcp`. Signs in with your kombify account (OAuth 2.0 with PKCE). Shows the tools your account is entitled to and that you equipped for this agent. |
| Connector `stackkit` | Local MCP server `stackkit-mcp --mode docs,local,server` from the StackKits product. Starts only on a machine where StackKits is installed. |
| Skills | `getting-started`, `connect` (`/kombify:connect`), `homelab-operations`, `techstack-inventory`, `cloud-agents`, `supply-dock`, `gateway-api`, `knowledge-usage`, `stackkits-catalog`, `stackkits-operations` |
| Agent | `homelab-operator`: investigates a homelab problem, proposes one change, runs it after your go-ahead and verifies the result |

## Install and connect

1. After the plugin is listed, add it from the Claude plugin directory. To try a local checkout of this bundle in Claude Code, start Claude with `claude --plugin-dir .` from the plugin folder.
2. In Claude or Cowork, open the plugin's **Connectors** tab and connect **Kombify**. In Claude Code, open `/mcp` and select the bundled `kombify` connector. Sign in with your kombify account in the browser.
3. Run `/kombify:connect` to see who the agent acts as and what it can reach.
4. In the kombify app's **External agents** settings, enable the client and equip the abilities you want it to use, such as homelab changes or Paperwork mail.

Installing the plugin signs in nothing, starts nothing on your servers and grants nothing.

## Safety

- When an action needs your Decision, Kombify asks in the Companion inbox. The operation's receipt shows its outcome.
- No tool returns a secret value. Secrets are referenced by Wallet item id.
- Outside agents cannot grant, share or reveal access; you do that in the kombify app.
- You can switch a client off at any time in the kombify app.

## Data

The plugin itself contains only instructions and connector addresses; it runs no code of its own. The `kombify` connector sends requests only to `api.kombify.io` and receives your account data that the tools you call return. Some optional tools, when you equipped them, read a file on a device you chose (only with your Files permission) or start a sign-in with a third-party provider you picked, which opens that provider's page in your browser. The `stackkit` connector runs on your machine and talks to your StackKits installation and the servers you configured in it. Nothing is sent unless you or the agent call such a tool. Privacy policy: [kombify.io/privacy](https://kombify.io/privacy). Terms: [kombify.io/terms](https://kombify.io/terms).

## Support

Documentation: [docs.kombify.io/apps/ai/mcp](https://docs.kombify.io/apps/ai/mcp). Support: [kombify.io/en/support](https://kombify.io/en/support).

## License

Apache-2.0. This repository is generated from the kombify plugin source; changes are made there, not here.
