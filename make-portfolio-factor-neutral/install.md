# Make Portfolio Factor Neutral

Use this skill when you have portfolio weights and need to see the trade-offs in reducing factor concentration.

```bash
npx skills add secapi-ai/secapi-skills --skill make-portfolio-factor-neutral
export SECAPI_API_KEY="your-api-key"
```

First prompt:

```text
Analyze a 50/50 AAPL/MSFT portfolio over 6M. Show the largest factor exposures,
propose a factor-neutral adjustment, and stress-test the resulting holdings.
State the country, lookback, objective, and scenario.
```

Read the [full instructions](./SKILL.md) for required holdings and scenario limits.
