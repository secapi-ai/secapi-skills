---
name: make-portfolio-factor-neutral
description: Measures factor exposure in a weighted portfolio and tests a constrained adjustment under stated scenarios. Use when you need to understand concentration or a proposed hedge's trade-offs.
---

# Make Portfolio Factor Neutral

Measure the portfolio before optimizing it. Require holdings with weights, state the country and lookback, then evaluate a proposed adjustment under explicit constraints and scenarios.

## First Read

```bash
curl --fail --silent --show-error https://api.secapi.ai/v1/portfolio/analyze \
  -H "x-api-key: $SECAPI_API_KEY" \
  -H "content-type: application/json" \
  -d '{"country":"US","lookback":"6m","holdings":[{"symbol":"AAPL","weight":0.5},{"symbol":"MSFT","weight":0.5}]}'
```

`holdings` is required; each holding has a `symbol` and `weight`. The portfolio routes also support country, lookback, category, and factor-key controls.

## What to provide

Give the agent the holdings and weights, country, lookback, objective, and constraints. Weights should represent the portfolio you want analyzed; an optimizer cannot infer omitted holdings, taxes, liquidity, or trading costs.

## Research path

1. Submit the actual or proposed book to `POST /v1/portfolio/analyze`.
2. Use `POST /v1/portfolio/optimize` with the stated objective. `factor_neutral`, `min_drawdown`, and `regime_aware` are the published objective values.
3. Test the resulting holdings with `POST /v1/portfolio/stress-test`. Name the historical, named, or custom scenario used.
4. Keep the returned analysis and stress-test records with the proposed holdings so another reviewer can reproduce the scenario.

## Expected result

Show the largest exposures, proposed changes, remaining concentration, and scenario results. State the weights, country, lookback, objective, and constraints. An optimized output is scenario analysis, not a trade instruction or a promise of neutrality.
