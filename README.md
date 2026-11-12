# Bugsly plugins for Claude Code

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
