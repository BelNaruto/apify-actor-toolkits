# Best Apify Actors for Traders & Investors: The Trading & Investing Data Toolkit

A bundle of 25+ market-data Actors — economic and earnings calendars, stock fundamentals, crypto data, Yahoo Finance, and CNN Business figures — that together answer the question every trader asks every morning: **what's moving today, and is this position still worth holding?**

Every Actor below scrapes a public financial data source (Investing.com, Yahoo Finance, CNN Business) into clean, structured JSON you can pull into a spreadsheet, a Python notebook, a trading bot, or a dashboard — no browser automation or anti-bot work required on your side.

## Who this is for

- **Day traders** who want economic-calendar catalysts and earnings surprises in a machine-readable feed instead of refreshing a website.
- **Swing traders and investors** screening stocks by fundamentals, analyst targets, and dividend history before entering a position.
- **Algo/quant builders** who need a historical or scheduled data pipeline to backtest or feed a model.
- **Fintech / indie-hacker builders** shipping a portfolio tracker, screener, or newsletter and need a data layer without a Bloomberg-terminal budget.

## What's in the toolkit

### Market calendars — know what's happening before it happens

| Actor | What it extracts | Link |
|---|---|---|
| Economic Calendar Data (Investing.com) | Scheduled macro releases (CPI, NFP, rate decisions) with forecast/actual/previous values, by country and impact level | [pintostudio/economic-calendar-data-investing-com](https://apify.com/pintostudio/economic-calendar-data-investing-com) |
| Earnings Calendar Data (investing.com) | Upcoming and historical earnings dates, EPS estimates vs. actuals | [pintostudio/earnings-calendar-data-investing-com](https://apify.com/pintostudio/earnings-calendar-data-investing-com) |
| IPO Calendar Data (investing.com) | Upcoming IPOs with expected pricing date and exchange | [pintostudio/ipo-calendar-data-investing-com](https://apify.com/pintostudio/ipo-calendar-data-investing-com) |
| Trader Master Calendar Data (investing.com) | Combined calendar view (economic + earnings + more) in one call | [pintostudio/trader-master-calendar-data-investing-com](https://apify.com/pintostudio/trader-master-calendar-data-investing-com) |

### Stock fundamentals & research — screen before you buy

| Actor | What it extracts | Link |
|---|---|---|
| Stock Profile (Investing.com) | Company overview, sector, exchange, key stats | [pintostudio/stock-profile-investing-com](https://apify.com/pintostudio/stock-profile-investing-com) |
| Stock Financials (investing.com) | Income statement, balance sheet, cash flow line items | [pintostudio/stock-financials-investing-com](https://apify.com/pintostudio/stock-financials-investing-com) |
| Stock Asset Metrics (investing.com) | Valuation ratios (P/E, P/B, margins, ROE, etc.) | [pintostudio/stock-asset-metrics-investing-com](https://apify.com/pintostudio/stock-asset-metrics-investing-com) |
| Stock Analyst Price Target (investing.com) | Consensus and individual analyst price targets | [pintostudio/stock-analyst-price-target-investing-com](https://apify.com/pintostudio/stock-analyst-price-target-investing-com) |
| Stock Consensus Estimates (investing.com) | Forward EPS/revenue consensus estimates | [pintostudio/stock-consensus-estimates-investing-com](https://apify.com/pintostudio/stock-consensus-estimates-investing-com) |
| Stock Fair Value (investing.com) | Investing.com's fair-value / undervalued-overvalued model output | [pintostudio/stock-fair-value-investing-com](https://apify.com/pintostudio/stock-fair-value-investing-com) |
| Stock Dividends (investing.com) | Dividend history, yield, ex-dividend dates | [pintostudio/stock-dividends-investing-com](https://apify.com/pintostudio/stock-dividends-investing-com) |
| Stock Historical Data (investing.com) | OHLCV historical price series | [pintostudio/stock-historical-data-investing-com](https://apify.com/pintostudio/stock-historical-data-investing-com) |
| Similar Stock (investing.com) | Peer/competitor tickers for comparative analysis | [pintostudio/similar-stock-investing-com](https://apify.com/pintostudio/similar-stock-investing-com) |
| Stock Information (investing.com) | General quote-page data snapshot | [pintostudio/stock-information-investing-com](https://apify.com/pintostudio/stock-information-investing-com) |
| Stock Earnings | Reported earnings history | [pintostudio/stock-earnings](https://apify.com/pintostudio/stock-earnings) |
| Stock Earnings Transcript | Full earnings-call transcripts, text-searchable | [pintostudio/stock-earnings-transcript](https://apify.com/pintostudio/stock-earnings-transcript) |
| Stock Insights | Aggregated analysis/insight snippets per ticker | [pintostudio/stock-insights](https://apify.com/pintostudio/stock-insights) |
| Stock Recent Data | Latest price/volume snapshot | [pintostudio/stock-recent-data](https://apify.com/pintostudio/stock-recent-data) |

### Crypto

| Actor | What it extracts | Link |
|---|---|---|
| Crypto Info (investing.com) | Coin overview: price, market cap, supply | [pintostudio/crypto-info-investing-com](https://apify.com/pintostudio/crypto-info-investing-com) |
| Cryptocurrency Overview (investing.com) | Market-wide crypto snapshot | [pintostudio/invest-crypto-Overview](https://apify.com/pintostudio/invest-crypto-Overview) |
| Invest Crypto Historical | Historical OHLCV for a coin | [pintostudio/invest-crypto-historical](https://apify.com/pintostudio/invest-crypto-historical) |
| Crypto Recent Data | Latest crypto price/volume snapshot | [pintostudio/crypto-recent-data](https://apify.com/pintostudio/crypto-recent-data) |

### Yahoo Finance

| Actor | What it extracts | Link |
|---|---|---|
| Yahoo Finance | Quote, summary, and key stats for a ticker | [pintostudio/yahoo-finance](https://apify.com/pintostudio/yahoo-finance) |
| Yahoo Finance Historical | Historical price data | [pintostudio/yahoo-finance-historical](https://apify.com/pintostudio/yahoo-finance-historical) |
| Yahoo Finance Stock Options | Options chain data (calls/puts, strikes, open interest) | [pintostudio/yahoo-finance-stock-options](https://apify.com/pintostudio/yahoo-finance-stock-options) |

### CNN Business & utilities

| Actor | What it extracts | Link |
|---|---|---|
| CNN Business Stock Price | Current price snapshot from CNN Business | [pintostudio/cnn-business-stock-price](https://apify.com/pintostudio/cnn-business-stock-price) |
| CNN Business Stock Total Revenue | Revenue figures | [pintostudio/cnn-business-stock-total-revenue](https://apify.com/pintostudio/cnn-business-stock-total-revenue) |
| CNN Business Stock Earnings Per Share | EPS figures | [pintostudio/cnn-business-stock-earnings-per-share](https://apify.com/pintostudio/cnn-business-stock-earnings-per-share) |
| CNN Business Stock Net Income | Net income figures | [pintostudio/cnn-business-stock-net-income](https://apify.com/pintostudio/cnn-business-stock-net-income) |
| Currency Converter | Real-time FX conversion between currency pairs | [pintostudio/currency-converter](https://apify.com/pintostudio/currency-converter) |

## How it fits together: a morning trading workflow

1. **Pull the Economic Calendar + Earnings Calendar** for today and tomorrow → flag high-impact events and tickers reporting earnings.
2. For every ticker on your watchlist that has an event, **pull Stock Profile + Stock Asset Metrics + Analyst Price Target** → is the setup fundamentally sound, or is this pure news noise?
3. **Pull Stock Historical Data** (or Yahoo Finance Historical) to check how the stock has reacted to similar events in the past.
4. If it's a dividend or long-hold candidate, add **Stock Dividends + Stock Fair Value** to the picture.
5. Log everything to a sheet or database — now you have a repeatable, backtestable pre-market checklist instead of a gut feeling.

## Code example: build a pre-market watchlist brief (Node.js)

```js
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const tickers = ['AAPL', 'NVDA', 'TSLA'];

async function runActor(slug, input) {
  const run = await client.actor(`pintostudio/${slug}`).call(input);
  const { items } = await client.dataset(run.defaultDatasetId).listItems();
  return items;
}

const [economicEvents, earningsEvents] = await Promise.all([
  runActor('economic-calendar-data-investing-com', { dateFrom: 'today', dateTo: 'today', importance: ['high'] }),
  runActor('earnings-calendar-data-investing-com', { dateFrom: 'today', dateTo: 'today' }),
]);

const watchlist = [];
for (const ticker of tickers) {
  const [profile, metrics, priceTarget] = await Promise.all([
    runActor('stock-profile-investing-com', { symbol: ticker }),
    runActor('stock-asset-metrics-investing-com', { symbol: ticker }),
    runActor('stock-analyst-price-target-investing-com', { symbol: ticker }),
  ]);
  watchlist.push({ ticker, profile, metrics, priceTarget });
}

console.log({ economicEvents, earningsEvents, watchlist });
// Feed this straight into a Slack/Discord digest, a Google Sheet, or an LLM summarizer.
```

*(Input field names above are illustrative — check each Actor's "Input" tab on its Apify Store page for the exact schema before running.)*

## Use cases

**Pre-market news-catalyst scanner.** Combine the Economic and Earnings calendars every morning to auto-generate a list of tickers with a scheduled catalyst today, ranked by historical volatility reaction.

**Earnings-season dashboard.** Pull Earnings Calendar + Stock Consensus Estimates + Stock Earnings Transcript to see, at a glance, which companies are about to report, what the Street expects, and — after the call — what management actually said.

**Fundamentals screener.** Loop Stock Asset Metrics + Stock Fair Value + Analyst Price Target across an index to rank stocks by how undervalued they look relative to consensus targets.

**Dividend income tracker.** Use Stock Dividends across a portfolio to build a forward income calendar and flag upcoming ex-dividend dates.

**Crypto/FX-aware portfolio bot.** Combine Crypto Recent Data and Currency Converter so a multi-asset portfolio tracker reports everything in one base currency.

**Backtesting dataset builder.** Schedule Stock Historical Data / Yahoo Finance Historical runs to accumulate your own point-in-time OHLCV dataset for strategy backtests, without a data-vendor subscription.

## FAQ

**What's the best way to get stock market data via API without a Bloomberg/Refinitiv subscription?**
Combining a few purpose-built Actors — like Stock Profile, Stock Financials, and Yahoo Finance above — gets you fundamentals, historicals, and calendars in structured JSON for a fraction of a terminal subscription, billed per use.

**Can I get an economic calendar (CPI, NFP, rate decisions) as an API instead of a website?**
Yes — the Economic Calendar Data Actor returns scheduled macro releases with forecast/actual/previous values as JSON, which you can poll on a schedule or trigger via webhook.

**Is scraping financial data sites like Investing.com or Yahoo Finance allowed?**
These Actors extract publicly visible data for personal research and internal tooling. Always check the target site's terms of service and your local regulations for your specific use case, and avoid redistributing raw data as a competing product.

**Can I run these on a schedule automatically?**
Yes — Apify Actors support built-in [scheduling](https://docs.apify.com/platform/schedules) and webhooks, so you can trigger a run every morning before market open and pipe the dataset straight into Slack, email, Google Sheets, or a database.

**Do I need to know how to code?**
No — every Actor also runs from the Apify Console UI (fill in a form, click Run, download CSV/Excel/JSON) and from no-code tools like Make, n8n, and Zapier via Apify's integrations.

---

⬅ [Back to all toolkits](../README.md) · Explore the full data catalog at [apify.com/pintostudio](https://apify.com/pintostudio)
