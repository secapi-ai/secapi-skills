---
name: investigate-filing-footnotes
description: Investigates a defined accounting disclosure with source-linked findings. Use when lease, tax, revenue-recognition, debt, covenant, or segment notes could change the investment case.
---

# Investigate Filing Footnotes

Turn an accounting question into a filing investigation. Define the note family and filing period first; return the disclosed evidence and its limits, not a generic accounting lecture.

## First Read

Install the skill, then ask the agent to locate the relevant filing material through the intelligence workflow declared in `metadata.json`:

```text
Investigate CRM's latest annual-report lease and revenue-recognition notes.
For each finding, identify the filing, accession number, filing URL, and note,
section, or page. Separate disclosed facts from interpretation.
```

## Research Path

1. Pin down issuer, filing form, reporting period, and note family.
2. Use the intelligence query route to locate relevant filing material; use `GET /v1/companies/overview` only for issuer context.
3. Read the cited disclosure rather than extrapolating from a summary.
4. Record the exact filing and passage behind each finding. If the record is incomplete, say so.

## Deliverable

Lead with the disclosure that matters and its financial or operating implication. Then list the supporting note evidence, changes across periods where the filings support comparison, and unresolved questions. Every filing claim needs accession number, filing URL, and note, item, section, or page. Label all analytical judgments as interpretation.

The skill investigates disclosures; it does not infer accounting quality or fraud from a footnote alone.
