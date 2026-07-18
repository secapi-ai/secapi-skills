---
name: write-country-regime-report
description: Writes a dated country macro brief from the high-signal pack and regime context. Use when observed data, release timing, and uncertainty must be separated from forecast.
---

# Write Country Regime Report

Write a country brief that can be revisited later. Identify the country, observation date, lookback, and source boundary before synthesizing growth, inflation, labor, policy, and trade.

## First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/macro/high-signal-pack?country=JP" \
  -H "x-api-key: $SECAPI_API_KEY"
```

The high-signal pack and `GET /v1/macro/regimes` accept a country; both also expose published `response_mode` and `include` controls.

## What to provide

Give the agent a country, lookback, horizon, and the decision the report should inform. The report should identify what was observed and when; it should not conceal forecasts inside a regime label.

## Research path

1. Read `GET /v1/macro/high-signal-pack` to establish the data and source context available for the country.
2. Read `GET /v1/macro/regimes` with the country and, where relevant, a stated lookback.
3. Use `POST /v1/intelligence/country-report` to assemble the report. Its published request supports `country`, `lookback`, `symbols`, `holdings`, `horizon`, and `briefingMode`.
4. Keep observed releases, estimates, forecasts, and expected release timing in separate statements.

## Expected result

Lead with the dated regime summary. Cover growth, inflation, labor, policy, trade, and watch items only where the returned evidence supports them. Name the country, lookback, horizon, and report timestamp. Prefer the source context supplied by the high-signal pack; label forecasts and release-date uncertainty. A country report is a dated research artifact, not a standing macro forecast.
