# Install: Write Country Regime Report

## One-Command Install

```bash
# Claude Code
claude skill install ./skills/write-country-regime-report

# Codex
codex skill add ./skills/write-country-regime-report

# Cowork
cowork skill install ./skills/write-country-regime-report
```

## Required Environment Variables

```bash
export SECAPI_API_KEY="your-api-key"
export SECAPI_BASE_URL="https://api.secapi.ai"
```

## Quick Start

```bash
# Fetch the Japan high-signal macro pack
curl -s "https://api.secapi.ai/v1/macro/high-signal-pack?country=JP" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## What This Skill Does

Builds allocator-style country reports from the high-signal pack, macro regime state, and country-report endpoint. Supports:

- Country macro regime identification
- Growth, inflation, labor, policy, and trade driver analysis
- Official-source high-signal data packs
- Release calendar and forecast context
- Narrative allocator memos via intelligence query

## Triggers

This skill activates when you ask about:
- Country report
- Macro report
- Japan economy
- China outlook
- Macro regime report

## Documentation

- [SKILL.md](./SKILL.md) — Full workflow guidance and endpoint reference
- [metadata.json](./metadata.json) — Triggers, tags, and required endpoints
