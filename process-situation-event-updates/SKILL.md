---
name: process-situation-event-updates
description: Processes updates to existing special situations by reading the reverse-chronological event feed, hydrating changed situations, comparing lifecycle status and key-date changes, and producing cited update briefs. Use when the user asks what changed in a deal, how to update a watchlist, or how to summarize new filings against existing situation state.
---

# Process Situation Event Updates

## Setup

Use the public REST API for now. The published `@secapi/cli` release does not yet include the `situations` command group; only use those CLI commands after `secapi situations --help` lists them in your installed version.

```bash
export SECAPI_API_KEY="your-api-key"
```

Use `x-api-key: $SECAPI_API_KEY` for raw HTTP calls. Never pass API keys as command-line arguments.

## Quick Start

```bash
curl -s "https://api.secapi.ai/v1/situations/feed?since=2026-07-10T14:00:00Z&limit=100" -H "x-api-key: $SECAPI_API_KEY"
curl -s "https://api.secapi.ai/v1/situations/sit_abc123" -H "x-api-key: $SECAPI_API_KEY"
curl -s "https://api.secapi.ai/v1/situations/sit_abc123/filings?limit=100" -H "x-api-key: $SECAPI_API_KEY"
```

## Supported Public Surfaces

- API: `GET /v1/situations/feed`, `GET /v1/situations/{situation_id}`, `GET /v1/situations/{situation_id}/filings`, `GET /v1/situations/{situation_id}/summary`, `GET /v1/situations/calendar`
- MCP: `situations.feed`, `situations.get`, `situations.calendar`

MCP currently does not expose `situations.filings` or `situations.summary`; use the raw API when you need those exact sub-resources.

## Endpoints

- `GET /v1/situations/feed` - reverse-chronological situation events, filterable by type, filing-event category, ticker, and `since`.
- `GET /v1/situations/{situation_id}` - current full state and full timeline for one situation.
- `GET /v1/situations/{situation_id}/filings` - paginated source timeline, oldest first.
- `GET /v1/situations/{situation_id}/summary` - compact rendered markdown, deal terms, and latest event.
- `GET /v1/situations/calendar` - upcoming key dates for follow-up after an update.

## Process

1. **Load prior state.** Use the user's watch ledger or last known situation snapshot. If none exists, call `GET /v1/situations/{situation_id}` and treat that as the baseline.
2. **Fetch new feed items.** Call `GET /v1/situations/feed?since=<last_checked_at>` with the relevant filters. Keep the returned event order and timestamps.
3. **Group by situation.** Multiple filings can update the same situation. Process all events for one `situation_id` together.
4. **Hydrate changed situations.** Call `GET /v1/situations/{situation_id}` for each changed item; call `GET /v1/situations/{situation_id}/filings` if the update depends on earlier timeline context or if the full event sequence is paginated.
5. **Compare facts.** Check lifecycle status, subtype, deal terms, key dates, latest event time, source accessions, and event count. Do not infer missing fields.
6. **Classify the update.** Use simple labels: `new_situation`, `status_change`, `terms_change`, `key_date_change`, `new_filing_context`, `no_material_change`, or `needs_manual_review`.
7. **Produce the update brief.** Cite the event accession and link, explain what changed, and name the next action.
8. **Advance the checkpoint.** Record the max event timestamp or cursor only after the update brief is complete.

## Output Format

1. **Checkpoint** - prior `last_checked_at`, new checkpoint, filters used.
2. **Update Summary** - count of feed items, affected situations, and material updates.
3. **Per-Situation Briefs** - situation ID, ticker, old state, new state, update label, accession, filing URL, and analyst note.
4. **Timeline Delta** - new filings or changed key events in chronological order.
5. **Action Queue** - underwrite, monitor, ignore, or manual review.
6. **Open Questions** - missing terms, absent dates, unclear status change, or API limitations.

## Examples

```bash
# Process all updates since the last run
curl -s "https://api.secapi.ai/v1/situations/feed?since=2026-07-10T14:00:00Z&limit=100" -H "x-api-key: $SECAPI_API_KEY"

# Hydrate each affected situation
curl -s "https://api.secapi.ai/v1/situations/sit_abc123" -H "x-api-key: $SECAPI_API_KEY"

# Inspect timeline if the delta is ambiguous
curl -s "https://api.secapi.ai/v1/situations/sit_abc123/filings?limit=100" -H "x-api-key: $SECAPI_API_KEY"

# Re-check calendar after a date update
curl -s "https://api.secapi.ai/v1/situations/calendar?tickers=ABC&date_types=vote,expiry,expected_close&days=90" -H "x-api-key: $SECAPI_API_KEY"
```

## Pending Surface: Weekly Issues

PR #1363 is pending for durable weekly issue/archive reads. Do not treat issue publication as the event-update source of truth until those endpoints are merged, deployed, and documented. Use `GET /v1/situations/feed` plus per-situation hydration for update workflows.

## Guidelines

- Do not collapse multiple feed events into one conclusion without checking the hydrated detail.
- Preserve prior and current status side by side when reporting changes.
- Cite the accession number and filing URL for each update.
- Do not invent lifecycle events, webhook deliveries, or server-side notification state.
- Use only public SEC API surfaces and the data returned by those surfaces.
