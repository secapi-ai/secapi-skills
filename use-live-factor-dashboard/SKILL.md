---
name: use-live-factor-dashboard
description: Monitors intraday factor returns, position loadings, correlations, and model-portfolio context. Use when the user needs a dated view of unusual factor movement and reported sensitivity.
---

# Use Live Factor Dashboard

Use the dashboard as a monitoring view: what is moving, when it was observed, and how a position's published loadings may be exposed. Do not imply a live trade signal.

## First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/factors/returns/intraday" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## Research Path

1. Start with `GET /v1/factors/returns/intraday` and retain the response timestamp and freshness state when supplied.
2. Inspect a position with `GET /v1/stocks/{ticker}/loadings`.
3. Use `GET /v1/factors/correlations` for concentration context, not a directional forecast.
4. Use `GET /v1/model-portfolios/{portfolioId}/factor-view` only when the relevant model-portfolio identifier is known.

## Deliverable

Show the unusual moves, the time observed, the position loadings that bear on sensitivity, and any stale, proxy, or degraded state returned by the API. Keep correlation and loading evidence separate from a claim about why a price moved. Intraday observations are not closing prices, execution instructions, or a guarantee of persistence.
