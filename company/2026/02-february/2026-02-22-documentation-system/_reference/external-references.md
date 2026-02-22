# External References Pattern

When referencing systems outside this documentation repository, use structured blocks for clarity and searchability.

## Pattern

```markdown
## External Reference

> **System**: [Name of external system]
> **Type**: [Drive / CRM / Analytics / etc.]
> **Location**: [Path or URL]
> **Purpose**: [Why we're referencing this]
> **Last Verified**: YYYY-MM-DD
```

## Examples

### Google Drive

```markdown
## External Reference

> **Document**: Q1 2026 Financial Report
> **Type**: Google Drive
> **Location**: `Drive > Finance > 2026 > Q1/`
> **Link**: [View Document](https://drive.google.com/...)
> **Last Verified**: 2026-02-22
```

### CRM System

```markdown
## External Reference

> **System**: Salesforce
> **Record**: Acme Corp Account
> **Link**: [View in CRM](https://crm.example.com/accounts/12345)
> **Last Verified**: 2026-02-20
```

### Analytics Dashboard

```markdown
## External Reference

> **System**: Analytics Platform
> **Dashboard**: Monthly Active Users
> **Link**: [View Dashboard](https://analytics.example.com/dash/mau)
> **Last Verified**: 2026-02-22
```

## Why This Matters

Structured references make it easy for agents and humans to:

1. Understand what external system holds the source of truth
2. Find the resource even if links break (location path provides context)
3. Know if a reference might be stale (last verified date)
