---
name: track-insiders-and-13fs
description: Analyzes Form 3, 4, and 5 insider activity or compares a manager's reported 13F holdings across periods. Use when the user needs company insider activity or a manager's 13F changes, filing history, and style drift.
---

# Track Insiders And 13Fs

## Quick Start

```bash
curl -s "https://api.secapi.ai/v1/insiders?ticker=NVDA&forms=3,4,5" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## Endpoints

- `GET /v1/insiders?ticker=...&forms=3,4,5` — insider ownership and transactions across Form 3 (initial), Form 4 (changes), and Form 5 (annual). Filter with `transaction_code`, `owner_name`, `date_from`/`date_to`.
- `GET /v1/owners/13f?cik=...`
- `GET /v1/owners/13f/filings?cik=...`
- `POST /v1/owners/13f/compare`
- `POST /v1/intelligence/query`

## Process

1. Use `insiders` for company-level insider activity. Pass `ticker` (or `cik`) and `forms=3,4,5` to cover initial, change, and annual insider reports.
2. Use `owners/13f` and `owners/13f/filings` for a manager’s current and historical filings.
3. Use `owners/13f/compare` for style-drift or quarter-over-quarter ownership change analysis.
4. Use `intelligence/query` when the user asks for a narrative manager-change explanation.

## Example Compare Payload

```json
{
  "cik": "0001067983",
  "leftPeriod": { "year": 2025, "quarter": 4 },
  "rightPeriod": { "year": 2026, "quarter": 1 }
}
```

## Guidelines

- Require a 10-digit manager CIK for 13F comparisons.
- Distinguish insider activity from institutional ownership.
- Highlight clusters, repeat actors, and style drift rather than dumping rows.
- Cite the source accession number (and filing URL) from the response when you attribute a transaction or holding to a specific filing.
