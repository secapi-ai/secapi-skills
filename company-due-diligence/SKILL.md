---
name: company-due-diligence
description: Produces a filing-led company memo with business, financial, ownership, factor, and dilution context. Use when a company decision needs a traceable evidence trail.
---

# Company Due Diligence

Produce a company memo another investor can audit. Start from the issuer record, identify the reporting periods, and attach every material filing claim to its source. Do not fill evidence gaps with generic sector commentary.

## First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/companies/overview?ticker=NVDA&include=segments,footnotes,dilution" \
  -H "x-api-key: $SECAPI_API_KEY"
```

If the user supplies only a company name, call `GET /v1/entities/resolve` first. The company overview and segments routes accept `ticker` or `cik`.

## What to provide

Give the agent a ticker or CIK, the decision under review, and any period, ownership, or risk questions that matter. Resolve a company name before asking for issuer data.

## Research path

1. Establish identity, latest material filing, financial snapshot, and the requested enrichments with `GET /v1/companies/overview`.
2. Read `GET /v1/companies/segments` for reported business mix. Treat axes marked low confidence as a boundary, not a fact to smooth over.
3. Use `GET /v1/insiders` for Forms 3, 4, and 5, and `GET /v1/owners/institutional/ticker` for a ticker-centric disclosed-holder view. Report the filing or report date.
4. Use `GET /v1/owners/13f` only for a manager identified by CIK. That is a manager filing view, not a company-holder view.
5. Add `GET /v1/factors/exposures`, `GET /v1/factors/decomposition`, and `GET /v1/dilution/score` when those model outputs answer a stated question. They are not evidence of business causality.
6. Use the available filing and intelligence routes to locate supporting material. Preserve filing identifiers instead of paraphrasing an uncited conclusion.

## Expected result

Write: snapshot; business and segment mix; financial record; ownership; filing risks; dilution and factor context; thesis, risks, and open questions. State each reporting period and lookback. Every filing-derived statement needs accession number, filing URL, and item, note, section, or page. Separate disclosed fact, model output, and interpretation.

13F positions are historical disclosures. A model score or filing extract does not establish an investment conclusion.
