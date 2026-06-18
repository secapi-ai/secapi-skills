# SEC API Skills

Installable workflow skills for Claude Code, Codex, and Cowork. Each skill teaches your AI agent how to use SEC API endpoints for specific financial analysis workflows.

## Authentication

Use `x-api-key: <key>` on every request.

## Base URL

```text
https://api.secapi.ai/v1
```

## Required Environment Variables

```bash
export SECAPI_API_KEY="your-api-key"
export SECAPI_BASE_URL="https://api.secapi.ai"
```

## Install a Skill

From the published package (recommended):

```bash
# Install all skills across Claude Code, Cursor, Codex, and ~70 other agents
npx skills add secapi-ai/secapi-skills --global

# Or a single skill
npx skills add secapi-ai/secapi-skills --global --skill company-due-diligence

# Or via npm for programmatic access
npm install @secapi/skills
```

From a local checkout of this repo:

```bash
# Claude Code
claude skill install ./skills/<skill-name>

# Codex
codex skill add ./skills/<skill-name>

# Cowork
cowork skill install ./skills/<skill-name>
```

## Available Skills

| Skill | Description | Install |
|-------|-------------|---------|
| [company-due-diligence](./company-due-diligence/) | Run a full DD workup — Overview, Segments, financials, factors, ownership, filing sections, and dilution — as a cited memo with filing provenance | `claude skill install ./skills/company-due-diligence` |
| [analyze-company-in-context](./analyze-company-in-context/) | Build issuer and security context packs with Company Overview, Segments, intelligence bundles, plus factor and macro overlays | `claude skill install ./skills/analyze-company-in-context` |
| [decompose-return-and-hedge](./decompose-return-and-hedge/) | Explain a stock's return with factor decomposition, loadings, and hedge ideas | `claude skill install ./skills/decompose-return-and-hedge` |
| [track-insiders-and-13fs](./track-insiders-and-13fs/) | Analyze insider activity and institutional ownership changes, including manager style drift | `claude skill install ./skills/track-insiders-and-13fs` |
| [investigate-filing-footnotes](./investigate-filing-footnotes/) | Use the semantic planner and intelligence bundles to investigate filing footnotes and accounting-risk areas | `claude skill install ./skills/investigate-filing-footnotes` |
| [make-portfolio-factor-neutral](./make-portfolio-factor-neutral/) | Analyze portfolio exposures, generate neutralization plans, and validate with stress scenarios | `claude skill install ./skills/make-portfolio-factor-neutral` |
| [run-regime-aware-screen](./run-regime-aware-screen/) | Screen factors and candidates against the active macro regime and rotation backdrop | `claude skill install ./skills/run-regime-aware-screen` |
| [write-country-regime-report](./write-country-regime-report/) | Build allocator-style country reports from high-signal packs, macro regime state, and official data | `claude skill install ./skills/write-country-regime-report` |
| [use-live-factor-dashboard](./use-live-factor-dashboard/) | Power a live factor dashboard with intraday returns, stock loadings, and model-portfolio drill-down | `claude skill install ./skills/use-live-factor-dashboard` |

## Skill Structure

Each skill contains:

- `SKILL.md` — Workflow guidance, example requests, and endpoint reference
- `metadata.json` — Triggers, tags, required endpoints, and schema version
- `install.md` — One-command install instructions and quick-start example

## List Skills

```bash
bun run skills:list
```
