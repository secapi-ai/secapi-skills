# Use Live Factor Dashboard

Install this for a dated factor-monitoring view with explicit data-quality boundaries.

```bash
npx skills add secapi-ai/secapi-skills --skill use-live-factor-dashboard
export SECAPI_API_KEY="your-api-key"
```

First prompt:

```text
What factors are moving now, which moves are unusual, and why might NVDA be
sensitive? Report the response timestamp and flag any stale, proxy, or degraded
state before interpreting the loadings.
```

The [workflow](./SKILL.md) describes the monitoring and causality boundaries.
