# Frequently Asked Questions

Common questions about using this documentation system.

## What if I don't know where something goes?

Use this decision tree:

1. **Is it a decision, requirement, or "why we do this"?**
   - Put it in this repo (GitHub) under the appropriate domain

2. **Is it a business artifact (PDF, deck, spreadsheet, etc.)?**
   - Put it in Google Drive

3. **Is it operational data that lives in a specialized system?**
   - Keep it in its platform:
     - Customer data → CRM
     - Tasks → Project management tool
     - Code → GitHub repos
     - Analytics → Analytics platform

## When should I create a new dated entry?

Create a new dated entry when:

- Starting a new initiative or project
- Making a significant decision or change
- Updating requirements based on feedback
- Changing strategy or approach
- Completing a phase and starting the next one

## When should I use `_independent/`?

Use the `_independent/` folder for:

- Small changes that don't need a full folder structure
- Bug fixes or minor updates
- Quick decisions that don't require multiple documents
- Standalone items that don't fit into a larger initiative

## Can I ever update old files?

The general rule is **no** - old files are never updated. This preserves history and means you don't need to maintain outdated documentation.

**Exceptions:**

- Fixing typos or formatting
- Adding clarification notes (clearly marked as additions)

## What goes in a retro?

A retro (retrospective) document captures:

- What worked well
- What didn't work
- Lessons learned
- What we'd do differently
- Follow-up actions or next steps

Retro templates are available in each domain's `_templates/` folder.

## How do I name my initiative?

Use this format: `YYYY-MM-DD-descriptive-name/`

**Examples:**

- `2026-02-10-task-api/`
- `2026-02-20-notification-service/`
- `2026-02-22-documentation-system/`

**Tips:**

- Use kebab-case (lowercase with hyphens)
- Make it descriptive but concise
- Include the phase if it's part of a series
- Focus on what the initiative is, not what you hope it will achieve

## What's the difference between PRD, ADR, and other docs?

Different domains use different document types:

**Engineering:**

- PRD (Product Requirements Document) - What we're building and why
- ADR (Architecture Decision Record) - Why we made a technical choice
- SDP (Software Development Plan) - How we'll build it
- SDR (Security Decision Record) - Security choices and rationale

**Company:**

- CDR (Company Decision Record) - Business or organizational decisions

**Marketing:**

- Campaign Brief - What we're testing and why
- Hypothesis Document - What we believe and how we'll test it
- Results Document - What happened and what we learned

See individual domain READMEs for templates and specific guidance.

## How do I handle document updates over multiple iterations?

Use a **delta-only approach**: each new dated entry contains only what changed, with a link back to prior work.

**Example:**

- `2026-02-10-task-api/prd.md` - Full foundational PRD
- `2026-02-18-task-api/prd.md` - Only new requirements, with link: `**Previous Work**: [2026-02-10: Initial PRD](../2026-02-10-task-api/prd.md)`

**Why delta-only:**

- Clear what changed between iterations
- Smaller, reviewable PRs
- True immutability (no copying entire documents)
- Git history shows evolution naturally

**When requirements supersede prior ones:**

State it explicitly in the delta document (e.g., "Section 4.2 supersedes 2026-02-10 Section 4.2"). This clarifies which parts readers should ignore from prior entries.

**When to create a consolidated snapshot:**

If a project accumulates many deltas (roughly 4-5+) and traversing the chain becomes burdensome, create a new dated entry that consolidates everything:

- `2026-03-01-task-api/prd.md` - Consolidated snapshot with full current state

This doesn't violate immutability—it's a new dated entry that happens to be comprehensive. Future deltas then reference this new baseline, resetting the chain length.

## What if a document gets too large?

When a document becomes difficult to navigate or edit, convert it to a folder:

1. Rename `sdp.md` to `sdp/`
2. Create `sdp/index.md` as the entry point
3. Split content into sub-files like `architecture.md`, `data-models.md`
4. Sub-folders can be nested as deep as needed
5. Link between files using relative paths

See [Folder Structure](./FOLDER_STRUCTURE.md) for examples.
