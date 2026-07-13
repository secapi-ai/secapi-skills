# Analyze Company in Context

Use this when an investor needs a fast, source-aware brief before deciding whether a company deserves deeper work. It starts with the issuer snapshot, then brings in segments, security context, earnings, factors, and macro only when they change the conclusion.

## Install and Connect

```bash
npx skills add secapi-ai/secapi-skills --skill analyze-company-in-context
export SECAPI_API_KEY="your-api-key"
```

Add `--global` to install for your user-level configuration. The Skills CLI chooses the supported agent integration; inspect its options with `npx skills --help` rather than relying on a client-specific command.

## Make the First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/companies/overview?ticker=MSFT&include=segments,dilution" \
  -H "x-api-key: $SECAPI_API_KEY"
```

Then ask: `Give me a fast allocator context pack on MSFT. Lead with the decision-relevant facts; separate filing evidence from interpretation.`

## What Good Looks Like

The answer identifies the issuer, its business and segment mix, the relevant security or earnings context, and only the factor or macro overlays that affect the case. Filing-derived numbers carry the response's accession number and filing URL. A context pack is not a full diligence memo or a hedge recommendation; escalate to the dedicated skills when that is the real task.

Read the [workflow](./SKILL.md) for the endpoint sequence and [metadata](./metadata.json) for discovery triggers and declared dependencies.
