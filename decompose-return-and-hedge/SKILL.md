---
name: decompose-return-and-hedge
description: Explains a security return over a stated window and evaluates hedge candidates as exposure trade-offs. Use when you need to separate model attribution from a hedge decision.
---

# Decompose Return and Hedge

Explain a return before discussing a hedge. Set the date window, report what the factor model explains, and keep issuer evidence separate from attribution output.

## First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/factors/decomposition?symbol=AAPL&lookback=6m" \
  -H "x-api-key: $SECAPI_API_KEY"
```

`symbol` is required. The API also supports optional `factors`, `keys`, `category`, `window`, `lookback`, `response_mode`, and `include` controls.

## What to provide

Give the agent a symbol, a precise date window or lookback, and the exposure question behind the hedge discussion. The skill evaluates trade-offs; it does not select a trade for the user.

## Research path

1. Run `GET /v1/factors/decomposition` for the stated symbol and window.
2. Use `GET /v1/stocks/{ticker}/loadings` to inspect reported position loadings.
3. Use `GET /v1/factors/exposures` or `GET /v1/factors/correlations` only when they clarify concentration or hedge overlap.
4. Bring in filing or company context through the routes declared in `metadata.json`, and cite it independently from the attribution model.

## Expected result

State the exact window, the model's explained and unexplained components, and any returned fit limitation. Present candidates as changes in exposures, concentration, and residual risk, not recommendations or guarantees. Distinguish factor attribution from filing facts, news, and causal explanation.
