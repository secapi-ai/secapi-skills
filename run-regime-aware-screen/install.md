# Run Regime-Aware Screen

Use this for factor-rotation research in current country-level macro context. It reads the regime when needed, then returns factor leaders and laggards; it does not turn a macro label into a long-horizon thesis.

## Install and Connect

```bash
npx skills add secapi-ai/secapi-skills --skill run-regime-aware-screen
export SECAPI_API_KEY="your-api-key"
```

Add `--global` for a user-level install. Use `npx skills --help` to inspect the supported agent integration options.

## Make the First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/macro/regimes?country=US" \
  -H "x-api-key: $SECAPI_API_KEY"
```

Then ask: `Identify the current US macro regime and return factor-rotation research for US style factors.`

## What Good Looks Like

The response states the returned country, observation time, regime context, leaders, and laggards before interpretation. Preserve the returned rationale and disclosures when present, and keep factor-rotation research distinct from a durable business thesis. Regimes and rankings can change as data changes; record their observation time.

Read the [workflow](./SKILL.md) for the sequence and [metadata](./metadata.json) for triggers and declared endpoint dependencies.
