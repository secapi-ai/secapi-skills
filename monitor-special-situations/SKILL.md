---
name: monitor-special-situations
description: Builds repeatable watch workflows for SEC-derived special situations using the situation event feed, calendar, stats, performance, and filtered rosters. Use when the user asks to monitor deal activity, watch a ticker/type/form, track upcoming votes or tender expiries, or create a recurring situation watchlist.
---

# Monitor Special Situations

## Setup

Use the public REST API for now. The published `@secapi/cli` release does not yet include the `situations` command group; only use those CLI commands after `secapi situations --help` lists them in your installed version.

```bash
export SECAPI_API_KEY="your-api-key"
```

Use `x-api-key: $SECAPI_API_KEY` for raw HTTP calls. Never pass API keys as command-line arguments.

## Quick Start

```bash
curl -s "https://api.secapi.ai/v1/situations/feed?types=merger,tender_offer&since=2026-07-01T00:00:00Z&limit=50" -H "x-api-key: $SECAPI_API_KEY"
curl -s "https://api.secapi.ai/v1/situations/calendar?date_types=vote,expiry,expected_close&days=30&limit=50" -H "x-api-key: $SECAPI_API_KEY"
```

## Supported Public Surfaces

- API: `GET /v1/situations/feed`, `GET /v1/situations/calendar`, `GET /v1/situations`, `GET /v1/situations/stats`, `GET /v1/situations/performance`, `GET /v1/situations/{situation_id}`
- MCP: `situations.feed`, `situations.calendar`, `situations.list`, `situations.stats`, `situations.performance`, `situations.get`

There is no public SEC API endpoint in the documented situations surface for creating a server-side alert subscription from this skill. Build local watchlists, recurring agent checks, or downstream jobs from the feed and calendar responses unless the user separately has an approved delivery product surface.

## Endpoints

- `GET /v1/situations/feed` - reverse-chronological situation events. Best for "what changed since last check?"
- `GET /v1/situations/calendar` - upcoming `record`, `vote`, `expiry`, and `expected_close` dates, up to 365 days.
- `GET /v1/situations` - current roster for a watch universe.
- `GET /v1/situations/stats` - aggregate counts over an optional window.
- `GET /v1/situations/performance` - closed-cohort base-rate context.
- `GET /v1/situations/{situation_id}` - hydrate a watched item when the feed reports a material update.

## Process

1. **Define the watch universe.** Capture types, statuses, tickers, forms, sectors, market-cap buckets, country, and the monitoring window.
2. **Create the baseline roster.** Call `GET /v1/situations` with stable filters. Store `situation_id`, status, latest event time, key dates, and latest accession.
3. **Track event flow.** On each run, call `GET /v1/situations/feed?since=<last_checked_at>` with the same type/ticker/category filters. Advance the cursor or timestamp only after recording the results.
4. **Track date risk.** Call `GET /v1/situations/calendar` for the next 30, 60, or 90 days and flag votes, expiries, record dates, and expected closes.
5. **Hydrate only changed items.** For each new feed item or key-date change, call `GET /v1/situations/{situation_id}`.
6. **Maintain a watch ledger.** Keep prior status, current status, latest event, key dates, accession, and action needed.
7. **Report drift.** Use `stats` for population changes and `performance` when a watch workflow needs historical closure context.

## Output Format

1. **Watch Definition** - filters, schedule, and last checked timestamp.
2. **New or Changed Situations** - situation ID, ticker, type, old status, new status, latest event, accession, and why it matters.
3. **Upcoming Calendar** - date, date type, situation ID, issuer, and action.
4. **Watchlist Ledger** - active situations with status, key dates, and next check.
5. **Escalations** - items needing a full underwriting update.
6. **Gaps** - API limitations, missing key dates, or non-public alerting surfaces.

## Examples

```bash
# Daily deal-flow watch
curl -s "https://api.secapi.ai/v1/situations/feed?types=merger,tender_offer&since=2026-07-10T14:00:00Z&limit=100" -H "x-api-key: $SECAPI_API_KEY"

# Forward catalyst calendar
curl -s "https://api.secapi.ai/v1/situations/calendar?date_types=vote,expiry,expected_close&days=45&limit=100" -H "x-api-key: $SECAPI_API_KEY"

# Watch a specific issuer universe
curl -s "https://api.secapi.ai/v1/situations?tickers=AAPL,MSFT,NVDA&statuses=announced,pending&limit=100" -H "x-api-key: $SECAPI_API_KEY"

# Population drift
curl -s "https://api.secapi.ai/v1/situations/stats?window=30d" -H "x-api-key: $SECAPI_API_KEY"
```

## Pending Surface: Weekly Issues

Datastream PR #1363 is still pending for weekly issue/archive reads. Do not build monitoring workflows around weekly issue endpoints or numbered archive pages until the PR has merged, deployed, and public docs show those endpoints. Use `feed` and `calendar` as the supported watch backbone.

## Guidelines

- Do not claim server-side alerts, webhooks, email alerts, or durable subscriptions unless the user has a documented delivery endpoint or product integration available.
- Always preserve the last checked timestamp and feed cursor discipline in recurring workflows.
- Treat `calendar` as a forward-looking catalyst surface, not a status-change log.
- Cite `situation_id` and accession number for every update.
- Use `get` before making a material assertion from a feed item alone.
