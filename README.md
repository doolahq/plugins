# doola plugins

The [doola](https://doola.com) plugin marketplace for **Claude Code**, **Grok Build**, and **Cursor**.

This repo is a catalog containing a single plugin, `doola`, that connects your AI coding agent to
the doola MCP server so you can form a Wyoming LLC end to end from a conversation -- company name,
industry, members, ownership, and filing with the Wyoming Secretary of State.

## Plugin

| Plugin | What it does | How it works |
|---|---|---|
| **doola** | Wyoming LLC formation, end to end, plus status on the companies you already have. | Remote MCP server at `https://mcp.doola.com`, connected over HTTP. |

## Network endpoint & credentials

The `doola` plugin talks to exactly one remote endpoint: **`https://mcp.doola.com`**, doola's
hosted MCP server. No other network calls are made by the plugin itself.

Authentication is via OAuth: the first tool call triggers your agent's OAuth flow, which opens a
browser to sign in with your doola account and authorize access. Tokens are stored and refreshed
by your agent (Claude Code / Grok Build / Cursor), not by this repo. Revoke access at any time from your
doola account settings or by removing the plugin.

## Install

Claude Code:

```bash
claude plugin marketplace add doolahq/plugins
claude plugin install doola@doola
```

Grok Build:

```bash
grok plugin marketplace add doolahq/plugins
grok plugin install doola@doola
```

Cursor: search for `doola` in the [Cursor Marketplace](https://cursor.com/marketplace) and
install it.

Or open `/plugin` (Claude Code) / `/plugins` (Grok Build) in the TUI and install from the
Marketplace tab.

On first use you'll be prompted to sign in to your doola account via OAuth.

## Layout

`.claude-plugin/marketplace.json` -- the Claude Code catalog. Lists the colocated
[`doola/`](./doola) plugin (`source: ./doola`).

`.grok-plugin/marketplace.json` -- the Grok Build catalog, self-hosted copy of the same
plugin. Submitted to the [xAI plugin marketplace](https://github.com/xai-org/plugin-marketplace)
as a url source pinned to a commit SHA, with `source.path` set to `doola`.

`.cursor-plugin/marketplace.json` -- the Cursor catalog, listing the same `doola/` plugin.
Submitted to the [Cursor Marketplace](https://cursor.com/marketplace/publish).

`doola/.claude-plugin/plugin.json` -- the plugin manifest (name, version, author, license,
keywords).

`doola/.cursor-plugin/plugin.json` -- the Cursor plugin manifest.

`doola/.mcp.json` -- the MCP server declaration, pointing at `https://mcp.doola.com`.
`doola/mcp.json` is the same declaration in the shape Cursor expects (`type: http`).

## License

MIT, see [LICENSE](./LICENSE).
