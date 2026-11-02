# Bob Research Tools

Paid web research tools for AI agents, available as a remote MCP server and as an HTTP API. Each call is paid in USDC with the x402 protocol, on Base or Solana. A call that fails is not charged.

## MCP server

- Address: https://bob.assimilatethis.com/mcp (streamable HTTP)
- Same ten tools with plain names, for clients that reject dots in tool names: https://bob.assimilatethis.com/flat/mcp
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
| weather.forecast | lat, lon | Current conditions and the National Weather Service 7-day forecast for a US latitude and longitude (nearest-station temperature, humidity, wind, pressure; up to 14 forecast periods). US government data | $0.003 |
| weather.alerts | lat, lon | Active National Weather Service warnings, watches and advisories for a US latitude and longitude. US government data | $0.002 |

On the plain-name endpoint the tools are called bob_research, bob_factcheck, bob_summarize, bob_extract, bob_search, bob_news, bob_market_research, bob_company_brief, bob_weather and bob_alerts.

## HTTP API

The same ten products, at https://bob.assimilatethis.com:

- GET /research?q=...
- GET /factcheck?claim=...
- GET /summarize?url=...
- GET /extract?url=...
- GET /search?q=...&n=...&since=YYYY-MM-DD&until=YYYY-MM-DD
- GET /news?q=...&days=...
- GET /market-research?question=...
- GET /company-brief?company=...

Two US weather routes use National Weather Service data (US government, public domain):

- GET /weather?lat=...&lon=...  ($0.003): current conditions at the nearest station plus the 7-day forecast (up to 14 periods) for a US point.
- GET /alerts?lat=...&lon=...  ($0.002): active warnings, watches and advisories for a US point.

An unpaid request returns HTTP 402 with the payment requirements. Use any x402 client to pay and retry.

## Free call and Bob Pass

- **One free call per caller.** Send the header `X-Bob-Preview: 1` (or add `?preview=1`) on any tool request, over HTTP or MCP. Every parameter must be present, and a failed call does not use it up. After that, each call is paid.
- **Bob Pass.** $10 in USDC for 30 days and 300 calls on any tool (market-research and company-brief count as 2). Buy it with an x402 payment at `GET /pass`; the key is shown once. Send it as the header `X-Bob-Pass: <key>` on any HTTP or MCP request and no per-call payment is needed. A failed call is not counted.
- Paying per call with x402 works exactly as before.

## Notes

- Typical response time is 3 to 9 seconds. If a request cannot be answered in time, you get an error and are not charged.
- Questions and claims are limited to 500 characters. URLs must be public http or https addresses.
- Answers come from live web search and page reading; check important facts against the sources returned.
- This repository is a public description of the service. It contains no source code.
