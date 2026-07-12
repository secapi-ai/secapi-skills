# Install: Decompose Return and Hedge

## One-Command Install

```bash
# Claude Code
claude skill install ./decompose-return-and-hedge

# Codex
codex skill add ./decompose-return-and-hedge

# Cowork
cowork skill install ./decompose-return-and-hedge
```

## Environment Configuration

```bash
export SECAPI_API_KEY="your-api-key"
# Optional runtime override; examples default to https://api.secapi.ai.
export SECAPI_BASE_URL="https://api.secapi.ai"
```

## Quick Start

```bash
# Decompose a stock's 6-month return into factors
curl -s "${SECAPI_BASE_URL:-https://api.secapi.ai}/v1/factors/decomposition?symbol=AAPL&lookback=6m" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## What This Skill Does

Breaks down a security return into factor and macro context, then proposes hedge candidates. Supports:

- Factor decomposition over configurable lookback windows
- Stock factor loadings and fit diagnostics
- Security intelligence bundle for filing-specific risks
- Hedge candidate generation with expected exposure delta

## Triggers

This skill activates when you ask about:
- Decompose return
- Why did this stock move
- Hedge this position
- Return drivers

## Documentation

- [SKILL.md](./SKILL.md) — Full workflow guidance and endpoint reference
- [metadata.json](./metadata.json) — Triggers, tags, and required endpoints
