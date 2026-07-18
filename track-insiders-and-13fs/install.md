# Track Insiders and 13Fs

Use this skill to investigate issuer insider filings or a manager's historical 13F disclosures without confusing the two.

```bash
npx skills add secapi-ai/secapi-skills --skill track-insiders-and-13fs
export SECAPI_API_KEY="your-api-key"
```

First prompt:

```text
Summarize recent NVDA Forms 3, 4, and 5. State the filing-date window, flag only
filing-supported clusters or repeat activity, and cite the accession number and
filing URL for every material transaction.
```

For a manager, supply its CIK and ask to compare the latest two parsable 13F reports. The [full instructions](./SKILL.md) explain the reporting boundary.
