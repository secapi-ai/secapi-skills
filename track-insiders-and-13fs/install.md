# Install: Track Insiders And 13Fs

## One-Command Install

```bash
# Claude Code
claude skill install ./skills/track-insiders-and-13fs

# Codex
codex skill add ./skills/track-insiders-and-13fs

# Cowork
cowork skill install ./skills/track-insiders-and-13fs
```

## Required Environment Variables

```bash
export SECAPI_API_KEY="your-api-key"
export SECAPI_BASE_URL="https://api.secapi.ai"
```

## Quick Start

```bash
# Get insider activity for a ticker
curl -s "https://api.secapi.ai/v1/insiders?ticker=NVDA" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## What This Skill Does

Tracks insider activity and institutional (13F) ownership changes. Supports:

- Insider buying/selling activity by company
- 13F institutional holder lookups by manager CIK
- Quarter-over-quarter ownership comparison (style drift detection)
- Narrative explanations via the intelligence query planner

## Triggers

This skill activates when you ask about:
- Insider buying or selling
- 13F changes
- Style drift
- Institutional holders

## Documentation

- [SKILL.md](./SKILL.md) — Full workflow guidance and endpoint reference
- [metadata.json](./metadata.json) — Triggers, tags, and required endpoints
