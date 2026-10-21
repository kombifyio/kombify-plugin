# Discover the right connector

Start from the intended result and inspect the selected connector's current `tools/list`: a package lists possible connections, discovery shows which tools this signed-in user can call now.

| Intended result | Connection | Evidence |
| --- | --- | --- |
| Understand Kombify, find product docs | Knowledge or OpenWiki | Search, read the returned source, report provenance |
| Work with the user's documents or mail | Paperwork | Discovered tools and tenant-bound results |
| Inspect the current local StackKit | StackKits | The installed product's self-check and discovered local tools |
| Operate a connected Kombify resource | Central customer MCP | The discovered tool and its structured permission guidance |

## Missing access

- Plugin installation, authentication and action permission are separate facts. Missing authentication: ask the client to complete its OAuth connection. Denied permission: relay the backend's reason and guidance. Installing a skill or reading this reference grants no action.
- Credentials stay in the client's store or the product's server-side custody; never ask for tokens, passwords or authorization headers in chat, skills or tool arguments.
- When one connector is unavailable, report that failure and keep the others. A tools listing does not prove an action completed; that needs the action's result.
