# Install: Underwrite Special Situation

## One-Command Install

```bash
# Claude Code
claude skill install ./underwrite-special-situation

# Codex
codex skill add ./underwrite-special-situation

# Cowork
cowork skill install ./underwrite-special-situation
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
# Hydrate one situation and its source timeline
curl -s "https://api.secapi.ai/v1/situations/sit_abc123/summary" -H "x-api-key: $SECAPI_API_KEY"
curl -s "https://api.secapi.ai/v1/situations/sit_abc123" -H "x-api-key: $SECAPI_API_KEY"
curl -s "https://api.secapi.ai/v1/situations/sit_abc123/filings?limit=100" -H "x-api-key: $SECAPI_API_KEY"
```

## What This Skill Does

Builds a cited workup for one situation:

- Compact summary and latest event
- Full structured situation detail
- Per-filing timeline with accession-level provenance
- Catalyst map for votes, expiries, expected close, and other key dates
- Underwriting tree with clear separation between API facts and analyst estimates
- Optional closed-cohort performance context

## Triggers

This skill activates when you ask about:

- A single situation ID
- A deal memo or event-driven underwriting memo
- Probability tree, break price, spread compensation, or catalyst map
- A per-situation filing timeline
- What changed in a specific deal

## Documentation

- [SKILL.md](./SKILL.md) - Full workflow guidance and endpoint reference
- [metadata.json](./metadata.json) - Triggers, tags, and required endpoints
