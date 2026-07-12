---
name: investigate-filing-footnotes
description: Investigates filing footnotes and structured filing risk context using SEC API intelligence and semantic query planning. Use when the user asks about lease, tax, revenue-recognition, debt covenant, or segment-note issues.
---

# Investigate Filing Footnotes

## Quick Start

Use the semantic planner for the broad request, then follow with the company or security bundle if you need supporting context.

```bash
curl -s https://api.secapi.ai/v1/intelligence/query \
  -H "x-api-key: $SECAPI_API_KEY" \
  -H "content-type: application/json" \
  -d '{"query":"Investigate the lease, tax, and revenue-recognition footnotes for CRM."}'
```

## Endpoints

- `POST /v1/intelligence/query`
- `GET /v1/companies/overview?ticker=...`
- `GET /v1/intelligence/security?ticker=...`

## Process

1. Start with `intelligence/query` so the planner can classify the note investigation correctly.
2. If the user wants broader issuer context, pull `companies/overview`.
3. If the user wants market and hedge context around the same issuer, pull the security bundle.

## Example

Question: `What lease and revenue-recognition risks show up in CRM's latest 10-K?`

Suggested sequence:
- `POST /v1/intelligence/query` with `{"query":"Investigate the lease and revenue-recognition footnotes for CRM."}`
- `GET /v1/companies/overview?ticker=CRM` for supporting issuer context

## Guidelines

- Name the note families explicitly: lease, tax, revenue recognition, debt covenant, segment note.
- Keep a clear line between extracted note findings and your interpretation.
- Return traceable evidence, not generic accounting commentary: for every note finding, cite the source **accession number, filing URL, and the section/item** from the response `provenance` (e.g. `0000320193-25-000123 — 10-K Item 8, Note 5`). If a claim cannot be tied to a filing, label it inference, not fact.
