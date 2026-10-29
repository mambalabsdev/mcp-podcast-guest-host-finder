# Podcast Guest and Host Finder MCP Server

[![Smithery](https://smithery.ai/badge/mambabuilt/mcp-podcast-guest-host-finder)](https://smithery.ai/servers/mambabuilt/mcp-podcast-guest-host-finder) [![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-podcast-guest-host-finder/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-podcast-guest-host-finder) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-podcast-guest-host-finder%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-podcast-guest-host-finder&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-podcast-guest-host-finder)](https://www.npmjs.com/package/@mambalabsdev/mcp-podcast-guest-host-finder) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-podcast-guest-host-finder)](https://www.npmjs.com/package/@mambalabsdev/mcp-podcast-guest-host-finder) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-podcast-guest-host-finder)](https://github.com/mambalabsdev/mcp-podcast-guest-host-finder/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-podcast-guest-host-finder)

<a href="https://mcprush.com/to/podcast-guest-host-finder-mcp?ref=badge"><img width="380" height="200" src="https://mcprush.com/badge/podcast-guest-host-finder-mcp/card.svg" alt="Podcast Guest Host Finder MCP server" /></a>

An MCP server for the Mamba Labs Podcast Guest and Host Finder actor on Apify. Give it a topic, or Apple Podcasts links and RSS feeds. Each run returns one row per show with what you need to pitch it.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Your keys](#your-keys)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Each row carries the host, the owner name and email the show publishes in its own RSS feed, episode count and cadence, an active flag, the share of episodes that name a guest, recent guest names (from podcast:person tags or episode titles), companies named beside guests, and the contact and be a guest pages on the show website. Shows come from the Apple Podcasts catalog for a topic, or from the links you give. A show whose feed cannot be read comes back free with Apple catalog fields only.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-podcast-guest-host-finder": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-podcast-guest-host-finder"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `find_podcasts` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Find 25 active B2B sales podcasts that interview guests, with the host email and the be a guest page."
- "Who were the recent guests on these three podcasts, and which companies were they from?"
- "List SaaS marketing podcasts that published in the last 90 days."

## Tool

`find_podcasts`. One tool. Example arguments:

```json
{
  "topic": "B2B sales",
  "max_podcasts": "25",
  "active_within_days": "90",
  "guest_shows_only": "true"
}
```

## Inputs

Every buyer facing input of the actor, unchanged. Omitted inputs take the actor's own defaults. Numbers and booleans are sent as strings.

| Input | Type | Description |
|---|---|---|
| `topic` | string | What the podcasts are about |
| `topics` | array | More topics, up to 20 |
| `podcast_urls` | array | Apple Podcasts links or RSS feed URLs, up to 200 |
| `country` | string | Apple Podcasts catalog country. Default us |
| `max_podcasts` | string | Shows per topic, 1 to 200. Default 25 |
| `episodes_to_read` | string | Newest episodes read per show, 5 to 300. Default 50 |
| `active_within_days` | string | Only shows with an episode in this many days |
| `min_episodes` | string | Only shows with at least this many episodes |
| `guest_shows_only` | string | true or false. Default false |
| `find_contact_page` | string | true or false. Default true |
| `max_charge_usd` | string | Optional cost cap for the run |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `podcast-row`, per show with its feed read | $0.004 | $0.0038 | $0.0036 | $0.0034 |
| `apify-actor-start`, per run start | $0.0005 | $0.0005 | $0.0005 | $0.0005 |

A show whose feed could not be read, no results rows, and error rows are free.

## Your keys

The actor needs no key. It reads the Apple iTunes Search API, public RSS feeds, and one page of each show website, and holds no key of any kind. Mamba Labs pays the platform and proxy costs of the run.

## Full actor documentation

[apify.com/mambalabs/podcast-guest-host-finder](https://apify.com/mambalabs/podcast-guest-host-finder)

## License

MIT. See [LICENSE](LICENSE).
