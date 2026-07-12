---
name: analyze-company-in-context
description: Builds a company or security view using SEC API intelligence bundles, macro overlays, factor exposures, and earnings context. Use when the user asks for a company briefing, security overview, or allocator-style company summary.
---

# Analyze Company in Context

## Quick Start

Resolve the issuer and get the snapshot in one call with Company Overview, then pull deeper atomic routes only when needed.

```bash
curl -s "https://api.secapi.ai/v1/companies/overview?ticker=MSFT&include=segments,dilution" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## Endpoints

- `GET /v1/companies/overview?ticker=...&include=segments,footnotes,dilution` — issuer identity, latest material filing, and a 5-year financial snapshot in one call
- `GET /v1/companies/segments?ticker=...&segment_type=product|geographic|operating` — revenue / operating-income broken out by reportable segment and geography
- `GET /v1/intelligence/security?ticker=...`
- `GET /v1/intelligence/earnings-preview?ticker=...`
- `GET /v1/factors/exposures?symbols=...`
- `GET /v1/macro/regimes?country=...`

## Process

1. Start with `companies/overview` (it accepts `ticker` or `cik`) and capture the canonical `cik`. If you only have a company name, resolve it first with `GET /v1/entities/resolve?name=...`. Add `?include=segments,dilution` for an inline summary.
2. Pull `companies/segments` for the full multi-axis business breakdown when the question is about revenue mix, concentration, or geographic exposure.
3. Use `companies/overview` for issuer context, and `intelligence/security` when the question is about trading, return drivers, or hedge candidates.
4. Add `intelligence/earnings-preview` when the question is near a reporting window.
5. Pull factor exposures and macro regimes only if they change the answer.
6. Return a compact summary before showing supporting data.

## Output Format

1. Company summary
2. Key drivers and risks
3. Macro and factor context
4. Next-step questions or hedge ideas

## Example

Question: `Give me a fast context pack on NVDA for an allocator.`

Suggested sequence:
- `GET /v1/companies/overview?ticker=NVDA&include=segments,dilution`
- `GET /v1/intelligence/security?ticker=NVDA`
- `GET /v1/factors/exposures?symbols=NVDA`

## Guidelines

- Prefer Company Overview and the intelligence bundles over stitching many raw endpoints by default.
- Use `view=full` only when the caller explicitly wants the full payload.
- Keep the answer short unless the user asks for a deeper memo.
- When you quote a number that comes from a filing, cite the source accession number and filing URL (preserved in the response `provenance`); keep extracted filing facts separate from your interpretation.
