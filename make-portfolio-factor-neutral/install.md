# Make Portfolio Factor Neutral

Use this when you have actual portfolio weights and want to understand or reduce factor concentration. The workflow analyzes the book, proposes a factor-neutral optimization, and stress-tests the proposed change.

## Install and Connect

```bash
npx skills add secapi-ai/secapi-skills --skill make-portfolio-factor-neutral
export SECAPI_API_KEY="your-api-key"
```

Add `--global` for a user-level install. Confirm supported agent targets in your version with `npx skills --help`.

## Make the First Read

```bash
curl --fail --silent --show-error https://api.secapi.ai/v1/portfolio/analyze \
  -H "x-api-key: $SECAPI_API_KEY" \
  -H "content-type: application/json" \
  -d '{"country":"US","lookback":"6m","holdings":[{"symbol":"AAPL","weight":0.5},{"symbol":"MSFT","weight":0.5}]}'
```

Then ask: `Analyze this 50/50 AAPL/MSFT portfolio, show the largest factor exposures, propose a neutralization, and stress-test the adjustment.`

## What Good Looks Like

The answer checks that weights describe a coherent portfolio, names the country and lookback, and shows the largest exposures before presenting a hedge basket. It distinguishes pure factor neutralization from a regime-aware compromise. Optimization and stress-test output are scenario analysis, not a trade instruction or a promise of neutrality.

Read the [workflow](./SKILL.md) for the sequence and [metadata](./metadata.json) for triggers and declared endpoint dependencies.
