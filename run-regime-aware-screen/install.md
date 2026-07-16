# Run Regime-Aware Screen

Install this for factor-rotation research that records its macro and timing context.

```bash
npx skills add secapi-ai/secapi-skills --skill run-regime-aware-screen
export SECAPI_API_KEY="your-api-key"
```

First prompt:

```text
Identify the current US macro regime, then screen US style-factor rotation over
a 1M window with a 6M lookback. State the observation time, country, regime,
leaders, laggards, and any returned rationale or disclosures.
```

Use the [workflow](./SKILL.md) to keep the screen distinct from an investment thesis.
