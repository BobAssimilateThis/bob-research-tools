# Bob Research Tools

Paid web research tools for AI agents, available as a remote MCP server and as an HTTP API. Each call is paid in USDC with the x402 protocol, on Base or Solana. A call that fails is not charged.

## MCP server

- Address: https://bob.assimilatethis.com/mcp (streamable HTTP)
- Same eight tools with plain names, for clients that reject dots in tool names: https://bob.assimilatethis.com/flat/mcp
- Registry name: com.assimilatethis.bob/research-tools (official MCP Registry)
- Listing the tools is free. Each tool call needs an x402 payment.

| Tool | Input | What it does | Price |
| --- | --- | --- | --- |
| research.answer | q | Answers one open research question from the live web in at most 80 words, with source URLs | $0.02 |
| research.factcheck | claim | Checks one claim against the live web: supported, contradicted or unclear, with sources | $0.01 |
| page.summarize | url | 80-word summary of a web page with key points | $0.005 |
| page.extract | url | Clean markdown of a page's main content (up to 8,000 characters) | $0.005 |
| web.search | q, n, since, until | Ranked search results (title, URL, snippet), optionally limited to a publish-date range | $0.005 |
| web.news | q, days | Recent news on a topic: a short summary and up to 4 dated developments, newest first | $0.01 |
| research.market | question | Evidence brief for a prediction-market question: evidence for and against, key dates, resolution notes. No probability, forecast or trading advice | $0.03 |
| research.company | company | Short sourced brief on one company: what it does, facts, recent news | $0.02 |

On the plain-name endpoint the tools are called bob_research, bob_factcheck, bob_summarize, bob_extract, bob_search, bob_news, bob_market_research and bob_company_brief.

## HTTP API

The same eight products, at https://bob.assimilatethis.com:

- GET /research?q=...
- GET /factcheck?claim=...
- GET /summarize?url=...
- GET /extract?url=...
- GET /search?q=...&n=...&since=YYYY-MM-DD&until=YYYY-MM-DD
- GET /news?q=...&days=...
- GET /market-research?question=...
- GET /company-brief?company=...

Two market-data routes are web routes only for now (not MCP tools). Each call is paid with x402 like the others, and a call that fails is not charged:

- GET /perps?ticker=...  ($0.002): every Kalshi perpetual market in one call: bid, ask, spread, mark price, 24-hour volume, open interest and funding (per period, annualised, 30-day average). Exchange data refreshed every minute. Optional ticker returns one market.
- GET /indicators?coin=...&tf=...  ($0.003): SMA 20/50/200, EMA 12/26, RSI 14, MACD, ATR 14 and Bollinger bands for BTC, ETH, SOL, XRP, DOGE or AVAX on 15m, 1h, 4h or 1d candles. Standard formulas on public prices. Not a forecast or trading advice.

An unpaid request returns HTTP 402 with the payment requirements. Use any x402 client to pay and retry.

## Notes

- Typical response time is 3 to 9 seconds. If a request cannot be answered in time, you get an error and are not charged.
- Questions and claims are limited to 500 characters. URLs must be public http or https addresses.
- Answers come from live web search and page reading; check important facts against the sources returned.
- This repository is a public description of the service. It contains no source code.
