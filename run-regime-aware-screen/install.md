# Run Regime-Aware Screen

Use this for a tactical factor screen conditioned on a named macro backdrop. It first establishes the regime, then produces a shortlist or rotation view; it does not turn a macro label into a long-horizon thesis.

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

Then ask: `Identify the current US macro regime, report its confidence, and run a quality-factor screen for that backdrop.`

## What Good Looks Like

The response states the regime label, confidence, country, and period before interpreting the screen. It explains why a factor may fit that backdrop and keeps tactical rotation distinct from a durable business thesis. Regimes and rankings can change as data changes; record their observation time.

Read the [workflow](./SKILL.md) for the sequence and [metadata](./metadata.json) for triggers and declared endpoint dependencies.
