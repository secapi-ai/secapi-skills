# SEC API Skills

Install focused research workflows for an agent that can call [SEC API](https://secapi.ai). Choose one when you need a cited company memo, a filing-footnote investigation, an insider or 13F review, factor research, or a country macro brief.

Each skill tells the agent which SEC API reads to make, what to verify before writing, and what evidence to retain. It does not fetch data by itself or make an investment decision.

## Start With One Question

Install a single workflow in the project where your agent runs:

```bash
npx skills add secapi-ai/secapi-skills --skill company-due-diligence
```

Give the agent access to an SEC API key through its runtime environment or secret store:

```bash
export SECAPI_API_KEY="your-api-key"
```

Then give it a bounded assignment:

```text
Prepare a due-diligence memo on NVDA. Separate filing facts from interpretation.
For every filing-derived claim, include the accession number, filing URL, and item or page.
```

The workflow resolves the issuer, gathers the relevant company, ownership, factor, and filing context, and records the reporting periods it uses. It should surface open questions when the evidence does not settle them.

## Find the Right Skill

| Skill | Ask your agent to | Example first request |
| --- | --- | --- |
| [Analyze Company in Context](./analyze-company-in-context/SKILL.md) | Build a compact issuer or security brief with only the relevant earnings, factor, and macro context. | `Give me an allocator context pack on NVDA.` |
| [Company Due Diligence](./company-due-diligence/SKILL.md) | Produce a source-backed company memo across business mix, ownership, filings, and dilution. | `Run full due diligence on NVDA.` |
| [Decompose Return and Hedge](./decompose-return-and-hedge/SKILL.md) | Explain a security return over a stated period and evaluate exposure-based hedge candidates. | `Decompose AAPL's last 6M return and identify hedge candidates.` |
| [Investigate Filing Footnotes](./investigate-filing-footnotes/SKILL.md) | Review lease, tax, revenue-recognition, debt-covenant, or segment disclosures. | `Investigate CRM's latest lease and revenue-recognition notes.` |
| [Make Portfolio Factor Neutral](./make-portfolio-factor-neutral/SKILL.md) | Analyze portfolio factor exposure, propose a neutralization, and stress-test it. | `Analyze and neutralize the factor exposures in my AAPL/MSFT portfolio.` |
| [Run Regime-Aware Screen](./run-regime-aware-screen/SKILL.md) | Compare factor-rotation leaders and laggards in a country's current macro context. | `For US style factors, return factor-rotation research with current macro-regime context.` |
| [Track Insiders and 13Fs](./track-insiders-and-13fs/SKILL.md) | Review Form 3/4/5 activity or compare a manager's reported 13F periods. | `Compare this manager's last two 13F periods: CIK 0001067983.` |
| [Use Live Factor Dashboard](./use-live-factor-dashboard/SKILL.md) | Monitor intraday factor moves, position loadings, correlations, and model-portfolio context. | `What factors are moving now, and why is NVDA sensitive?` |
| [Write Country Regime Report](./write-country-regime-report/SKILL.md) | Write a dated country-level macro and regime brief. | `Write an allocator-style macro report on Japan.` |

Every skill directory includes an `install.md` with its installation command, first API request, and example prompt.

## Install and Check Access

The [Skills CLI](https://www.skills.sh/docs/cli) installs and manages skills for AI agents. It prompts for installation scope and agent targets. Use `--global` for a user-level installation, and use `--all` only when you want the entire collection:

```bash
# One workflow for this project
npx skills add secapi-ai/secapi-skills --skill investigate-filing-footnotes

# All skills for your user-level configuration
npx skills add secapi-ai/secapi-skills --global --all

# Check CLI options and installed skills
npx skills --help
npx skills list
```

Confirm that the agent runtime can make an authenticated API request before relying on a workflow:

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/companies/overview?ticker=AAPL" \
  -H "x-api-key: $SECAPI_API_KEY"
```

That confirms the key, network egress, and one API response. Availability for a particular issuer, filing, derived dataset, market-data entitlement, or live surface depends on the route and account. Keep the key out of prompts, browser code, checked-in configuration, and support requests.

## Keep the Evidence With the Answer

For filing-backed claims, retain the response `provenance`: the accession number, filing URL, and relevant item, section, or page. State which observations are extracted from the filing and which are your interpretation. When returned, retain timestamps, freshness, degradation, rate-limit, and request-identification fields with the result.

These are research workflows, not investment advice. A factor decomposition is an attribution model, a 13F reports a past filing period rather than a live position, and an intraday response can be stale or proxy-based. Read each workflow's required inputs, lookbacks, and caveats before automating an output or using it in a decision.

## Reference

- [SEC API documentation](https://docs.secapi.ai/api-reference) for API contracts and examples
- [SEC API status](https://docs.secapi.ai/status) for public service checks and request diagnosis
- [SEC API Skills issues](https://github.com/secapi-ai/secapi-skills/issues) for workflow feedback

Each skill's `metadata.json` lists its active status, discovery triggers, and declared API dependencies.
