# Investigate Filing Footnotes

Use this when the investment question lives in the notes: lease commitments, taxes, revenue recognition, covenants, or segments. It turns a broad question into a filing investigation, not generic accounting commentary.

## Install and Connect

```bash
npx skills add secapi-ai/secapi-skills --skill investigate-filing-footnotes
export SECAPI_API_KEY="your-api-key"
```

Add `--global` for a user-level install. Use `npx skills --help` to verify the agent targets supported by your CLI version.

## Make the First Read

```bash
curl --fail --silent --show-error https://api.secapi.ai/v1/intelligence/query \
  -H "x-api-key: $SECAPI_API_KEY" \
  -H "content-type: application/json" \
  -d '{"query":"Investigate the lease and revenue-recognition footnotes for CRM."}'
```

Then ask: `What lease and revenue-recognition risks appear in CRM's latest 10-K? Cite each finding with its accession number, filing URL, and note or section.`

## What Good Looks Like

The answer identifies the exact note family, records which filing it examined, and keeps disclosed facts separate from analytical judgment. It should say when the evidence is incomplete rather than generalizing from another issuer or period.

Read the [workflow](./SKILL.md) for the process and [metadata](./metadata.json) for triggers and declared endpoint dependencies.
