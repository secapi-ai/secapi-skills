---
name: write-country-regime-report
description: Writes a dated country macro report from official-source data, regime context, and release metadata. Use when the user needs a country macro brief or regime memo that separates observed data from forecasts and release timing.
---

# Write Country Regime Report

## Quick Start

```bash
curl -s "https://api.secapi.ai/v1/macro/high-signal-pack?country=JP" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## Endpoints

- `GET /v1/macro/high-signal-pack?country=...`
- `GET /v1/macro/regimes?country=...`
- `POST /v1/intelligence/country-report`
- `POST /v1/intelligence/query`

## Process

1. Fetch the high-signal pack to understand source coverage and canonical series.
2. Fetch the regime to anchor the report.
3. Generate the country report for the requested lookback.
4. Use `intelligence/query` only when the user wants a more narrative allocator memo.

## Output Format

1. Regime summary
2. Growth, inflation, labor, policy, and trade drivers
3. Releases and forecast context
4. Risks and watch items

## Example

Question: `Write an allocator-style macro report on Japan.`

Suggested sequence:
- `GET /v1/macro/high-signal-pack?country=JP`
- `GET /v1/macro/regimes?country=JP`
- `POST /v1/intelligence/country-report` for the written report

## Guidelines

- Cite the country and lookback explicitly.
- Prefer the official-source series listed in the high-signal pack.
- Distinguish observed data from forecast or estimated release timing.
