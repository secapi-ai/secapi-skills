# Install: Analyze Company in Context

## One-Command Install

```bash
# Claude Code
claude skill install ./analyze-company-in-context

# Codex
codex skill add ./analyze-company-in-context

# Cowork
cowork skill install ./analyze-company-in-context
```

## Environment Configuration

```bash
export SECAPI_API_KEY="your-api-key"
# Optional runtime override; examples default to https://api.secapi.ai.
export SECAPI_BASE_URL="https://api.secapi.ai"
```

## Quick Start

```bash
# Get a company overview by ticker
curl -s "${SECAPI_BASE_URL:-https://api.secapi.ai}/v1/companies/overview?ticker=MSFT" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## What This Skill Does

Builds company and security context packs using SEC API intelligence bundles, macro overlays, factor exposures, and earnings context. Supports:

- Issuer-level company briefings
- Security-level trading and return driver analysis
- Earnings preview context near reporting windows
- Factor exposure and macro regime overlays
- Allocator-style summary output

## Triggers

This skill activates when you ask about:
- Company analysis
- Security overview
- Allocator brief
- Issuer context
- Company bundle

## Documentation

- [SKILL.md](./SKILL.md) — Full workflow guidance and endpoint reference
- [metadata.json](./metadata.json) — Triggers, tags, and required endpoints
