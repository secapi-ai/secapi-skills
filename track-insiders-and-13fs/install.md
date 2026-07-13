# Track Insiders and 13Fs

Use this to examine company insider filings or a particular manager's reported 13F book. Those are different questions: insider data is issuer-level Form 3, 4, and 5 activity, while manager 13F analysis requires the filer's 10-digit CIK.

## Install and Connect

```bash
npx skills add secapi-ai/secapi-skills --skill track-insiders-and-13fs
export SECAPI_API_KEY="your-api-key"
```

Add `--global` for a user-level install. Inspect supported agent targets with `npx skills --help`.

## Make the First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/insiders?ticker=NVDA&forms=3,4,5" \
  -H "x-api-key: $SECAPI_API_KEY"
```

Then ask: `Summarize recent NVDA Form 3, 4, and 5 activity. Identify clusters or repeat actors, and cite the accession number and filing URL for each material transaction.`

## What Good Looks Like

The analysis names the reporting period, distinguishes transactions from institutional ownership, and does not imply that a delayed 13F filing is a live position. For manager comparisons, require a 10-digit filer CIK and two explicit reporting periods. A row dump is not an ownership thesis.

Read the [workflow](./SKILL.md) for the process and [metadata](./metadata.json) for triggers and declared endpoint dependencies.
