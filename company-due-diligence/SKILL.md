---
name: company-due-diligence
description: Produces a filing-cited company due-diligence memo covering business mix, ownership, factors, and dilution. Use for a company deep dive or pre-investment workup when the final memo needs traceable filing evidence.
---

# Company Due Diligence

## Quick Start

Always resolve the entity first with Company Overview, then layer the deeper reads.

```bash
# Resolve the issuer + snapshot in one call (capture the canonical CIK)
curl -s "https://api.secapi.ai/v1/companies/overview?ticker=NVDA&include=segments,dilution,footnotes" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## Endpoints

- `GET  /v1/entities/resolve?name=...` — resolve a company name (or ticker/cik/cusip/isin/figi) to the canonical entity. Only needed when you don't already have a ticker or CIK.
- `GET  /v1/companies/overview?ticker=...&include=segments,footnotes,dilution` — issuer identity, latest material filing, 5-year financial snapshot
- `GET  /v1/companies/segments?ticker=...&segment_type=product|geographic|operating` — revenue / operating-income by reportable segment and geography
- `GET  /v1/intelligence/earnings-preview?ticker=...` — near-reporting context
- `GET  /v1/factors/exposures?symbols=...` — factor exposures
- `GET  /v1/factors/decomposition?symbol=...` — return / factor decomposition
- `GET  /v1/insiders?ticker=...&forms=3,4,5` — Form 3/4/5 insider activity
- `GET  /v1/owners/institutional/ticker?ticker=...` — institutional (13F) holders **of the company** (use `reportDate` to compare periods)
- `POST /v1/intelligence/query` — semantic pull of 10-K Item 1 / 1A / 7 sections
- `GET  /v1/dilution/score?ticker=...` — dilution / share-count risk score with per-factor breakdown

## Process

1. **Resolve the entity.** `companies/overview` accepts only `ticker` or `cik`. If
   the user gives a company name, first call `entities/resolve?name=...` to get the
   canonical ticker/CIK, then call `companies/overview`. Capture the canonical `cik`
   and ticker and reuse them downstream — never guess a CIK.
2. **Overview + Segments.** Read `companies/overview` (business description,
   sector, size, financial snapshot) and `companies/segments` (revenue and
   operating income by reportable segment and geography). This frames the memo.
3. **Financials & ratios.** Use `companies/overview` for the financial summary
   and ratios; add `intelligence/earnings-preview` near a
   reporting window.
4. **Factors.** Pull `factors/exposures` for the symbol, then
   `factors/decomposition` to attribute recent return to factor vs idiosyncratic.
5. **Ownership / insiders.** Pull `insiders` with `forms=3,4,5` (recent buys and
   sells, clusters, repeat actors) and `owners/institutional/ticker` for the
   company's top institutional (13F) holders. Compare two `reportDate` periods to
   flag accumulation or exits. (Use `owners/13f?cik=` only when analyzing a
   specific *manager's* portfolio — it is keyed by the filer's CIK, not the issuer.)
6. **Filings & sections.** Use `intelligence/query` to extract 10-K **Item 1**
   (business), **Item 1A** (risk factors), and **Item 7** (MD&A). Capture the
   source accession number and filing URL for every claim pulled here.
7. **Dilution.** Pull `dilution/score` and flag the share-count trajectory and
   the highest-weighted dilution factors from the breakdown.
8. **Synthesize the DD memo** (Output Format below). Every material claim must
   carry a provenance reference.

## Output Format (cited DD memo)

1. **Snapshot** — name, ticker, CIK, sector, size (from Overview).
2. **Business & Segments** — what they do; revenue / operating income by segment and geography.
3. **Financials & Ratios** — growth, margins, balance sheet, key ratios.
4. **Factor Profile** — exposures + return decomposition (factor vs idiosyncratic).
5. **Ownership** — insider Form 3/4/5 signal; top institutional (13F) holders of the company + period drift.
6. **Filing Risks** — 10-K Item 1A / Item 7 findings, each cited.
7. **Dilution** — dilution score, band, and the dominant factors driving it.
8. **DD Verdict** — strengths, risks, open questions.
9. **Sources** — every cited filing with **accession number + filing URL + page/section**
   (e.g. `0001045810-26-000123 — 10-K Item 1A, p.27`).

## Example

Question: `Do full due diligence on NVDA.`

Suggested sequence:
- `GET /v1/companies/overview?ticker=NVDA&include=segments,dilution,footnotes` (capture the CIK)
- `GET /v1/companies/segments?ticker=NVDA`
- `GET /v1/factors/exposures?symbols=NVDA`, then `GET /v1/factors/decomposition?symbol=NVDA`
- `GET /v1/insiders?ticker=NVDA&forms=3,4,5` and `GET /v1/owners/institutional/ticker?ticker=NVDA`
- `POST /v1/intelligence/query` for 10-K Item 1A / Item 7, then `GET /v1/dilution/score?ticker=NVDA`

## Provenance (the differentiator)

- Every quantitative or qualitative claim sourced from a filing MUST cite the
  **accession number, the filing URL, and the specific page or Item/section**
  (all preserved in the response `provenance`).
- Prefer the structured Overview / Segments numbers over re-deriving from raw
  filings; when you quote a filing, cite the exact filing page.
- Keep extracted filing facts strictly separate from your interpretation.
- If a fact cannot be tied to a filing or an Overview / Segments field, label it
  as inference, not fact.

## Guidelines

- Resolve the entity before any deep call; pass the resolved ticker/CIK downstream.
- `companies/overview`, `companies/segments`, `insiders`, and
  `owners/institutional/ticker` all accept a `ticker`; only manager-level
  `owners/13f` requires a 10-digit filer CIK.
- Lead with the verdict and snapshot; show supporting data after.
- Name lookback windows and reporting periods explicitly.
- Tolerate `503` from the beta-gated factor surface and `429` from segmented
  statements — retry with backoff rather than failing the whole memo.
