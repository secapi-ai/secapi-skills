---
name: company-due-diligence
description: Produces a filing-led company due-diligence memo with business, financial, ownership, factor, and dilution context. Use when a company decision needs a traceable evidence trail.
---

# Company Due Diligence

Produce a defensible company memo. Start from the issuer record, identify the reporting periods, and make every material filing claim auditable. Do not fill gaps with generic sector commentary.

## First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/companies/overview?ticker=NVDA&include=segments,footnotes,dilution" \
  -H "x-api-key: $SECAPI_API_KEY"
```

If the user supplies only a company name, call `GET /v1/entities/resolve` first. The company overview and segments routes accept `ticker` or `cik`.

## Research Path

1. Establish identity, latest material filing, financial snapshot, and the requested enrichments with `GET /v1/companies/overview`.
2. Read `GET /v1/companies/segments` for reported business mix. Treat axes marked low confidence as a boundary, not a fact to smooth over.
3. Use `GET /v1/insiders` for Forms 3, 4, and 5, and `GET /v1/owners/institutional/ticker` for a ticker-centric disclosed-holder view. Report the filing or report date.
4. Use `GET /v1/owners/13f` only for a manager identified by CIK. That is a manager filing view, not a company-holder view.
5. Add `GET /v1/factors/exposures`, `GET /v1/factors/decomposition`, and `GET /v1/dilution/score` when those model outputs answer a stated question. They are not evidence of business causality.
6. Use the filing and intelligence routes declared in `metadata.json` to locate supporting material. Preserve filing identifiers instead of paraphrasing an uncited conclusion.

## Deliverable

Write: snapshot; business and segment mix; financial record; ownership; filing risks; dilution and factor context; thesis, risks, and open questions. State each reporting period and lookback. Every filing-derived statement needs accession number, filing URL, and item, note, section, or page. Separate disclosed fact, model output, and interpretation.

13F positions are historical disclosures. A favorable model score or a filing extract does not establish an investment conclusion.
