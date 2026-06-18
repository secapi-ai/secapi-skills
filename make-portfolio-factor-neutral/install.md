# Install: Make Portfolio Factor Neutral

## One-Command Install

```bash
# Claude Code
claude skill install ./skills/make-portfolio-factor-neutral

# Codex
codex skill add ./skills/make-portfolio-factor-neutral

# Cowork
cowork skill install ./skills/make-portfolio-factor-neutral
```

## Required Environment Variables

```bash
export SECAPI_API_KEY="your-api-key"
export SECAPI_BASE_URL="https://api.secapi.ai"
```

## Quick Start

```bash
# Analyze portfolio factor exposures
curl -s https://api.secapi.ai/v1/portfolio/analyze \
  -H "x-api-key: $SECAPI_API_KEY" \
  -H "content-type: application/json" \
  -d '{"country":"US","lookback":"6m","holdings":[{"symbol":"AAPL","weight":0.5},{"symbol":"MSFT","weight":0.5}]}'
```

## What This Skill Does

Analyzes portfolio factor exposures, generates neutralization plans, and validates them with stress scenarios. Supports:

- Portfolio factor exposure analysis
- Factor-neutral optimization targets
- Hedge basket generation
- Stress-test validation of proposed adjustments
- Model portfolio factor views

## Triggers

This skill activates when you ask about:
- Factor neutral
- Hedge my portfolio
- Portfolio exposures
- Portfolio optimization

## Documentation

- [SKILL.md](./SKILL.md) — Full workflow guidance and endpoint reference
- [metadata.json](./metadata.json) — Triggers, tags, and required endpoints
