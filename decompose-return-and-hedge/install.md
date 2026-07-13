# Decompose Return and Hedge

Use this to explain a security's return over a named period and assess possible hedges. It is an attribution workflow: it should distinguish factor contributions from issuer-specific overlays instead of giving a post-hoc market story.

## Install and Connect

```bash
npx skills add secapi-ai/secapi-skills --skill decompose-return-and-hedge
export SECAPI_API_KEY="your-api-key"
```

Use `--global` for a user-level install. Confirm your supported agent targets with `npx skills --help`.

## Make the First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/factors/decomposition?symbol=AAPL&lookback=6m" \
  -H "x-api-key: $SECAPI_API_KEY"
```

Then ask: `Decompose AAPL's last 6M return. State the lookback, report fit diagnostics, separate factor and issuer-specific drivers, then evaluate hedge candidates.`

## What Good Looks Like

The output names the window, reports weak fit instead of hiding it, and labels hedge candidates as exposure trade-offs rather than recommendations. Filing or news context must be sourced distinctly from factor attribution. A decomposition cannot establish causality or guarantee hedge performance.

Read the [workflow](./SKILL.md) for the sequence and [metadata](./metadata.json) for triggers and declared endpoint dependencies.
