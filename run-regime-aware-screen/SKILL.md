---
name: run-regime-aware-screen
description: Compares factor-rotation leaders and laggards in a country's current macro context. Use when the user needs country-specific factor-rotation research anchored to the current macro regime.
---

# Run Regime Aware Screen

## Quick Start

```bash
curl --fail --silent --show-error https://api.secapi.ai/v1/strategies/factor-rotation \
  -H "x-api-key: $SECAPI_API_KEY" \
  -H "content-type: application/json" \
  -d '{"country":"US","category":"style","window":"1m","lookback":"6m","limit":5}'
```

## Endpoints

- `POST /v1/strategies/factor-rotation`
- `GET /v1/macro/regimes?country=...`

## Process

1. Read `macro/regimes` for the country when you need to record its current macro context.
2. Post the country, category, window, lookback, and limit to `factor-rotation`.
3. Use the response's leaders, laggards, regime, and `asOf` fields in the research summary.

## Example

Prompt: `For US style factors, return factor-rotation research with current macro-regime context.`

Preferred sequence:
- `GET /v1/macro/regimes?country=US`
- `POST /v1/strategies/factor-rotation`

## Guidelines

- Report the returned country, `asOf`, regime fields, leaders, and laggards.
- Preserve the response rationale and disclosures when present.
- Treat the result as factor-rotation research, not an individual-security screen or investment recommendation.
