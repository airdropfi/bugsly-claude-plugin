# Bugsly plugins for Claude Code

> Bugsly is error tracking built for AI agents to operate: your agent (ChatGPT, Claude, Cursor, Gemini CLI) reads, triages and, when asked, resolves issues over MCP while you tag the work, approve and review. It is hosted, accepts Sentry SDK events and adds AI explanations, cron and uptime monitoring and session replay.

## At a glance

| | |
|---|---|
| What it is | Bugsly is error tracking built for AI agents to operate: your agent (ChatGPT, Claude, Cursor, Gemini CLI) reads, triages and, when asked, resolves issues over MCP while you tag the work, approve and review. It is hosted, accepts Sentry SDK events and adds AI explanations, cron and uptime monitoring and session replay. |
| Who it is for | Engineering teams at startups and small companies that let an AI agent work on their errors (the agent reads and triages, you approve and audit); individual developers on the Free plan. |
| What it does not do | Bugsly is not open source and cannot be self-hosted, has no single sign-on, and never merges code by itself. This repository is a connector, not an error tracker: you need a Bugsly account with a project that has received errors. |
| Price | Free $0 (100 issues/month), Team $19/month (2,000 issues), Business $49/month (20,000 issues), Enterprise custom; billed by unique issues, unlimited users on paid plans. Current numbers: https://bugsly.dev/pricing.md |
| MCP server | https://bugsly.dev/api/mcp (Streamable HTTP, OAuth 2.1). Official MCP Registry name: `dev.bugsly/mcp-server` |
| Human oversight | OAuth consent page, every connection listed and revocable under Settings, AI Agent / MCP, destructive tools annotated so the client can ask first, status changes reversible in the dashboard. |
| More | https://bugsly.dev/mcp (install steps, agent quickstart) , https://bugsly.dev/llms.txt , https://bugsly.dev/.well-known/mcp/server-card.json |

## Connect in 60 seconds

```text
/plugin marketplace add airdropfi/bugsly-claude-plugin
/plugin install bugsly@bugsly-plugins
```
Then `/reload-plugins`, open `/mcp`, choose `bugsly` and Authenticate: Bugsly opens in your browser, you sign in and press Allow.

## Prompts to try

Tag the work, then review: add "Show me what you read and what you changed so I can approve" to any of these.

- "Use Bugsly to list my projects and show the 5 newest unresolved errors in the first one."
- "Use Bugsly to find the issue about TypeError, open its latest event and explain the stack trace and the likely cause."
- "Use Bugsly to check whether my cron monitors and uptime monitors are healthy."
- "Use Bugsly to give me the crash-free sessions and users percentage for the last 30 days."
- "Use Bugsly to read the most frequent unresolved issue, find the failing line in this repository and propose a fix. Do not change the issue's status."

Site: https://bugsly.dev - MCP page: https://bugsly.dev/mcp - Registry: https://registry.modelcontextprotocol.io/v0/servers?search=dev.bugsly

---

A Claude Code plugin marketplace with one plugin, [`bugsly`](plugins/bugsly/README.md): read, search and triage the errors in your Bugsly projects, check monitors and crash-free rate, and resolve or ignore an issue only when you ask.

## Install

```text
/plugin marketplace add airdropfi/bugsly-claude-plugin
/plugin install bugsly@bugsly-plugins
```

You need a Bugsly account (https://bugsly.dev) and Claude Code. Then `/reload-plugins`, open `/mcp`, choose `bugsly` and Authenticate (OAuth sign-in in your browser; no key to paste). From a shell: `claude plugin marketplace add airdropfi/bugsly-claude-plugin` then `claude plugin install bugsly@bugsly-plugins`. Details are in [plugins/bugsly/README.md](plugins/bugsly/README.md).

## Layout

```text
.claude-plugin/marketplace.json     marketplace "bugsly-plugins", lists the plugin
plugins/bugsly/
  .claude-plugin/plugin.json        manifest (name, version, listing URLs, icon)
  .mcp.json                         remote MCP server https://bugsly.dev/api/mcp (OAuth)
  skills/                           triage-an-error, check-project-health
  commands/                         /bugsly:issues, /bugsly:health
  README.md, LICENSE, assets/icon.png
scripts/validate.mjs                schema checks, no dependencies
LICENSE                             MIT
```

## Validate

```bash
node scripts/validate.mjs            # documented-schema checks, exit 1 on errors
node scripts/validate.mjs --strict   # warnings fail too
node scripts/validate.mjs --cli      # also runs `claude plugin validate --strict` when the claude CLI is installed
```

## Keeping it honest

- The skills name tools from the Bugsly MCP server's tool list.
- Plans and prices are never written here; they live at https://bugsly.dev/pricing.

## License

MIT, see [LICENSE](LICENSE).
