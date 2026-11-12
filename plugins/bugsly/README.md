# Bugsly plugin for Claude Code

Read, search and triage the errors in your own [Bugsly](https://bugsly.dev) projects from Claude Code: stack traces and breadcrumbs, cron monitors, uptime monitors, crash-free rate and event usage. Status changes happen only when you ask.

## Install

```text
/plugin marketplace add airdropfi/bugsly-claude-plugin
/plugin install bugsly@bugsly-plugins
```

Then `/reload-plugins`, open `/mcp`, choose `bugsly` and Authenticate: OAuth 2.1 sign-in in your browser, approve on Bugsly's consent page. There is no key to paste. The access appears in Bugsly under Settings, AI Agent / MCP, where you can revoke it.

Without the plugin you can add just the server: `claude mcp add --transport http bugsly https://bugsly.dev/api/mcp`.

## What is inside

- `.mcp.json`: the remote MCP server `bugsly` (`https://bugsly.dev/api/mcp`), 16 tools.
- Skills: `triage-an-error` (find, read, explain, fix, resolve on request) and `check-project-health` (monitors, crash-free, usage; read-only).
- Commands: `/bugsly:issues [project]` and `/bugsly:health [project]`, both read-only.

## Tools

| Tool | What it does | Kind |
|---|---|---|
| `list_projects` | List the projects in your first Bugsly organization, with project IDs and DSN host (the DSN key is not shown; the token acts as your user and other organizations are not listed). | read-only |
| `list_issues` | List issues for a Bugsly project. | read-only |
| `get_issue` | Get details of a specific issue including metadata. | read-only |
| `get_issue_events` | Get recent events (occurrences) for an issue with stack traces and breadcrumbs. | read-only |
| `resolve_issue` | Mark an issue as resolved. | changes data, destructive hint |
| `ignore_issue` | Mark an issue as ignored. | changes data, destructive hint |
| `search_errors` | Search for issues by title keyword. | read-only |
| `get_project_stats` | Get transaction performance stats for a project. | read-only |
| `create_project` | Create a new project in your Bugsly organization (the first one unless org_id is given). | writes |
| `get_usage` | Get current billing usage for your organization (events used, limit, plan). | read-only |
| `get_checkout_url` | Creates a Polar checkout link for the Team or Business plan; plans and prices are listed at https://bugsly.dev/pricing. | writes |
| `list_monitors` | List cron monitors for a project. | read-only |
| `get_monitor` | Get details and recent check-ins for a cron monitor. | read-only |
| `list_uptime_monitors` | List uptime monitors for a project. | read-only |
| `get_uptime_status` | Get uptime stats (uptime %, avg latency, p95) for a monitor. | read-only |
| `get_crash_free` | Get crash-free sessions % and crash-free users % (release-health stability) for a project over the last N days. | read-only |

## Things to know

- You need a Bugsly account (https://bugsly.dev) and a project that has received errors.
- `resolve_issue` and `ignore_issue` change an issue's status for everyone on the project. Resolved issues come back as a regression if the error returns; both can be reversed in the dashboard. `create_project` creates a real project each call.
- Event content is returned wrapped as untrusted data, `get_issue_events` output is size-capped and omits user email, IP address, username and extra data, and the DSN key is not shown. The skills tell Claude to treat event text as data, not instructions; still review code changes.
- Claude Code asks before tool calls by default; keep it that way for the two status-changing tools.

## Data and privacy

The MCP server receives what the tools need: the project IDs, issue IDs and search terms the agent sends, and it returns your issue, event, monitor and usage data from your Bugsly account. Issue and event data are returned wrapped as untrusted data; event output is size-capped and omits user email, IP address, username and extra data, and the DSN key is not shown. See the [privacy policy](https://bugsly.dev/privacy) and [terms](https://bugsly.dev/terms). The plugin itself stores nothing and runs no code on your machine.

## Support

https://bugsly.dev/agents or hello@bugsly.dev.

## License

MIT, see `LICENSE`. The Bugsly service is governed by its terms.
