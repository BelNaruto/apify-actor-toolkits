# Apify Actor Toolkits

**Ready-to-run bundles of [Apify Actors](https://apify.com/store) — grouped by real job, not by platform — for traders, e-commerce sellers, resellers, content creators, and researchers.**

Apify Actors are hosted, pay-per-use scraping and automation programs you can call from an API, a no-code tool, or an AI agent (they also work as [MCP tools](https://mcp.apify.com/)). Each folder in this repo is a **toolkit**: a small set of Actors from the [Pinto Studio](https://apify.com/pintostudio) store profile that solve one specific problem when used *together*, plus copy-pasteable Node.js and Python code, real use cases, and an FAQ.

No Actor here needs you to write a scraper, maintain proxies, or fight anti-bot systems — you send a JSON input, and you get structured JSON (or CSV/Excel) back.

## Toolkits

| Toolkit | Best for | Actors bundled |
|---|---|---|
| [Trading & Investing Data Toolkit](./trading-investing-toolkit) | Day traders, swing traders, algo/quant builders, fintech apps | Economic, earnings & IPO calendars, stock fundamentals, crypto, Yahoo Finance, CNN Business |
| [Shopify & E-commerce Competitive Intelligence Toolkit](./shopify-ecommerce-intelligence-toolkit) | Dropshippers, Shopify agencies, lead-gen, market researchers | Shopify store intelligence, leads finder, competitor tracking, Amazon scrapers |
| [Sneaker & Fashion Resale Price-Tracking Toolkit](./sneaker-fashion-resale-toolkit) | Sneaker resellers, fashion arbitrage sellers, price-comparison tools | Sneaker resell tracker, Kickscrew, Zara, Vinted, Etsy, H&M |
| [YouTube Content Research & Repurposing Toolkit](./youtube-content-research-toolkit) | Creators, podcasters, marketers, AI/LLM training pipelines | Transcript scraper, translated & multi-video transcripts, search, channel & video data |
| [Reddit Community & Market Research Toolkit](./reddit-market-research-toolkit) | Marketers, community managers, trend & sentiment researchers | Subreddit search, posts, comments, users, trending & random subreddit discovery |

Each toolkit README follows the same structure: **who it's for → the Actors and what they extract → how to chain them → runnable code → use cases → FAQ.**

## Quickstart: running any Actor in this repo

All Actors are called the same way, whether you use the [Apify API](https://docs.apify.com/api/v2), the [JavaScript client](https://docs.apify.com/api/client/js/), or the [Python client](https://docs.apify.com/api/client/python/). Grab a free API token from your [Apify Console → Settings → Integrations](https://console.apify.com/account/integrations) page, then:

### Node.js

```bash
npm install apify-client
```

```js
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });

// Replace with any Actor slug from a toolkit below, e.g. "pintostudio/economic-calendar-data-investing-com"
const run = await client.actor('pintostudio/<actor-slug>').call({
  // Actor-specific input — see each Actor's README/Input tab on Apify Store
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

### Python

```bash
pip install apify-client
```

```python
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])

run = client.actor("pintostudio/<actor-slug>").call(run_input={
    # Actor-specific input
})

items = client.dataset(run["defaultDatasetId"]).list_items().items
print(items)
```

### One-off, no code (REST)

```bash
curl "https://api.apify.com/v2/acts/pintostudio~<actor-slug>/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{ }'
```

`run-sync-get-dataset-items` blocks until the run finishes and streams the dataset straight back — ideal for quick tests and n8n/Zapier/Make webhooks. For production, use the async `run` endpoint and poll or use a webhook.

## Why bundle Actors instead of using one at a time?

A single scraper answers one question. Real decisions — *is this stock worth watching, is this Shopify store worth prospecting, is this sneaker worth flipping* — need two or three data sources cross-referenced. Each toolkit below exists because that combination comes up constantly and is worth wiring once instead of re-discovering every time.

## About the Actors

All Actors linked here are published and maintained by **[Pinto Studio](https://apify.com/pintostudio)** on the Apify Store — 130+ public Actors spanning finance, e-commerce, social, and content data. Browse the full catalog at [apify.com/pintostudio](https://apify.com/pintostudio).

---

*This repo is documentation and code examples only — it doesn't bundle or resell the Actors themselves. Each Actor is run directly on Apify under its own pay-per-event pricing.*
