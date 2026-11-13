# SIMBIA for AI agents

Connect Claude, ChatGPT, Gemini, Cursor or any other MCP client to [SIMBIA](https://simbia.eu), a business system with CRM, accounting, bank, mail, documents and HR.

The agent reads what you can see in SIMBIA and prepares changes. Every change waits for your approval in SIMBIA before anything happens.

- **Server address:** `https://crm.simbia.eu/api/mcp`
- **Protocol:** Model Context Protocol, Streamable HTTP
- **Sign-in:** OAuth. You sign in to SIMBIA in the browser and choose what the agent may do.

You need a SIMBIA account with the manager role. Access for client companies is being rolled out; write to us at [simbia.eu](https://simbia.eu) to get it.

## What the agent can do

| | |
|---|---|
| Read | Leads, tasks, offers, documents, projects, invoices, bank operations, journal, reports, tax calendar, company mail |
| Propose | Bank matching, journal entries, invoice posting, reversals, author's fees, and any other change in the CRM. You approve or reject each one in SIMBIA, with a preview computed by the server |
| Do right away | Upload a file you pointed at and add it to Documents |
| Never | Approve its own proposals, send mail or e-invoices, create access keys, change accounts and roles |

When you connect an agent, SIMBIA asks which right to give it: **read only** or **read and propose**. You can disconnect it at any time in SIMBIA: Settings → Claude access.

## Install

### Claude (claude.ai, desktop and mobile)

1. Open **Customize → Connectors → Add custom connector**.
2. Name: `SIMBIA`. URL: `https://crm.simbia.eu/api/mcp`.
3. Sign in to SIMBIA and press **Allow**.

### ChatGPT

1. Open the connectors (plugins) settings and add a custom MCP server.
2. Name: `SIMBIA`. URL: `https://crm.simbia.eu/api/mcp`. Authentication: OAuth.
3. Sign in to SIMBIA and press **Allow**.

Custom MCP servers in ChatGPT depend on your plan.

### Claude Code

```bash
claude plugin marketplace add Sunlucki/simbia-mcp
```

```bash
claude plugin install simbia@simbia
```

Then run `/mcp` in a session, pick `simbia` and authenticate. The plugin also adds a skill with the rules for working in SIMBIA.

Without the plugin, the server alone:

```bash
claude mcp add --transport http simbia https://crm.simbia.eu/api/mcp
```

### Cursor

Add to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "simbia": {
      "url": "https://crm.simbia.eu/api/mcp"
    }
  }
}
```

Or, if your Cursor version supports install links: `cursor://anysphere.cursor-deeplink/mcp/install?name=simbia&config=eyJ1cmwiOiJodHRwczovL2NybS5zaW1iaWEuZXUvYXBpL21jcCJ9`

### Gemini CLI

```bash
gemini extensions install https://github.com/Sunlucki/simbia-mcp
```

Then run `/mcp auth simbia`.

Without the extension, add to `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "simbia": {
      "httpUrl": "https://crm.simbia.eu/api/mcp"
    }
  }
}
```

### Any other MCP client

Point the client at `https://crm.simbia.eu/api/mcp`. Clients that support MCP authorization discover the OAuth endpoints by themselves. Clients that only send a fixed header can use a personal key from SIMBIA (Settings → Claude access):

```
Authorization: Bearer <your key>
```

## What is in this repository

| Path | For |
|---|---|
| `.claude-plugin/`, `.mcp.json`, `skills/` | Claude Code plugin and its marketplace entry |
| `gemini-extension.json`, `GEMINI.md` | Gemini CLI extension |
| `README.md` | Instructions for the other clients |

The SIMBIA server itself is not here. This repository only tells each client where the server is and how to work with it.

## Support

[simbia.eu](https://simbia.eu)
