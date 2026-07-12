# SEC API Skills

SEC API Skills give an AI agent repeatable research workflows for SEC filings, company analysis, ownership, factors, portfolios, and macro research. Install a skill when you want your agent to know which SEC API calls to make, what context to gather, and when filing-derived claims need provenance.

Each skill is a directory containing a `SKILL.md` workflow and `metadata.json` with its triggers and required API routes. The skills guide an agent; they do not replace an SEC API account, API key, or the agent runtime's ability to make API calls.

## Install

This repository is consumable with the [Skills CLI](https://www.skills.sh/docs/cli). The commands below use its documented repository-install flow.

Install all nine skills for your user-level agent configuration:

```bash
npx skills add https://github.com/secapi-ai/secapi-skills --global --all
```

Or install one skill:

```bash
npx skills add https://github.com/secapi-ai/secapi-skills --global --skill company-due-diligence
```

Omit `--global` to install for the current project. To select an integration explicitly, use the agent names accepted by your installed CLI:

```bash
npx skills add https://github.com/secapi-ai/secapi-skills --agent <agent> --skill company-due-diligence
npx skills --help
```

The repository's individual `install.md` files also include client-specific instructions for Claude Code, Codex, and Cowork. Those instructions are supplied with each skill; verify support and configuration in the version of the client you run.

## Configure SEC API Access

Create an API key through [SEC API](https://secapi.ai), then make it available to the agent runtime that will execute the workflow:

```bash
export SECAPI_API_KEY="your-api-key"
export SECAPI_BASE_URL="https://api.secapi.ai"
```

SEC API REST requests authenticate with `x-api-key`. Keep the key in your runtime or secret manager, never in a prompt or committed file. See the [getting-started guide](https://docs.secapi.ai/getting-started), [API conventions](https://docs.secapi.ai/api-conventions), and [API reference](https://docs.secapi.ai/api-reference) for account setup and route contracts.

## Use a Skill

After installing a skill and configuring the agent's SEC API access, ask for the analysis in ordinary language. For example, with `company-due-diligence` installed:

```text
Do full due diligence on NVDA. Cite every filing-derived claim with its accession number, filing URL, and item or page.
```

The workflow directs the agent to resolve the entity, gather company, factor, ownership, and filing context, and separate evidence from interpretation. Review the skill before relying on it for a decision: prompts, required inputs, lookback windows, and response availability vary by workflow.

## Skills

| Skill | Use it for |
| --- | --- |
| [Analyze Company in Context](./analyze-company-in-context/SKILL.md) | A company or security briefing with issuer, factor, macro, and earnings context. |
| [Company Due Diligence](./company-due-diligence/SKILL.md) | A cited company workup covering issuer data, segments, factors, ownership, filings, and dilution. |
| [Decompose Return and Hedge](./decompose-return-and-hedge/SKILL.md) | Security return attribution, factor context, and hedge candidates. |
| [Investigate Filing Footnotes](./investigate-filing-footnotes/SKILL.md) | Lease, tax, revenue-recognition, debt-covenant, and segment-note research. |
| [Make Portfolio Factor-Neutral](./make-portfolio-factor-neutral/SKILL.md) | Portfolio factor exposures, neutralization, optimization, and stress testing. |
| [Run Regime-Aware Screen](./run-regime-aware-screen/SKILL.md) | Factor screens and rotation analysis under a macro regime. |
| [Track Insiders and 13Fs](./track-insiders-and-13fs/SKILL.md) | Form 3, 4, and 5 activity plus 13F holdings and period comparisons. |
| [Use Live Factor Dashboard](./use-live-factor-dashboard/SKILL.md) | Intraday factor monitoring, security loadings, correlations, and model-portfolio views. |
| [Write Country Regime Report](./write-country-regime-report/SKILL.md) | A country macro report using high-signal data and regime context. |

Each directory also has an `install.md` with a short API request example and a `metadata.json` record of its triggers and required endpoints.

## Compatibility and Status

All nine skills are marked `active` in their checked-in metadata. They are discoverable by the Skills CLI as of this repository version. The repository does not include automated compatibility tests for individual agent clients, so confirm skill loading and API authentication in your target runtime.

API route access, market-data coverage, and live or intraday data depend on your SEC API plan, provider entitlements, and current service state. Preserve response provenance, freshness, degraded-state, and rate-limit metadata when using results in user-facing work. See [coverage and depth](https://docs.secapi.ai/coverage-and-depth), [freshness and trust](https://docs.secapi.ai/freshness-and-trust), and [status](https://docs.secapi.ai/status).

## Docs and Support

- [SEC API documentation](https://docs.secapi.ai)
- [MCP workflows](https://docs.secapi.ai/mcp-workflows)
- [Libraries and SDKs](https://docs.secapi.ai/libraries-and-sdks)
- [SEC API changelog](https://docs.secapi.ai/changelog)
- [Repository issues](https://github.com/secapi-ai/secapi-skills/issues) for problems with these skill files

To update installed skills, use the Skills CLI:

```bash
npx skills update
```
