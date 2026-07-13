# SEC API Skills

Research workflows for agents that can call the SEC API. A skill does not fetch data or make an investment decision on its own. It gives an agent a disciplined sequence of API reads, the questions to settle before it writes, and the evidence it must preserve when the answer rests on a filing.

Start with one workflow, not the whole shelf. Install `company-due-diligence` when you want a cited issuer memo; install `investigate-filing-footnotes` when the question is a disclosure question. The per-skill `install.md` files include a first request and a prompt you can run immediately.

## First Useful Result

Install the company diligence workflow in the current project:

```bash
npx skills add secapi-ai/secapi-skills --skill company-due-diligence
```

Give the agent a key in the runtime where it will make requests:

```bash
export SECAPI_API_KEY="your-api-key"
```

Then ask it for a bounded result:

```text
Prepare a due-diligence memo on NVDA. Separate filing facts from interpretation.
For every filing-derived claim, include the accession number, filing URL, and item or page.
```

The workflow starts with issuer resolution and Company Overview, then adds segments, ownership, factor context, filing sections, and dilution only where they change the memo. It should name its reporting periods and leave unanswered questions unanswered.

## Choose a Workflow

| Skill | Use it when you need | First request to give the agent |
| --- | --- | --- |
| [Analyze Company in Context](./analyze-company-in-context/SKILL.md) | A fast issuer or security brief with business, earnings, factor, and macro context. | `Give me an allocator context pack on NVDA.` |
| [Company Due Diligence](./company-due-diligence/SKILL.md) | A source-backed company memo across business mix, ownership, filings, and dilution. | `Run full due diligence on NVDA.` |
| [Decompose Return and Hedge](./decompose-return-and-hedge/SKILL.md) | A stated-period return explanation and candidate hedges. | `Decompose AAPL's last 6M return and identify hedge candidates.` |
| [Investigate Filing Footnotes](./investigate-filing-footnotes/SKILL.md) | A review of lease, tax, revenue-recognition, debt-covenant, or segment disclosures. | `Investigate CRM's latest lease and revenue-recognition notes.` |
| [Make Portfolio Factor Neutral](./make-portfolio-factor-neutral/SKILL.md) | Factor exposure analysis, a neutralization proposal, and stress testing. | `Analyze and neutralize the factor exposures in my AAPL/MSFT portfolio.` |
| [Run Regime-Aware Screen](./run-regime-aware-screen/SKILL.md) | A tactical factor screen tied to the current macro regime. | `Run a US quality screen for the current regime.` |
| [Track Insiders and 13Fs](./track-insiders-and-13fs/SKILL.md) | Form 3/4/5 activity or a specific manager's 13F changes. | `Compare this manager's last two 13F periods: CIK 0001067983.` |
| [Use Live Factor Dashboard](./use-live-factor-dashboard/SKILL.md) | Intraday factor moves, position loadings, correlations, and model-portfolio context. | `What factors are moving now, and why is NVDA sensitive?` |
| [Write Country Regime Report](./write-country-regime-report/SKILL.md) | A country-level macro and regime brief. | `Write an allocator-style macro report on Japan.` |

## Install Deliberately

The [Skills CLI](https://www.skills.sh/docs/cli) is the supported installation path for this repository. By default it prompts for the installation scope and agent targets. Add `--global` for a user-level install, or install the whole collection only after you know you need it:

```bash
# One workflow for this project
npx skills add secapi-ai/secapi-skills --skill investigate-filing-footnotes

# All skills for your user-level configuration
npx skills add secapi-ai/secapi-skills --global --all

# Inspect supported flags and installed skills
npx skills --help
npx skills list
```

Use the `--agent` option only with an agent name your installed CLI reports as supported. This repository does not maintain or test every agent client's native skill command; the Skills CLI owns that integration step. Update an installed copy when you deliberately want a newer workflow:

```bash
npx skills update
```

## API Access and a Safe Check

The workflows call `https://api.secapi.ai/v1` and authenticate REST requests with `x-api-key`. Create and rotate keys through [SEC API](https://secapi.ai), then put `SECAPI_API_KEY` in the agent runtime's secret store or environment. Do not paste it into a prompt, browser code, checked-in configuration, or a support ticket.

Before using a skill in a production workflow, make one recognizable read with the same runtime and key your agent will use:

```bash
curl --fail --silent --show-error \
  "https://api.secapi.ai/v1/companies/overview?ticker=AAPL" \
  -H "x-api-key: $SECAPI_API_KEY"
```

That verifies credentials, network egress, and a real response. It does not prove that every issuer, derived dataset, market-data entitlement, or live surface is available to your account.

## Treat Evidence as Part of the Output

For filing-derived work, retain the accession number, filing URL, and cited item, section, or page supplied in the response `provenance`. Say what is extracted evidence and what is your interpretation. Retain request IDs, timestamps, freshness, degradation, and rate-limit information when the endpoint returns them. For `429`, respect `Retry-After` and reduce concurrency; do not turn one request into an unbounded retry loop.

The skills are research aids, not investment advice. A factor decomposition is an attribution model, a 13F is a periodic filing rather than a real-time position, and an intraday response can be stale or proxy-based. Read the workflow's lookbacks, required inputs, and caveats before automating an output or using it in a decision.

## Reference

Each skill directory contains its workflow, install notes, and a checked-in metadata record of its triggers and declared endpoint dependencies:

- `SKILL.md` — the agent's process, output format, and workflow-specific evidence rules
- `install.md` — a targeted installation command, first API request, and first prompt
- `metadata.json` — active status, discovery triggers, and required API routes

For precise request and response contracts, use the [API reference](https://docs.secapi.ai/api-reference). For service state and failure evidence, use [status and support signals](https://docs.secapi.ai/status). File workflow issues at [github.com/secapi-ai/secapi-skills/issues](https://github.com/secapi-ai/secapi-skills/issues).
