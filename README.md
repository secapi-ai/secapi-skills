# SEC API Skills

Focused research workflows for agents using [SEC API](https://secapi.ai). Choose the job you need, install that skill, and give the agent a bounded question with an evidence standard. These skills organize research; they do not make an investment decision or replace review of the underlying filing.

## Start Here

Install one skill in the project where your agent runs:

```bash
npx skills add secapi-ai/secapi-skills --skill company-due-diligence
export SECAPI_API_KEY="your-api-key"
```

Then give the agent a concrete assignment:

```text
Prepare a due-diligence memo on NVDA. State the reporting periods used.
Separate disclosed facts from interpretation, and cite each filing claim with
the accession number, filing URL, and relevant item, note, or page.
```

SEC API accepts the key in the `x-api-key` header. Keep it in your runtime environment or secret manager, never in a prompt, browser client, or checked-in file.

## Choose A Workflow

| Skill                                                                     | Job                                                                            | First prompt                                                           |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------- |
| [Analyze Company in Context](./analyze-company-in-context/SKILL.md)       | Build a concise issuer brief before committing to deeper work.                 | `Give me an allocator context pack on NVDA.`                           |
| [Company Due Diligence](./company-due-diligence/SKILL.md)                 | Produce a filing-led company memo with business, ownership, and risk context.  | `Run due diligence on NVDA and show the evidence trail.`               |
| [Decompose Return and Hedge](./decompose-return-and-hedge/SKILL.md)       | Attribute a security return and frame hedge candidates as exposure trade-offs. | `Decompose AAPL's last 6M return and assess hedge candidates.`         |
| [Investigate Filing Footnotes](./investigate-filing-footnotes/SKILL.md)   | Investigate a precise accounting disclosure in the filing record.              | `Review CRM's latest lease and revenue-recognition notes.`             |
| [Make Portfolio Factor Neutral](./make-portfolio-factor-neutral/SKILL.md) | Measure a weighted portfolio's factor exposure and test a neutralization.      | `Analyze this portfolio's factor exposures and test a neutralization.` |
| [Run Regime-Aware Screen](./run-regime-aware-screen/SKILL.md)             | Research factor rotation against a dated country regime.                       | `Show US style-factor rotation in its current macro context.`          |
| [Track Insiders and 13Fs](./track-insiders-and-13fs/SKILL.md)             | Review issuer insider filings or a manager's reported 13F history.             | `Compare the latest two reported 13Fs for CIK 0001067983.`             |
| [Use Live Factor Dashboard](./use-live-factor-dashboard/SKILL.md)         | Monitor intraday factor moves and a position's reported loadings.              | `What factors are moving now, and why is NVDA sensitive?`              |
| [Write Country Regime Report](./write-country-regime-report/SKILL.md)     | Write a dated country macro brief with observed data and release context.      | `Write an allocator-style macro brief on Japan.`                       |

Each directory has an `install.md` with the command and first prompt.

## Check Access

Use the Skills CLI to inspect supported agents or install the whole collection:

```bash
npx skills --help
npx skills add secapi-ai/secapi-skills --all
```

Check that your environment can authenticate before relying on a workflow:

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/companies/overview?ticker=AAPL" \
  -H "x-api-key: $SECAPI_API_KEY"
```

A successful request establishes access to that route, not coverage for every issuer, filing, derived dataset, or market-data surface. For a failed request, retain the route, timestamp, HTTP status, error code, `Request-Id`, and `traceparent` when present; never include the key or private payload in a support report.

## Evidence Standard

Treat filings, derived models, and live market observations as different kinds of evidence. For filing-backed claims, retain the accession number, filing URL, and exact item, note, section, or page. Name report dates, lookbacks, and response timestamps. Label interpretation, forecast, and model output as such, and state uncertainty where the returned source, freshness, or degradation fields do not settle a point.

These workflows support research, not investment advice. A 13F is a historical filing, a factor model is not causality, and intraday observations are not a closing-price record or execution signal.

## Reference

- [SEC API reference](https://docs.secapi.ai/api-reference)
- [SEC API status and request diagnosis](https://docs.secapi.ai/status)
- [Skills CLI reference](https://www.skills.sh/docs/cli)
