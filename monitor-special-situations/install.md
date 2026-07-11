# Install: Monitor Special Situations

## One-Command Install

```bash
# Claude Code
claude skill install ./monitor-special-situations

# Codex
codex skill add ./monitor-special-situations

# Cowork
cowork skill install ./monitor-special-situations
```

## API access

```bash
export SECAPI_API_KEY="your-api-key"
```

## Required Environment Variables

```bash
export SECAPI_API_KEY="your-api-key"
# Optional: only when pointing at a non-production origin
export SECAPI_BASE_URL="https://api.secapi.ai"
```

## Quick Start

```bash
# Check new events and upcoming catalysts
curl -s "https://api.secapi.ai/v1/situations/feed?types=merger,tender_offer&since=2026-07-01T00:00:00Z&limit=50" -H "x-api-key: $SECAPI_API_KEY"
curl -s "https://api.secapi.ai/v1/situations/calendar?date_types=vote,expiry,expected_close&days=30&limit=50" -H "x-api-key: $SECAPI_API_KEY"
```

## What This Skill Does

Builds watch workflows from public situations surfaces:

- Baseline watch rosters for selected types, tickers, forms, sectors, and statuses
- Incremental feed checks since the last run
- Forward calendar checks for votes, record dates, expiries, and expected closes
- Changed-item hydration through situation detail
- Watch ledgers with next actions and accession-level provenance

## Triggers

This skill activates when you ask about:

- Monitoring special situations
- Deal watchlists or daily deal-flow checks
- Upcoming votes, tender expiries, record dates, or expected closes
- Ticker, form, or category watch workflows
- Recurring situation updates

## Documentation

- [SKILL.md](./SKILL.md) - Full workflow guidance and endpoint reference
- [metadata.json](./metadata.json) - Triggers, tags, and required endpoints
