---
name: use-live-factor-dashboard
description: Uses SEC API intraday factor returns, stock loadings, and model-portfolio views to power a live factor dashboard. Use when the user asks for live factor performance, intraday anomalies, or dashboard-style factor monitoring.
---

# Use Live Factor Dashboard

## Quick Start

```bash
curl -s "${SECAPI_BASE_URL:-https://api.secapi.ai}/v1/factors/returns/intraday" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## Endpoints

- `GET /v1/factors/returns/intraday`
- `GET /v1/stocks/{ticker}/loadings`
- `GET /v1/model-portfolios/{portfolioId}/factor-view`
- `GET /v1/factors/correlations`

## Process

1. Pull `factors/returns/intraday` for the live leaderboard.
2. Pull stock loadings for the positions the user clicks into.
3. Pull model-portfolio factor view for the portfolio panel.
4. Pull factor correlations if the dashboard needs cluster/risk context.

## Dashboard Notes

- Show z-scores and leverage when present.
- Use stock loadings diagnostics to explain why a position is sensitive to a factor move.

## Example

Question: `What factors are moving now, and why is NVDA sensitive?`

Suggested sequence:
- `GET /v1/factors/returns/intraday` for the live leaderboard
- `GET /v1/stocks/NVDA/loadings` to explain the position's factor sensitivity

## Guidelines

- Call out stale or proxy-based intraday data clearly.
- Keep the live panel compact and numerically dense.
- Let users drill from factor -> portfolio -> position without changing terminology.
