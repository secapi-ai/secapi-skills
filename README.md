# SEC API Skills

Give an agent a disciplined way to research SEC filings, ownership disclosures, factor exposure, and macro context with [SEC API](https://secapi.ai). Each skill defines a specific research job, the evidence to retain, and the limits the agent should state before it draws a conclusion.

The shortest path is to install one skill, provide an API key to the agent runtime, and ask a concrete question. Skills help structure research. They are not investment advice and do not replace reading the cited filing.

## Install a skill

Install the skill that matches the question in the project where your agent runs:

```bash
npx skills add secapi-ai/secapi-skills --skill company-due-diligence
export SECAPI_API_KEY="your-api-key"
```

Then give the agent a question with an evidence standard:

```text
Prepare a due-diligence memo on NVDA. State the reporting periods used.
Separate disclosed facts from interpretation, and cite each filing claim with
the accession number, filing URL, and relevant item, note, or page.
```

SEC API reads the key from the `x-api-key` header. Keep `SECAPI_API_KEY` in the agent runtime or a secret manager. Do not put it in a prompt, browser client, or checked-in file.

## Choose a skill

| Skill                                                                     | Job                                                                            | First prompt                                                           |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------- |
| [Analyze Company in Context](./analyze-company-in-context/SKILL.md)       | Decide what matters about an issuer before deeper work.                        | `Give me an allocator context pack on NVDA.`                           |
| [Company Due Diligence](./company-due-diligence/SKILL.md)                 | Write a filing-led memo with an auditable evidence trail.                      | `Run due diligence on NVDA and show the evidence trail.`               |
| [Decompose Return and Hedge](./decompose-return-and-hedge/SKILL.md)       | Separate modeled return attribution from a hedge decision.                     | `Decompose AAPL's last 6M return and assess hedge trade-offs.`         |
| [Investigate Filing Footnotes](./investigate-filing-footnotes/SKILL.md)   | Read a precise accounting disclosure in its filing context.                    | `Review CRM's latest lease and revenue-recognition notes.`             |
| [Make Portfolio Factor Neutral](./make-portfolio-factor-neutral/SKILL.md) | Measure portfolio exposure and test a constrained adjustment.                  | `Analyze this portfolio's factor exposures and test an adjustment.`    |
| [Run Regime-Aware Screen](./run-regime-aware-screen/SKILL.md)             | Compare factor rotation with dated country-regime context.                     | `Show US style-factor rotation in its current macro context.`          |
| [Track Insiders and 13Fs](./track-insiders-and-13fs/SKILL.md)             | Distinguish issuer insider activity from manager 13F history.                  | `Compare the latest two reported 13Fs for CIK 0001067983.`             |
| [Use Live Factor Dashboard](./use-live-factor-dashboard/SKILL.md)         | Read intraday factor moves alongside dated position loadings.                  | `What factors are moving now, and why is NVDA sensitive?`              |
| [Write Country Regime Report](./write-country-regime-report/SKILL.md)     | Produce a country brief that separates data from forecast.                     | `Write an allocator-style macro brief on Japan.`                       |

Each directory includes a short installation guide, a first prompt, and the full skill instructions.

## Confirm access

Use the Skills CLI to inspect supported agents or install the whole collection:

```bash
npx skills --help
npx skills add secapi-ai/secapi-skills --all
```

Before relying on a skill, make one authenticated request from the same environment as the agent:

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/companies/overview?ticker=AAPL" \
  -H "x-api-key: $SECAPI_API_KEY"
```

A successful response confirms access to that route. It does not establish coverage for every issuer, filing, derived dataset, or market-data product. For a failed request, retain the route, timestamp, HTTP status, error code, `Request-Id`, and `traceparent` when present. Never include the API key or private payload in a support request.

## What to retain

Treat filings, derived models, and market observations as different kinds of evidence. For a filing-backed statement, retain the accession number, filing URL, and the exact item, note, section, or page. Name report dates, lookbacks, and response timestamps. Label interpretation, forecast, and model output. State uncertainty when source, freshness, or degradation fields leave a point unresolved.

These skills support research, not investment advice. A 13F is a historical filing, a factor model does not establish causality, and intraday observations are not a closing-price record or execution signal.

## Reference

- [SEC API reference](https://docs.secapi.ai/api-reference)
- [Getting started](https://docs.secapi.ai/getting-started)
- [Pricing](https://secapi.ai/pricing)
- [SEC API status and request diagnosis](https://docs.secapi.ai/status)
- [Support](https://secapi.ai/support)
- [Skills CLI reference](https://www.skills.sh/docs/cli)
