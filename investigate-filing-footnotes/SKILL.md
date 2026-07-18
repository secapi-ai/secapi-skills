---
name: investigate-filing-footnotes
description: Investigates a defined accounting disclosure with source-linked findings. Use when a lease, tax, revenue-recognition, debt, covenant, or segment note needs filing evidence.
---

# Investigate Filing Footnotes

Turn an accounting question into a filing investigation. Define the note family and filing period first. Return disclosed evidence and its limits, not a generic accounting lecture.

## First Read

After installation, give the agent a concrete filing question:

```text
Investigate CRM's latest annual-report lease and revenue-recognition notes.
For each finding, identify the filing, accession number, filing URL, and note,
section, or page. Separate disclosed facts from interpretation.
```

## What to provide

Give the agent an issuer, a filing period or form when known, and the accounting question to investigate. A broad question such as "is accounting quality good?" is not a filing question; specify the note, metric, or change that needs evidence.

## Research path

1. Pin down issuer, filing form, reporting period, and note family.
2. Use the intelligence query endpoint to locate relevant filing material; use `GET /v1/companies/overview` only for issuer context.
3. Read the cited disclosure rather than extrapolating from a summary.
4. Record the exact filing and passage behind each finding. If the record is incomplete, say so.

## Expected result

Lead with the disclosure that matters and its financial or operating implication. Then list the supporting note evidence, changes across periods where the filings support comparison, and unresolved questions. Every filing claim needs accession number, filing URL, and note, item, section, or page. Label all analytical judgments as interpretation.

The result explains a disclosure and its open questions. It does not infer accounting quality or fraud from a footnote alone.
