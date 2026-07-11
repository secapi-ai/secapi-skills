---
name: underwrite-special-situation
description: Underwrites one SEC-derived special situation using its deal summary, full per-filing timeline, key dates, lifecycle status, and cited source filings. Use when the user gives a situation ID or asks for a deal memo, probability tree, catalyst map, spread-risk review, or single-situation workup.
---

# Underwrite Special Situation

## Setup

Use the public REST API for now. The published `@secapi/cli` release does not yet include the `situations` command group; only use those CLI commands after `secapi situations --help` lists them in your installed version.

```bash
export SECAPI_API_KEY="your-api-key"
```

Use `x-api-key: $SECAPI_API_KEY` for raw HTTP calls. Never pass API keys as command-line arguments.

## Quick Start

```bash
curl -s "https://api.secapi.ai/v1/situations/sit_abc123/summary" -H "x-api-key: $SECAPI_API_KEY"
curl -s "https://api.secapi.ai/v1/situations/sit_abc123" -H "x-api-key: $SECAPI_API_KEY"
curl -s "https://api.secapi.ai/v1/situations/sit_abc123/filings?limit=100" -H "x-api-key: $SECAPI_API_KEY"
```

Raw API equivalent:

```bash
curl -s "https://api.secapi.ai/v1/situations/sit_abc123" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## Supported Public Surfaces

- API: `GET /v1/situations/{situation_id}`, `GET /v1/situations/{situation_id}/summary`, `GET /v1/situations/{situation_id}/filings`, `GET /v1/situations/performance`
- MCP: `situations.get`, `situations.performance`

MCP currently does not expose `situations.summary` or `situations.filings`; use the raw API for those sub-resources.

## Endpoints

- `GET /v1/situations/{situation_id}` - one situation with its full per-filing timeline.
- `GET /v1/situations/{situation_id}/summary` - compact rendered markdown, deal terms, and latest timeline event.
- `GET /v1/situations/{situation_id}/filings` - paginated timeline sub-resource, oldest first.
- `GET /v1/situations/performance` - closed-situation cohorts for base-rate context.
- `GET /v1/situations/feed` - optional check for latest updates affecting the same ticker or type.

## Process

1. **Identify the situation.** If the user gives a ticker or form instead of an ID, first use `discover-special-situations` style calls to select the correct `situation_id`.
2. **Pull the compact summary.** Use `summary` for the rendered thesis, headline deal terms, latest event, and fast orientation.
3. **Hydrate the detail.** Use `get` for the full timeline and structured fields: type, subtype, status, terms, key dates, market snapshot, source accessions, and verification fields.
4. **Page filings when the timeline is long.** Use `filings` to inspect each event in order. Capture accession numbers, form types, filing URLs, event titles, and event summaries.
5. **Build the underwriting frame.** Separate facts from judgment: terms, dates, parties, and status are facts; probability, break price, and spread compensation are analyst estimates unless returned by the API.
6. **Use base rates carefully.** Pull `performance` for the same type or subtype when the user asks about odds, but present it as historical context, not a prediction.
7. **Name missing evidence.** If consideration, premium, financing, vote timing, regulatory status, or termination fees are absent from the API response, say so directly.

## Output Format

1. **Verdict First** - one paragraph on the current setup, major risk, and what would change the view.
2. **Situation Snapshot** - situation ID, issuer, ticker, type/subtype, status, latest event time, and key dates.
3. **Deal Terms** - counterparty, consideration, price, premium, deal value, stake, and any missing terms.
4. **Timeline** - accession-cited event chronology with form type, date, title, and why it mattered.
5. **Catalyst Map** - upcoming votes, expiries, record dates, expected close, and monitoring triggers.
6. **Underwriting Tree** - base case, upside/close case, downside/break case, and key uncertainties. Label estimates as estimates.
7. **Base-Rate Context** - optional closed-cohort performance, with type/subtype and window stated.
8. **Sources** - situation ID plus accession numbers and filing URLs used.

## Examples

```bash
# Fast memo inputs
curl -s "https://api.secapi.ai/v1/situations/sit_abc123/summary" -H "x-api-key: $SECAPI_API_KEY"
curl -s "https://api.secapi.ai/v1/situations/sit_abc123" -H "x-api-key: $SECAPI_API_KEY"

# Full source chronology
curl -s "https://api.secapi.ai/v1/situations/sit_abc123/filings?limit=100" -H "x-api-key: $SECAPI_API_KEY"

# Historical context
curl -s "https://api.secapi.ai/v1/situations/performance?types=merger&window=365d&group_by=subtype" -H "x-api-key: $SECAPI_API_KEY"
```

## Pending Surface: Weekly Issues

Pending datastream PR #1363 adds a weekly issue/archive foundation. Do not use issue/archive endpoints or claim a situation appeared in a numbered issue unless that PR has merged, deployed, and the public docs for your target environment list the issue endpoints. Before then, cite the situation timeline and filings directly.

## Guidelines

- Cite accession numbers and filing URLs for all deal terms, key dates, and lifecycle-status changes.
- Do not invent probability, spread, financing, regulatory, break-price, or termination-fee details.
- Distinguish the API's `status` from your risk view.
- If the user asks for investment advice, frame outputs as research support, not a recommendation.
- Use only documented public SEC API endpoints, CLI commands, or MCP tools.
