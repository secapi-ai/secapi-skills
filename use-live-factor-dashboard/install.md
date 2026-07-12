# Install: Use Live Factor Dashboard

## One-Command Install

```bash
# Claude Code
claude skill install ./use-live-factor-dashboard

# Codex
codex skill add ./use-live-factor-dashboard

# Cowork
cowork skill install ./use-live-factor-dashboard
```

## Environment Configuration

```bash
export SECAPI_API_KEY="your-api-key"
# Optional runtime override; examples default to https://api.secapi.ai.
export SECAPI_BASE_URL="https://api.secapi.ai"
```

## Quick Start

```bash
# Get live intraday factor returns
curl -s "${SECAPI_BASE_URL:-https://api.secapi.ai}/v1/factors/returns/intraday" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## What This Skill Does

Powers a live factor dashboard with intraday returns, stock loadings, and model-portfolio drill-down. Supports:

- Intraday factor return monitoring
- Stock-level factor loading diagnostics
- Model portfolio factor views
- Factor correlation and cluster analysis
- Dashboard-style compact numerical output

## Triggers

This skill activates when you ask about:
- Live factor dashboard
- Intraday factor returns
- Factor monitor
- Factor leaderboard live

## Documentation

- [SKILL.md](./SKILL.md) — Full workflow guidance and endpoint reference
- [metadata.json](./metadata.json) — Triggers, tags, and required endpoints
