---
name: run-regime-aware-screen
description: Researches factor rotation in a stated country's macro regime. Use when you need dated leaders and laggards with regime context, not an individual-security recommendation.
---

# Run Regime-Aware Screen

Place factor rotation in country and time context. Report the observed regime and screen output before interpreting either.

## First Read

```bash
curl --fail --silent --show-error https://api.secapi.ai/v1/strategies/factor-rotation \
  -H "x-api-key: $SECAPI_API_KEY" \
  -H "content-type: application/json" \
  -d '{"country":"US","category":"style","window":"1m","lookback":"6m","limit":5}'
```

The published request supports country, category, window, lookback, and limit. Use `GET /v1/macro/regimes` to add the country's returned regime context.

## What to provide

Give the agent a country, factor category, window, lookback, and desired result count. These settings determine the screen. The result is a dated ranking, not a substitute for issuer-level research.

## Research path

1. Read `GET /v1/macro/regimes?country=US` for the country in scope; it also accepts optional lookback controls.
2. Submit the factor-rotation request with the country, category, window, lookback, and limit you intend to report.
3. Preserve returned dates, country, ranking, regime context, rationale, and disclosures when supplied.

## Expected result

State the observation time, country, regime context, leaders, and laggards before offering interpretation. Explain the limits of the selected window and do not turn a ranking into a durable business thesis or investment recommendation. Rankings and regimes can change with the underlying data.
