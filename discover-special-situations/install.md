# Install: Discover Special Situations

## One-Command Install

```bash
# Claude Code
claude skill install ./discover-special-situations

# Codex
codex skill add ./discover-special-situations

# Cowork
cowork skill install ./discover-special-situations
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
# List pending merger and tender-offer candidates
curl -s "https://api.secapi.ai/v1/situations?types=merger,tender_offer&statuses=announced,pending&limit=25" -H "x-api-key: $SECAPI_API_KEY"
```

## What This Skill Does

Finds SEC-derived special situations using the documented public situations API:

- Live rosters filtered by type, status, ticker, sector, market-cap bucket, country, and announcement/update date
- Form-triggered discovery for filings such as `SC 13D`, `SC TO-T`, `425`, and `DEFM14A`
- Recent situation-event flow
- Aggregate stats and closed-cohort performance for context
- Candidate shortlists with situation IDs and accession-level provenance

## Triggers

This skill activates when you ask about:

- Special situations or deal discovery
- Merger-arb candidates
- Tender offers, spin-offs, activist campaigns, restructurings, or bankruptcies
- Situations opened by a specific EDGAR form
- Current situation counts or completed-cohort base rates

## Documentation

- [SKILL.md](./SKILL.md) - Full workflow guidance and endpoint reference
- [metadata.json](./metadata.json) - Triggers, tags, and required endpoints
