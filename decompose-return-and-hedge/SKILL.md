---
name: decompose-return-and-hedge
description: Attributes a security return over a stated window and evaluates hedge candidates as factor-exposure trade-offs. Use when the question is what moved, what the model explains, and what risks a hedge changes.
---

# Decompose Return and Hedge

Explain the return before discussing a hedge. Set the date window, report what the factor model explains, and keep issuer evidence separate from attribution output.

## First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/factors/decomposition?symbol=AAPL&lookback=6m" \
  -H "x-api-key: $SECAPI_API_KEY"
```

`symbol` is required. The API also supports optional `factors`, `keys`, `category`, `window`, `lookback`, `response_mode`, and `include` controls.

## Research Path

1. Run `GET /v1/factors/decomposition` for the stated symbol and window.
2. Use `GET /v1/stocks/{ticker}/loadings` to inspect reported position loadings.
3. Use `GET /v1/factors/exposures` or `GET /v1/factors/correlations` only when they clarify concentration or hedge overlap.
4. Bring in filing or company context through the routes declared in `metadata.json`, and cite it independently from the attribution model.

## Deliverable

State the exact window, the model's explained and unexplained components, and any fit limitation returned by the route. Present hedge candidates as changes in exposures, concentration, and residual risk; do not call them recommendations or guarantees. Distinguish factor attribution from filing facts, news, and causal explanation.
