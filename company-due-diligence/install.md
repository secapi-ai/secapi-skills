# Company Due Diligence

Use this for an investable company workup, not a generic company summary. The workflow connects business mix, financial snapshot, factors, ownership, filing sections, and dilution into one memo with a visible evidence trail.

## Install and Connect

```bash
npx skills add secapi-ai/secapi-skills --skill company-due-diligence
export SECAPI_API_KEY="your-api-key"
```

Add `--global` for a user-level install. The Skills CLI handles supported agent targets; run `npx skills --help` to see the options available in your installed version.

## Make the First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/companies/overview?ticker=NVDA&include=segments,dilution,footnotes" \
  -H "x-api-key: $SECAPI_API_KEY"
```

Then ask: `Prepare a due-diligence memo on NVDA. Separate filing facts from interpretation, and cite every filing-derived claim with accession number, filing URL, and item or page.`

## What Good Looks Like

The resulting memo names the reporting periods it uses, distinguishes company-level institutional ownership from a manager's 13F portfolio, and ends with open questions rather than manufactured conviction. Filing claims must retain the response `provenance`; a factor exposure or dilution score is model output, not a substitute for the cited underlying evidence.

Read the [workflow](./SKILL.md) for the full process and [metadata](./metadata.json) for triggers and declared endpoint dependencies.
