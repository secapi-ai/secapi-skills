---
name: make-portfolio-factor-neutral
description: Analyzes portfolio factor exposures, proposes a neutralization, and validates the adjustment with stress tests. Use when the user has portfolio weights and needs to reduce factor concentration or evaluate a portfolio hedge.
---

# Make Portfolio Factor Neutral

## Quick Start

```bash
curl -s "${SECAPI_BASE_URL:-https://api.secapi.ai}/v1/portfolio/analyze" \
  -H "x-api-key: $SECAPI_API_KEY" \
  -H "content-type: application/json" \
  -d '{"country":"US","lookback":"6m","holdings":[{"symbol":"AAPL","weight":0.5},{"symbol":"MSFT","weight":0.5}]}'
```

## Endpoints

- `POST /v1/portfolio/analyze`
- `POST /v1/portfolio/optimize`
- `POST /v1/portfolio/stress-test`
- `GET /v1/model-portfolios/{portfolioId}/factor-view`

## Process

1. Run `portfolio/analyze` to identify top absolute exposures.
2. Run `portfolio/optimize` with `objective=factor_neutral`.
3. Validate the proposed hedge basket with `portfolio/stress-test`.
4. For canned examples or dashboards, use `model-portfolios/{portfolioId}/factor-view`.

## Example

Question: `Neutralize the factor exposures in my 50/50 AAPL/MSFT book.`

Suggested sequence:
- `POST /v1/portfolio/analyze` with the holdings to find the top absolute exposures
- `POST /v1/portfolio/optimize` with `objective=factor_neutral`
- `POST /v1/portfolio/stress-test` to validate the proposed hedge basket

## Output Format

1. Top exposures
2. Suggested hedge basket
3. Neutralization plan
4. Stress-test caveats

## Guidelines

- Require weights that sum to a sensible portfolio.
- Show the top 3-5 exposures first.
- Explain whether the recommendation is pure neutralization or a regime-aware compromise.
