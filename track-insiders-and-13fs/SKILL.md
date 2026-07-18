---
name: track-insiders-and-13fs
description: Reviews issuer insider filings or a manager's reported 13F history. Use when you need Form 3, 4, or 5 activity, or a dated manager ownership comparison.
---

# Track Insiders And 13Fs

Separate two jobs: issuer-level insider transactions and manager-level 13F reports. Both are filings, and neither is a live-position feed.

## First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/insiders?ticker=NVDA&forms=3,4,5" \
  -H "x-api-key: $SECAPI_API_KEY"
```

`GET /v1/insiders` accepts issuer `ticker` or `cik`, plus `forms`, `date_from`, `date_to`, `owner_name`, `owner_cik`, `transaction_code`, and pagination filters.

## What to provide

For insider activity, give the agent an issuer ticker or CIK and a filing-date window. For 13F work, give it the reporting manager's CIK. Do not substitute an issuer CIK for a manager CIK.

## Research path

1. Use `GET /v1/insiders` for Forms 3, 4, and 5 linked to an issuer. Record the filing-date window.
2. Use `GET /v1/owners/13f?cik=...` and `GET /v1/owners/13f/filings?cik=...` for a manager's reported holdings and filing history. Manager CIK is required.
3. Use `POST /v1/owners/13f/compare` with the manager CIK to compare the latest two parsable reports. Do not invent a date-pair parameter that the public contract does not expose.
4. Cite the accession number and filing URL whenever a transaction or holding is attributed to a filing.

## Expected result

Report the issuer or manager identity, filing and report dates, material changes, and uncertainty. Highlight coherent clusters or repeated activity only when the filing record supports it. Do not present a delayed 13F or an insider row as a current position, motive, or ownership thesis.
