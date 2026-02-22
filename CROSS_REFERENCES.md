# Cross-Reference Pattern

This document defines standard patterns for referencing external resources (Google Drive, GitHub repos, issues, etc.) within documentation.

## Google Drive References

Use this pattern when referencing documents stored in Google Drive:

```markdown
## Google Drive Reference

> **Document**: [Document Name]
> **Link**: [Link Text](https://drive.google.com/file/d/XXXXX/view)
> **Location**: `Drive > Campaigns > 2026 > Q1/`
> **Status**: [Status if applicable]
```

### When to Use

Reference Google Drive for:

- Legal documents and contracts
- Presentation decks
- Spreadsheets and financial documents
- Marketing assets (images, videos)
- Any business artifact (PDFs, docs, etc.)

## Other GitHub Repositories

When referencing code in other repositories, use the repo name followed by the path within that repo:

```markdown
## Code Reference

> **Repository**: [repo-name]
> **Component**: [Component name]
> **Docs**: [docs/file.md](repo-name/docs/file.md)
> **Issues**: [#123](repo-name/issues/123), [#124](repo-name/issues/124)
```

For repos in the same GitHub organization:

```markdown
See [docs/file.md](repo-name/docs/file.md) for details.
Related issue: [#42](repo-name/issues/42)
```

### When to Use

- Referencing implementation details
- Linking to related features
- Connecting decisions to code changes
- Tracking related issues or PRs

## Cross-Domain References (Within This Repo)

When referencing decisions or initiatives in other domains within this docs repo:

```markdown
## Related Initiatives

- **Engineering**: [2026-02-10-task-api](/engineering/2026/02-february/2026-02-10-task-api/)
- **Marketing**: [2026-02-12-product-launch-campaign](/marketing/2026/02-february/2026-02-12-product-launch-campaign/)
```

Use absolute paths from the repo root (starting with `/`) for clarity.

## Best Practices

1. **Be Specific** - Include exact file paths when possible
2. **Add Context** - Explain why the reference is relevant
3. **Keep Links Updated** - If a resource moves, update the reference in the current document (this is one of the few cases where updates are acceptable)
4. **Use Descriptive Link Text** - Instead of "click here", use "see the pricing strategy document"

## External System References

For CRM entries, project management tools, etc.:

```markdown
## External References

> **CRM**: [Customer Account](https://crm.example.com/accounts/123)
> **Project Board**: [Task Board](https://board.example.com/project/abc)
> **Analytics**: [Dashboard](https://analytics.example.com/dash/xyz)
```
