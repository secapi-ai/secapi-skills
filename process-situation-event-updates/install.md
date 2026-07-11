# Install: Process Situation Event Updates

## One-Command Install

```bash
# Claude Code
claude skill install ./process-situation-event-updates

# Codex
codex skill add ./process-situation-event-updates

# Cowork
cowork skill install ./process-situation-event-updates
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
# Process updates since a prior checkpoint
curl -s "https://api.secapi.ai/v1/situations/feed?since=2026-07-10T14:00:00Z&limit=100" -H "x-api-key: $SECAPI_API_KEY"
curl -s "https://api.secapi.ai/v1/situations/sit_abc123" -H "x-api-key: $SECAPI_API_KEY"
```

## What This Skill Does

Turns new situation feed items into cited update briefs:

- Incremental feed reads since a checkpoint
- Grouping multiple events by situation ID
- Hydration of changed situations
- Timeline delta review when the latest event needs context
- Classification of status, terms, date, and filing-context changes
- Action queues for underwriting, monitoring, ignoring, or manual review

## Triggers

This skill activates when you ask about:

- What changed in a situation or deal
- Updating a watchlist after new filings
- Summarizing new situation events
- Status changes, key-date changes, or timeline deltas
- Event-update workflows for recurring monitors

## Documentation

- [SKILL.md](./SKILL.md) - Full workflow guidance and endpoint reference
- [metadata.json](./metadata.json) - Triggers, tags, and required endpoints
