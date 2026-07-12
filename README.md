# SEC API Skills

Install these skills in an agent that can call the [SEC API](https://docs.secapi.ai). They give the agent named, repeatable workflows for company due diligence, filing-footnote review, ownership analysis, factor work, and macro research. The skills direct the agent to the relevant SEC API routes and require source details when the workflow returns filing-derived claims.

## Install

The [Skills CLI](https://www.skills.sh/docs/cli) installs this public GitHub repository into supported agent environments. It runs through `npx`; there is no package to add to your application.

Install every skill globally for your local agent tools:

```bash
npx skills add https://github.com/secapi-ai/secapi-skills --global --all
```

Install one skill globally:

```bash
npx skills add https://github.com/secapi-ai/secapi-skills --global --skill company-due-diligence
```

Install one skill for the current project instead of your user-level agent configuration:

```bash
npx skills add https://github.com/secapi-ai/secapi-skills --skill company-due-diligence
```

To target particular agent integrations, pass `--agent` with the agent name accepted by your installed Skills CLI. Run `npx skills --help` to see the available options and `npx skills list` to inspect project-installed skills.

## Give The Agent API Access

Create an API key in [SEC API](https://secapi.ai), then provide it to the runtime that executes your agent:

```bash
export SECAPI_API_KEY="your-api-key"
```

The workflows call `https://api.secapi.ai/v1` and send the key as `x-api-key`. Keep the key in the agent runtime or its secret manager; do not put it in a prompt, a repository, or client-side code. See the [API reference](https://docs.secapi.ai) for route contracts and response fields.

## Use A Skill

After installation, ask the agent for the analysis you need. The skill's trigger and workflow guide it toward the applicable SEC API calls. For example:

```text
Run full due diligence on NVDA. Cite every filing-derived claim with its accession number, filing URL, and item or page.
```

Each skill is a directory containing a `SKILL.md` workflow and a `metadata.json` record with its triggers and required endpoints. Review the workflow before production use, especially its required inputs, lookback periods, and provenance requirements.

## Available Skills

| Skill | Use it for | Workflow |
| --- | --- | --- |
| Company Due Diligence | A cited company workup spanning issuer data, segments, factors, ownership, filings, and dilution. | [Read](./company-due-diligence/SKILL.md) |
| Analyze Company In Context | An issuer or security briefing with intelligence, factor, macro, and earnings context. | [Read](./analyze-company-in-context/SKILL.md) |
| Decompose Return And Hedge | Return attribution, factor loadings, and hedge candidates for a security. | [Read](./decompose-return-and-hedge/SKILL.md) |
| Track Insiders And 13Fs | Insider transactions and a manager's 13F holdings or period-over-period changes. | [Read](./track-insiders-and-13fs/SKILL.md) |
| Investigate Filing Footnotes | Filing-note research across leases, tax, revenue recognition, debt covenants, and segments. | [Read](./investigate-filing-footnotes/SKILL.md) |
| Make Portfolio Factor Neutral | Portfolio exposure analysis, factor-neutral optimization, and stress testing. | [Read](./make-portfolio-factor-neutral/SKILL.md) |
| Run Regime Aware Screen | Factor screens and rotation analysis under a stated macro regime. | [Read](./run-regime-aware-screen/SKILL.md) |
| Write Country Regime Report | A country macro report using the high-signal pack, regime state, and country-report routes. | [Read](./write-country-regime-report/SKILL.md) |
| Use Live Factor Dashboard | Intraday factor returns, security loadings, correlations, and model-portfolio views. | [Read](./use-live-factor-dashboard/SKILL.md) |

## Source And Updates

This repository is the source for the skill files: [github.com/secapi-ai/secapi-skills](https://github.com/secapi-ai/secapi-skills). Update installed skills with the Skills CLI when you want the latest repository version:

```bash
npx skills update
```
