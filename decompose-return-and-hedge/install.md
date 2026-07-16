# Decompose Return and Hedge

Install this when a stock move needs a disciplined attribution and a hedge discussion framed as exposure trade-offs.

```bash
npx skills add secapi-ai/secapi-skills --skill decompose-return-and-hedge
export SECAPI_API_KEY="your-api-key"
```

First prompt:

```text
Decompose AAPL's last 6M return. State the exact window, report what the factor
model explains and does not explain, then assess hedge candidates as exposure trade-offs.
```

Read the [workflow](./SKILL.md) before treating attribution as causality.
