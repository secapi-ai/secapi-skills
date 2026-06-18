# Install: Company Due Diligence

## One-Command Install

```bash
# Claude Code
claude skill install ./skills/company-due-diligence

# Codex
codex skill add ./skills/company-due-diligence

# Cowork
cowork skill install ./skills/company-due-diligence
```

## Required Environment Variables

```bash
export SECAPI_API_KEY="your-api-key"
export SECAPI_BASE_URL="https://api.secapi.ai"
```

## Quick Start

```bash
# Resolve the issuer + snapshot in one call
curl -s "https://api.secapi.ai/v1/companies/overview?ticker=NVDA&include=segments,dilution" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## What This Skill Does

Runs a full company due-diligence workflow and outputs a cited DD memo:

- Entity resolution + Company Overview and business Segments
- Financials, ratios, factor exposures, and return decomposition
- Ownership: 13F institutional holders + Form 3/4/5 insider activity
- 10-K Item 1 / 1A / 7 filing-section extraction with citations
- Dilution score with per-factor breakdown
- A cited memo where every filing-sourced claim carries an accession number + filing URL + page

## Triggers

This skill activates when you ask about:
- Due diligence
- Deep dive
- Company workup
- Pre-investment pack
- Full company analysis / DD memo

## Documentation

- [SKILL.md](./SKILL.md) — Full workflow guidance and endpoint reference
- [metadata.json](./metadata.json) — Triggers, tags, and required endpoints
