# Install: Analyze Company In Context

## One-Command Install

```bash
# Claude Code
claude skill install ./skills/analyze-company-in-context

# Codex
codex skill add ./skills/analyze-company-in-context

# Cowork
cowork skill install ./skills/analyze-company-in-context
```

## Required Environment Variables

```bash
export SECAPI_API_KEY="your-api-key"
export SECAPI_BASE_URL="https://api.secapi.ai"
```

## Quick Start

```bash
# Get a company intelligence bundle
curl -s "https://api.secapi.ai/v1/intelligence/company?ticker=MSFT" \
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
