---
name: discover-special-situations
description: Finds SEC-derived special situations by type, status, ticker, form trigger, sector, market cap, geography, and recent event flow. Use when the user asks for live deal discovery, merger-arb candidates, activist campaigns, tender offers, spin-offs, restructurings, or situations opened by a specific EDGAR form.
---

# Discover Special Situations

## Setup

Use the public REST API for now. The published `@secapi/cli` release does not yet include the `situations` command group; only use those CLI commands after `secapi situations --help` lists them in your installed version.

```bash
export SECAPI_API_KEY="your-api-key"
```

Use `x-api-key: $SECAPI_API_KEY` for raw HTTP calls. Never pass API keys as command-line arguments.

## Quick Start

```bash
curl -s "https://api.secapi.ai/v1/situations?types=merger,tender_offer&statuses=announced,pending&limit=25" \
  -H "x-api-key: $SECAPI_API_KEY"
```

Raw API equivalent:

```bash
curl -s "https://api.secapi.ai/v1/situations?types=merger,tender_offer&statuses=announced,pending&limit=25" \
  -H "x-api-key: $SECAPI_API_KEY"
```

## Supported Public Surfaces

- API: `GET /v1/situations`, `/by-form/{form}`, `/feed`, `/stats`, and `/performance`
- API: `GET /v1/situations`, `GET /v1/situations/by-form/{form}`, `GET /v1/situations/feed`, `GET /v1/situations/stats`, `GET /v1/situations/performance`
- MCP: `situations.list`, `situations.feed`, `situations.stats`, `situations.performance`

MCP currently does not expose `situations.by-form`; use the raw API for form-triggered discovery.

## Endpoints

- `GET /v1/situations` - durable special-situation roster. Filters: `types`, `subtypes`, `statuses`, `tickers`, `sectors`, `market_cap`, `country`, `announced_from`, `announced_to`, `updated_from`, `forms`, `cursor`, `limit`, `response_mode`, `enrich`.
- `GET /v1/situations/by-form/{form}` - situations opened or advanced by a given EDGAR form such as `SC 13D`, `SC TO-T`, `425`, or `DEFM14A`.
- `GET /v1/situations/feed` - reverse-chronological situation-event feed. Filters: `types`, `categories`, `tickers`, `since`, `cursor`, `limit`.
- `GET /v1/situations/stats` - counts by type, status, sector, and market-cap bucket.
- `GET /v1/situations/performance` - closed-situation cohorts with completion rate, median days to close, premium, and terminated or expired counts.

## Process

1. **Clarify the discovery frame.** If the user names a deal type, use `types`; if they name a form, use `by-form`; if they want "what changed today", use `feed`; if they want a broad market map, start with `stats`.
2. **Start wide and cheap.** Use `enrich=false` for broad rosters. It returns the stripped payload but does not change billing.
3. **Filter deliberately.** Combine `types`, `statuses`, `market_cap`, `country`, and `updated_from` rather than doing multiple unbounded scans.
4. **Use form-triggered discovery when appropriate.** For `SC 13D`, `SC TO-T`, `425`, `DEFM14A`, or similar prompts, call `/v1/situations/by-form/{form}` with a URL-encoded form.
5. **Ground the opportunity set.** Pair the roster with `stats` and, for completed cohorts, `performance` so the user sees both candidates and base rates.
6. **Hand off candidate IDs.** Return `situation_id`, ticker, type, status, latest event time, key dates, and the accession number behind the opening or latest event.

## Output Format

1. **Discovery Frame** - filters used, date window, and whether the result is roster-based, form-triggered, or event-feed-based.
2. **Candidate Table** - situation ID, ticker, issuer, type/subtype, status, headline terms, latest event, key next date, and accession.
3. **Market Map** - distribution from `stats` or `performance` when requested or useful.
4. **Shortlist Rationale** - why each selected situation deserves follow-up.
5. **Next Calls** - exact `summary`, `get`, or `filings` calls to underwrite the top candidates.
6. **Limitations** - missing fields, sparse terms, stale updates, or endpoint gaps.

## Examples

```bash
# Pending merger and tender-offer candidates
curl -s "https://api.secapi.ai/v1/situations?types=merger,tender_offer&statuses=announced,pending&enrich=false&limit=50" -H "x-api-key: $SECAPI_API_KEY"

# Activist situations opened or advanced by Schedule 13D filings
curl -s "https://api.secapi.ai/v1/situations/by-form/SC%2013D?statuses=announced,pending&limit=25" -H "x-api-key: $SECAPI_API_KEY"

# Recent spin-off and restructuring event flow
curl -s "https://api.secapi.ai/v1/situations/feed?types=spin_off,restructuring&since=2026-07-01T00:00:00Z&limit=25" -H "x-api-key: $SECAPI_API_KEY"

# Base-rate context for completed merger cohorts
curl -s "https://api.secapi.ai/v1/situations/performance?types=merger&window=365d&group_by=subtype" -H "x-api-key: $SECAPI_API_KEY"
```

## Pending Surface: Weekly Issues

Weekly issue/archive reads are part of pending datastream PR #1363. Do not call or promise `/v1/situations/issues`, public issue archive reads, CLI issue commands, or MCP issue tools until that PR is merged, deployed, and reflected in the public docs for the environment you are using. Until then, build discovery from `list`, `feed`, `stats`, `performance`, and `by-form`.

## Guidelines

- Use only SEC API public situations data and SEC filing provenance returned by the API.
- Do not infer a deal type from a headline when the API returns a different `type` or `subtype`; report the API taxonomy.
- Never fabricate deal terms, premiums, market data, dates, or probabilities.
- Treat lifecycle status as data, not a verdict. "Pending" does not mean "likely to close."
- Cite `situation_id` and accession number for every candidate that advances to analysis.
