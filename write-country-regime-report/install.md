# Write Country Regime Report

Install this to create a country macro brief with observed data and forecast boundaries made explicit.

```bash
npx skills add secapi-ai/secapi-skills --skill write-country-regime-report
export SECAPI_API_KEY="your-api-key"
```

First prompt:

```text
Write an allocator-style report on Japan with a 6M horizon. State the country,
lookback, horizon, and report date. Separate observed data, estimates, forecasts,
and expected release timing, and preserve uncertainty where the source does not settle it.
```

Read the [workflow](./SKILL.md) for the high-signal-pack and regime sequence.
