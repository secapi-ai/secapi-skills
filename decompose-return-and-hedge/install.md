# Decompose Return and Hedge

Use this skill when a stock move needs disciplined attribution and a hedge discussion framed as exposure trade-offs.

```bash
npx skills add secapi-ai/secapi-skills --skill decompose-return-and-hedge
export SECAPI_API_KEY="your-api-key"
```

First prompt:

```text
Decompose AAPL's last 6M return. State the exact window, report what the factor
model explains and does not explain, then assess hedge candidates as exposure trade-offs.
```

Read the [full instructions](./SKILL.md) before treating attribution as causality.
