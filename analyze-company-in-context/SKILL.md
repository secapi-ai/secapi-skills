---
name: analyze-company-in-context
description: Builds a concise issuer brief before deeper research. Use when a business, financial, factor, or macro fact could change the next question.
---

# Analyze Company in Context

Build a short issuer brief before committing to a full diligence process. Start with a ticker or CIK and a reporting period. Add segment, factor, or macro context only when it changes the research question.

## First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/companies/overview?ticker=MSFT&include=segments,dilution" \
  -H "x-api-key: $SECAPI_API_KEY"
```

If the request starts with a name rather than a ticker or CIK, resolve it with `GET /v1/entities/resolve` before calling the issuer routes.

## What to provide

Give the agent a ticker or CIK, the question it should help answer, and a reporting period or lookback where it matters. A company name alone must be resolved before issuer routes can be used.

## Research path

1. Read `GET /v1/companies/overview` using `ticker` or `cik`. Its optional `include` values are `segments`, `footnotes`, `dilution`, and `factors`.
2. Use `GET /v1/companies/segments` when product, geographic, or operating mix matters. It accepts `ticker` or `cik`, plus optional `period` and `segment_type`.
3. Add `GET /v1/factors/exposures` only when factor sensitivity belongs in the decision.
4. Use `GET /v1/macro/regimes` only when country regime context changes the interpretation.
5. Use the security and earnings context endpoints as supporting material. Keep their returned context distinct from filing evidence.

## Expected result

Lead with the issuer, the decision-relevant facts, and the open question. Follow with business mix, financial or filing context, and only the factor or macro overlays that matter. Name the report date and lookback. For every filing claim, retain the accession number, filing URL, and item, note, section, or page; label your conclusion as interpretation.

The result is a scoping brief, not a price target, hedge instruction, or substitute for full diligence.
