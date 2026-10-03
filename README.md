# Bob Research Tools

Paid web research tools for AI agents, available as a remote MCP server and as an HTTP API. Each call is paid in USDC with the x402 protocol, on Base or Solana. A call that fails is not charged.

## MCP server

- Address: https://bob.assimilatethis.com/mcp (streamable HTTP)
- Registry name: com.assimilatethis.bob/research-tools
- Listing the tools is free. Each tool call needs an x402 payment.

| Tool | Input | What it does | Price |
| --- | --- | --- | --- |
| bob_research | q | Answers a research question from the live web, with source URLs | $0.01 |
| bob_factcheck | claim | Checks a claim against the live web: supported, contradicted or unclear, with sources | $0.01 |
| bob_summarize | url | 80-word summary of a web page with key points | $0.005 |
| bob_extract | url | Clean markdown of a page's main content (up to 8,000 characters) | $0.005 |

## HTTP API

The same four products, at https://bob.assimilatethis.com:

- GET /research?q=...
- GET /factcheck?claim=...
- GET /summarize?url=...
- GET /extract?url=...

An unpaid request returns HTTP 402 with the payment requirements. Use any x402 client to pay and retry.

## Notes

- Typical response time is 3 to 9 seconds. If a request cannot be answered in time, you get an error and are not charged.
- Questions and claims are limited to 500 characters. URLs must be public http or https addresses.
- Answers come from live web search and page reading; check important facts against the sources returned.
- This repository is a public description of the service. It contains no source code.
