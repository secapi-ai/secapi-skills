# Write Country Regime Report

Use this for a country-specific macro brief grounded in the high-signal pack, regime state, and report workflow. It should connect observed data, release timing, forecasts, and watch items without blurring them together.

## Install and Connect

```bash
npx skills add secapi-ai/secapi-skills --skill write-country-regime-report
export SECAPI_API_KEY="your-api-key"
```

Add `--global` for a user-level install. Use `npx skills --help` to inspect supported agent integration options.

## Make the First Read

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/macro/high-signal-pack?country=JP" \
  -H "x-api-key: $SECAPI_API_KEY"
```

Then ask: `Write an allocator-style report on Japan. State the country and lookback, use the high-signal pack, and distinguish observed data from forecasts and estimated release timing.`

## What Good Looks Like

The report anchors the regime before explaining growth, inflation, labor, policy, and trade. It uses the official-source series identified by the high-signal pack where available and labels both forecast and release-date uncertainty. A country report is a dated research artifact, not a standing macro forecast.

Read the [workflow](./SKILL.md) for the process and [metadata](./metadata.json) for triggers and declared endpoint dependencies.
