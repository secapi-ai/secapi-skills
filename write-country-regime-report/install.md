# Write Country Regime Report

Use this skill to create a country macro brief that separates observed data from forecasts.

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

Read the [full instructions](./SKILL.md) for the high-signal-pack and regime sequence.
