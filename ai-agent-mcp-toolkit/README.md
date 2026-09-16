# Turn Your Apify Actors into AI Agent Tools: The MCP Toolkit

A bundle showing how to expose YouTube transcripts, market data, Reddit research, and e-commerce/resale actors as **MCP tools** — so Claude, Cursor, VS Code Copilot, and other AI agents can call them live, mid-conversation, with no code written per query.

## What is MCP, in one paragraph

The [Model Context Protocol](https://modelcontextprotocol.io) (MCP) is an open standard that lets an AI assistant call external tools directly inside a conversation — read a file, hit an API, run a scraper — instead of only working from its training data. Apify runs a **hosted MCP server at `https://mcp.apify.com`** that turns any of its 5,000+ Actors, including every actor in this repo, into a callable MCP tool. Point an MCP-compatible client at that URL, and your agent can say *"let me check that"* and actually check it.

## Why this matters for the actors in this repo

Every other toolkit in this repo shows you how to call an Actor from your own code. This toolkit is the opposite direction: **you don't write the calling code — your AI agent does, live, based on what you ask it in plain English.** "Summarize this YouTube video," "what's on the economic calendar this week," "find me Shopify stores selling pet supplies" all become normal chat requests once the relevant Actor is registered as an MCP tool.

## How the Apify MCP server works

- **Hosted endpoint:** `https://mcp.apify.com` — no server to run or host yourself.
- **Authentication:** OAuth sign-in through your browser (no token needed for most clients), or a Bearer token (`Authorization: Bearer <APIFY_TOKEN>`) from Apify Console → Settings → Integrations if your client needs header-based auth.
- **Choosing which Actors are exposed:** append a `tools` query parameter with a comma-separated list of Actor slugs, e.g. `https://mcp.apify.com?tools=pintostudio/youtube-transcript-scraper,pintostudio/economic-calendar-data-investing-com`. Without it, the server exposes generic discovery tools (`search-actors`, `call-actor`, etc.) that let the agent find and run *any* public Actor on the fly.
- **Local/self-hosted alternative:** run `@apify/actors-mcp-server` over stdio if you want the MCP server local to your machine instead of the hosted endpoint (see config below).
- **Limits:** 30 requests/second per user; full-permission and rental Actors are excluded from the hosted server for security.

Full reference: [Apify MCP server docs](https://docs.apify.com/platform/integrations/mcp) · [MCP server configurator](https://mcp.apify.com) (pick tools visually, copy the config) · [apify/apify-mcp-server on GitHub](https://github.com/apify/apify-mcp-server).

## A curated MCP starter pack

You *can* expose all 130+ Pinto Studio Actors at once, but agents pick the right tool more reliably from a focused list. These are the best candidates for MCP — fast, single-purpose, and return text/data an LLM can reason about directly without extra processing:

| Actor | Why it's a great agent tool | `tools=` slug |
|---|---|---|
| Youtube Transcript Scraper | "Summarize/analyze this video" becomes a one-line ask | `pintostudio/youtube-transcript-scraper` |
| Youtube Search Actor | Agent can find relevant videos before summarizing them | `pintostudio/youtube-search-actor` |
| Economic Calendar Data (Investing.com) | "What's moving markets this week?" answered live | `pintostudio/economic-calendar-data-investing-com` |
| Stock Profile (Investing.com) | Quick fundamentals lookup mid-conversation | `pintostudio/stock-profile-investing-com` |
| Yahoo Finance | General quote/stat lookups the agent can cite | `pintostudio/yahoo-finance` |
| Currency Converter | Instant FX conversion inside any answer | `pintostudio/currency-converter` |
| Reddit Search Actor | "What is Reddit saying about X?" answered on demand | `pintostudio/reddit-search-actor` |
| Reddit Subreddit Posts Actor | Pull recent community discussion into the chat | `pintostudio/reddit-subreddit-posts-actor` |
| Shopify Store Intelligence | "Is this Shopify store worth pursuing?" — instant competitive read | `pintostudio/shopify-store-intelligence` |
| Sneaker Resell Price Tracker | "Is this pair worth flipping?" answered before you leave the chat | `pintostudio/sneaker-resell-price-tracker` |

Mix and match with any other Actor from the [Trading](../trading-investing-toolkit), [Shopify/E-commerce](../shopify-ecommerce-intelligence-toolkit), [Sneaker/Fashion](../sneaker-fashion-resale-toolkit), [YouTube](../youtube-content-research-toolkit), or [Reddit](../reddit-market-research-toolkit) toolkits — every slug listed there works the same way with `mcp.apify.com`.

## Setup: connect Apify Actors to your AI client

### Claude Desktop (no local install)

Settings → Connectors → Add custom connector → server URL `https://mcp.apify.com` → restart Claude Desktop and sign in via the browser prompt when it appears. Or search "Apify" in the Claude Desktop connector directory for one-click install.

### Claude Code / Cowork / other JSON-config MCP clients

```json
{
  "mcpServers": {
    "apify": {
      "url": "https://mcp.apify.com?tools=pintostudio/youtube-transcript-scraper,pintostudio/economic-calendar-data-investing-com,pintostudio/reddit-search-actor"
    }
  }
}
```

### Cursor (`.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "apify": {
      "url": "https://mcp.apify.com",
      "headers": {
        "Authorization": "Bearer <APIFY_TOKEN>"
      }
    }
  }
}
```

### VS Code with Copilot (`mcp.json`)

```json
{
  "mcpServers": {
    "apify": {
      "url": "https://mcp.apify.com?tools=pintostudio/youtube-transcript-scraper,pintostudio/shopify-store-intelligence"
    }
  }
}
```

### One-line install via Apify CLI

```bash
apify mcp install cursor --tools pintostudio/youtube-transcript-scraper,pintostudio/economic-calendar-data-investing-com
apify mcp install vscode --tools pintostudio/reddit-search-actor,pintostudio/sneaker-resell-price-tracker
```

### Local/self-hosted stdio server

For running the MCP server on your own machine instead of the hosted endpoint:

```json
{
  "mcpServers": {
    "actors-mcp-server": {
      "command": "npx",
      "args": ["-y", "@apify/actors-mcp-server", "--tools", "pintostudio/youtube-transcript-scraper"],
      "env": { "APIFY_TOKEN": "YOUR_APIFY_TOKEN" }
    }
  }
}
```

## Use cases

**A research assistant that actually watches videos.** With Youtube Transcript Scraper registered, ask Claude "pull the transcript from this video and give me the 5 key claims with timestamps" — no copy-pasting a transcript, no separate tool.

**A markets co-pilot inside your normal chat.** With the Economic Calendar and Stock Profile Actors connected, ask "what's the setup on NVDA and is there a catalyst this week?" and get a live answer instead of a knowledge-cutoff guess.

**A Reddit research analyst on call.** Connect Reddit Search and Subreddit Posts, then ask "what are people in r/webscraping frustrated with lately?" and get an actual, current answer pulled from live threads.

**A Shopify prospecting assistant.** Connect Shopify Store Intelligence and ask your agent to qualify a list of store URLs during a normal planning conversation — no separate script to run.

**A sneaker cop-or-pass advisor.** Connect Sneaker Resell Price Tracker and ask "is the Thunder 4s worth copping at retail right now?" and get a margin estimate on the spot.

## FAQ

**What is MCP and why does it matter for these Actors?**
MCP (Model Context Protocol) is the standard that lets an AI assistant call external tools mid-conversation. It turns any Actor in this repo from "something I run from code" into "something my AI agent can reach for on its own, when it decides it's relevant."

**Do I need to write any code to use this?**
No — connecting a client (Claude Desktop, Cursor, VS Code) to `https://mcp.apify.com` is a settings/config step, not a coding task. Coding is only needed for the direct-API approach covered in the other toolkits in this repo.

**Which AI clients support this?**
Any MCP-compatible client works, including Claude Desktop, Claude Code, Cursor, and VS Code with Copilot. Support across other assistants is expanding quickly — check your client's documentation for "MCP" or "connectors" support.

**Does exposing more Actors as tools make the agent smarter?**
Not necessarily — a long, unfocused tool list can make an agent worse at picking the right one. Start with the curated list above (or the specific Actors you use most) rather than exposing all 130+ at once.

**Is there a cost to using Actors this way?**
The MCP connection itself is free; each Actor run still bills under its normal Apify pay-per-event pricing, the same as calling it directly via API.

**Can I combine this with the code-based approach in the other toolkits?**
Yes — use MCP for ad-hoc, conversational lookups, and switch to the direct API/client code in the [other toolkits](../README.md) for scheduled jobs, batch processing, or anything that needs to run without a human in the loop.

---

⬅ [Back to all toolkits](../README.md) · Explore the full data catalog at [apify.com/pintostudio](https://apify.com/pintostudio)
