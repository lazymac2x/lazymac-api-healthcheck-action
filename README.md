# lazymac API Healthcheck Action

> ⭐ **Building in public from $0 MRR.** Star if you want to follow the journey — [lazymac-mcp](https://github.com/lazymac2x/lazymac-mcp) (42 tools, one MCP install) · [lazymac-k-mcp](https://github.com/lazymac2x/lazymac-k-mcp) (Korean wedge) · [lazymac-sdk](https://github.com/lazymac2x/lazymac-sdk) (TS client) · [api.lazy-mac.com](https://api.lazy-mac.com) · [Pro $29/mo](https://coindany.gumroad.com/l/zlewvz).

> A zero-dep GitHub Action that pings a REST/MCP API and fails the workflow on non-2xx, slow responses, or repeated errors. Drop into any pipeline.

[![GitHub Marketplace](https://img.shields.io/badge/GitHub%20Marketplace-Available-green)](https://github.com/marketplace/actions/lazymac-api-healthcheck)

## Why

API uptime monitoring shouldn't need a separate SaaS. Run this action on a 5-min cron and you have free per-endpoint uptime checks straight from GitHub Actions — alerting via the workflow notification you already have.

## Quickstart

```yaml
name: API Healthcheck
on:
  schedule:
    - cron: '*/5 * * * *'   # every 5 min
  workflow_dispatch:

jobs:
  ping:
    runs-on: ubuntu-latest
    steps:
      - uses: lazymac2x/lazymac-api-healthcheck-action@v1
        with:
          url: https://api.lazy-mac.com/qr-code
          expected-status: 200,204
          max-response-ms: 1500
          retries: 3
```

## Inputs

| Name | Default | Description |
|------|---------|-------------|
| `url` | — (required) | URL to ping |
| `expected-status` | `200` | Comma-separated list of acceptable HTTP codes |
| `timeout` | `10` | Per-request timeout (seconds) |
| `max-response-ms` | `0` | Fail if response time exceeds this. `0` disables |
| `headers` | `''` | Extra headers, one `Key: Value` per line |
| `retries` | `2` | Retry attempts on failure |

## Outputs

| Name | Description |
|------|-------------|
| `status` | HTTP status returned |
| `response-ms` | Response time (ms) |

## Use with the lazymac API hub

Built for [api.lazy-mac.com](https://api.lazy-mac.com) — 36+ developer APIs on Cloudflare Workers (REST + MCP). Free tier on every endpoint.

## License

MIT

<sub>💡 Host your own stack? <a href="https://m.do.co/c/c8c07a9d3273">Get $200 DigitalOcean credit</a> via lazymac referral link.</sub>
