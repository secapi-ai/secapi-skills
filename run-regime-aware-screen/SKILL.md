---
name: run-regime-aware-screen
description: Screens factors and candidates against the active macro regime. Use when the user asks for tightening-cycle screens, rate-sensitive ideas, or factor rotation suggestions under a named macro backdrop.
---

# Run Regime Aware Screen

## Quick Start

```bash
curl -s https://api.secapi.ai/v1/strategies/regime-screen \
  -H "x-api-key: $SECAPI_API_KEY" \
  -H "content-type: application/json" \
  -d '{"country":"US","lookback":"6m","category":"style"}'
```

## Endpoints

- `POST /v1/strategies/regime-screen`
- `POST /v1/strategies/factor-rotation`
- `GET /v1/macro/regimes?country=...`
- `GET /v1/factors/screen`

## Process

1. Pull the active regime with `macro/regimes`.
2. Run `regime-screen` for the shortlist.
3. Run `factor-rotation` when the user wants leaders vs laggards.
4. Use `factors/screen` for a broader factor leaderboard.

## Example

Prompt: `Run a regime-aware quality screen for tightening cycles.`

Preferred sequence:
- `GET /v1/macro/regimes?country=US`
- `POST /v1/strategies/regime-screen`

## Guidelines

- Always state the regime label and confidence.
- Explain why a factor is favored in that regime.
- Separate tactical screens from long-horizon thesis work.
