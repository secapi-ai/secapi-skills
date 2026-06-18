# Install: Run Regime Aware Screen

## One-Command Install

```bash
# Claude Code
claude skill install ./skills/run-regime-aware-screen

# Codex
codex skill add ./skills/run-regime-aware-screen

# Cowork
cowork skill install ./skills/run-regime-aware-screen
```

## Required Environment Variables

```bash
export SECAPI_API_KEY="your-api-key"
export SECAPI_BASE_URL="https://api.secapi.ai"
```

## Quick Start

```bash
# Run a regime-aware factor screen
curl -s https://api.secapi.ai/v1/strategies/regime-screen \
  -H "x-api-key: $SECAPI_API_KEY" \
  -H "content-type: application/json" \
  -d '{"country":"US","lookback":"6m","category":"style"}'
```

## What This Skill Does

Screens factors and candidates against the active macro regime and rotation backdrop. Supports:

- Macro regime identification and labeling
- Regime-aware factor screening
- Factor rotation leader/laggard analysis
- Broad factor leaderboard views
- Tightening-cycle and rate-sensitive idea generation

## Triggers

This skill activates when you ask about:
- Regime screen
- Tightening cycle
- Factor rotation
- Macro regime

## Documentation

- [SKILL.md](./SKILL.md) — Full workflow guidance and endpoint reference
- [metadata.json](./metadata.json) — Triggers, tags, and required endpoints
