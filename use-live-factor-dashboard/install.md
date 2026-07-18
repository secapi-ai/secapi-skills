# Use Live Factor Dashboard

Use this skill for a dated factor-monitoring view with explicit data-quality boundaries.

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

The [full instructions](./SKILL.md) describe monitoring and causality limits.
