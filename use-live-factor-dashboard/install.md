# Use Live Factor Dashboard

Use this for a compact view of factor moves, the loadings behind a position, and correlation or model-portfolio context. It is a monitoring workflow, not a claim that the intraday signal is final.

## Install and Connect

```bash
npx skills add secapi-ai/secapi-skills --skill use-live-factor-dashboard
export SECAPI_API_KEY="your-api-key"
```

Add `--global` for a user-level install. Confirm the agent options your CLI supports with `npx skills --help`.

## Make the First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/factors/returns/intraday" \
  -H "x-api-key: $SECAPI_API_KEY"
```

Then ask: `What factors are moving now, which are most unusual, and why is NVDA sensitive? Flag stale or proxy-based intraday data explicitly.`

## What Good Looks Like

The output keeps the live panel numerically dense, connects a factor move to position loadings, and uses correlations only as risk context. Record the response timestamp and call out a stale or proxy-based series when the response indicates one. Intraday returns are not a closing-price record or an execution signal.

Read the [workflow](./SKILL.md) for the sequence and [metadata](./metadata.json) for triggers and declared endpoint dependencies.
