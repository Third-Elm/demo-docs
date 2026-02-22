# Docs Contribution Checklist

Use this checklist when creating or updating documentation.

## Content Principles

### Self-Contained

- [ ] Context is explained inline - Don't rely on external context, conversations, or tribal knowledge. If it matters, explain it.
- [ ] Links are searchable - References point to stable, discoverable resources. Not "see the discussion from last Tuesday."
- [ ] Acronyms are defined - On first use or in a glossary. Not everyone knows what you know.

### Essential Only

- [ ] Progressive discovery - Top-level files contain only what readers ALWAYS need. Details go in linked files.
- [ ] Clear information hierarchy - Overview first, specifics in sub-documents.
- [ ] No explanation "for later" - If it doesn't serve a clear purpose now, remove it.

### Verifiable

- [ ] Facts are checked - Don't assume. Verify against actual code, configs, or systems before writing.
- [ ] Examples are accurate - Use real tech choices, not illustrative placeholders. Use generic names for entities.
- [ ] Nothing is guessed - If you're unsure, either verify or leave it out.

### Clear and Correctable

- [ ] Correctness is testable - Can someone verify if a requirement is met? Use specific, observable criteria.
- [ ] Definition of done exists - It's clear when the work described is complete.
- [ ] Rationale is provided when needed - Explain "why" only when it's not obvious from context.

## Structure and Location

### Right Place, Right Time

- [ ] Content belongs here - Decisions and "why" go here. Code goes in repos. Business artifacts go in Drive. Operational data stays in specialized platforms.
- [ ] Correct domain - Engineering, company, or marketing.
- [ ] No duplication - If content naturally lives elsewhere (individual repo docs, external system docs), reference it instead of duplicating.

### Dating and Immutability

- [ ] Dated format - Use `YYYY-MM-DD-descriptive-name/` for initiatives.
- [ ] No retroactive updates - Never update old files. Create a new dated entry instead.
- [ ] Clear evolution - New entries reference what they build upon.
- [ ] Copy reference and templates - Copy `_reference/` and `_templates/` from domain to project folder.
- [ ] Add to project-slugs.md - Add project slug to `project-slugs.md` in the month folder.

### Document Types

- [ ] Type matches domain - PRD/ADR/SDP for engineering, campaign briefs for marketing, CDR for company decisions.
- [ ] Appropriate template used - When applicable, start from the domain template.

### Large Documents

- [ ] Convert when unwieldy - If a doc is difficult to navigate or edit, convert to a folder with `index.md`.
- [ ] Logical sections - Split into coherent sub-files or sub-folders.
- [ ] Relative links - Use `[Section](./section.md)` pattern.

## Path References

### Clear Across All Contexts

- [ ] Repo references - Use `repo-name/path` format (e.g., `backend-api/docs/flows.md`)
- [ ] Internal references - Use `/path` from root (e.g., `/engineering/2026/02-february/...`)
- [ ] External references - Use full URLs or clear platform-specific paths (e.g., `Drive > Campaigns > 2026 > ...`)
- [ ] No misleading prefixes - Avoid patterns that suggest incorrect structure.

### Cross-References

- [ ] Minimum necessary links - Only reference what's actually needed for context.
- [ ] Progressive discovery - Link to detailed info, don't embed it.
- [ ] References are maintained - If content moves, update the links.

## Review

### Before Publishing

- [ ] Read as a newcomer - Does it make sense without additional context?
- [ ] Check for stale info - Is anything already outdated?
- [ ] No jargon without explanation - Are domain-specific terms clear?
