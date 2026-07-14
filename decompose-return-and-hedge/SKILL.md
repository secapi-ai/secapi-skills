---
name: decompose-return-and-hedge
description: Explains a security return over a stated period with factor attribution, loadings, and hedge-candidate analysis. Use when the user needs to understand what drove a stock move or compare hedges by their expected exposure trade-offs.
---

# Decompose Return and Hedge

## Quick Start

```bash
curl -s "${SECAPI_BASE_URL:-https://api.secapi.ai}/v1/factors/decomposition?symbol=AAPL&lookback=6m" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## Endpoints

- `GET /v1/factors/decomposition?symbol=...`
- `GET /v1/stocks/{ticker}/loadings`
- `GET /v1/intelligence/security?ticker=...`
- `POST /v1/intelligence/query`

## Process

1. Start with factor decomposition for the requested lookback.
2. Pull stock loadings when the user wants fit diagnostics or factor betas.
3. Pull the security intelligence bundle for filing-specific risks and hedge candidates.
4. Use `POST /v1/intelligence/query` when the user wants the fully composed allocator answer in one shot.

## Example Query Payload

```json
{
  "query": "Decompose AAPL's last 6M return into factors, macro drivers, filing-specific risks, then suggest hedges."
}
```

## Output Format

1. Main return drivers
2. Important loadings and diagnostics
3. Filing or macro overlays
4. Hedge candidates with expected exposure delta

## Guidelines

- Name the lookback window explicitly.
- Mention fit diagnostics when `rSquared` is weak.
- Distinguish factor-driven moves from filing/news-specific moves.
