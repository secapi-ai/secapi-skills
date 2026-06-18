# Install: Investigate Filing Footnotes

## One-Command Install

```bash
# Claude Code
claude skill install ./skills/investigate-filing-footnotes

# Codex
codex skill add ./skills/investigate-filing-footnotes

# Cowork
cowork skill install ./skills/investigate-filing-footnotes
```

## Required Environment Variables

```bash
export SECAPI_API_KEY="your-api-key"
export SECAPI_BASE_URL="https://api.secapi.ai"
```

## Quick Start

```bash
# Investigate footnotes for a company
curl -s https://api.secapi.ai/v1/intelligence/query \
  -H "x-api-key: $SECAPI_API_KEY" \
  -H "content-type: application/json" \
  -d '{"query":"Investigate the lease, tax, and revenue-recognition footnotes for CRM."}'
```

## What This Skill Does

Investigates filing footnotes and structured filing risk context using semantic query planning. Supports:

- Lease, tax, revenue-recognition, debt covenant, and segment-note analysis
- Semantic query planning for intelligent footnote classification
- Company and security intelligence bundles for supporting context

## Triggers

This skill activates when you ask about:
- Footnotes
- Lease notes
- Tax footnotes
- Revenue recognition
- Segment notes
- Debt covenants

## Documentation

- [SKILL.md](./SKILL.md) — Full workflow guidance and endpoint reference
- [metadata.json](./metadata.json) — Triggers, tags, and required endpoints
