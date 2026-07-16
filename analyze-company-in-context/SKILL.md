---
name: analyze-company-in-context
description: Builds a concise, evidence-aware issuer brief before deeper research. Use when the user needs the business, financial, factor, and macro context that could change an allocation decision.
---

# Analyze Company in Context

Build a short decision brief, not a diluted diligence memo. Establish the issuer and reporting period, then add only the business breakdown, factor exposure, or macro context that materially changes the question.

## First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/companies/overview?ticker=MSFT&include=segments,dilution" \
  -H "x-api-key: $SECAPI_API_KEY"
```

If the request starts with a name rather than a ticker or CIK, resolve it with `GET /v1/entities/resolve` before calling the issuer routes.

## Research Path

1. Read `GET /v1/companies/overview` using `ticker` or `cik`. Its optional `include` values are `segments`, `footnotes`, `dilution`, and `factors`.
2. Use `GET /v1/companies/segments` when product, geographic, or operating mix matters. It accepts `ticker` or `cik`, plus optional `period` and `segment_type`.
3. Add `GET /v1/factors/exposures` only when factor sensitivity belongs in the decision.
4. Use `GET /v1/macro/regimes` only when country regime context changes the interpretation.
5. Use the intelligence routes named in `metadata.json` as supporting bundles, and keep their returned context distinct from filing evidence.

## Deliverable

Lead with the issuer, the decision-relevant facts, and the open question. Follow with business mix, financial or filing context, and only the factor or macro overlays that matter. Name the report date and lookback. For every filing claim, retain the accession number, filing URL, and item, note, section, or page; label your conclusion as interpretation.

Do not turn a compact brief into a price target, a hedge instruction, or a substitute for full diligence.
