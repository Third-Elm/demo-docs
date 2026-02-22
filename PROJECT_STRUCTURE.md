# Project Structure Guide

This document explains the repository structure for creating new projects.

## Month Structure

Each month folder contains projects and tracking files:

```
domain/YYYY/MM-month/
├── YYYY-MM-DD-project-slug/
│   ├── _reference/        # Snapshot of domain _reference at creation time
│   ├── _templates/        # Snapshot of domain _templates at creation time
│   └── [decision records]
└── project-slugs.md       # List of all project slugs in this month
```

## project-slugs.md

Every month folder that contains projects must include a `project-slugs.md` file:

```
# Project Slugs - February 2026

- documentation-system
- task-api
```

**Purpose**: Enables agents to quickly discover all projects in a month.

## Project Snapshots

Each project folder includes snapshots of `_reference` and `_templates` from its domain at creation time.

**Why**: Templates and reference materials evolve. Snapshots preserve the exact rules and context that applied when the project was created.

**What to copy**:

- Entire `<domain>/_reference/` folder
- Entire `<domain>/_templates/` folder

**Where**: Into the project folder as `project-slug/_reference/` and `project-slug/_templates/`

## Domain Structure

Each domain follows the same pattern:

```
<domain>/
├── _templates/         # Document templates for this domain
├── _reference/         # Static reference materials
└── YYYY/
    └── MM-month/
        ├── project-slugs.md
        ├── YYYY-MM-DD-project-slug/
        │   ├── _reference/      # Snapshot from domain
        │   ├── _templates/      # Snapshot from domain
        │   └── [decision records]
        └── _independent/
            └── YYYY-MM-DD-small-change.md
```

## File Naming Conventions

### Project Folders

- Format: `YYYY-MM-DD-descriptive-name/`
- Example: `2026-02-10-task-api/`
- Use kebab-case
- The descriptive name becomes the project slug

### Independent Changes

- Format: `YYYY-MM-DD-description.md`
- Example: `2026-02-15-fix-api-timeout-bug.md`
- Used for small changes that don't need a full folder structure
- Located in `_independent/` subdirectory within each month

### Decision Records

- Format: `{type}-decision-title.md`
- Example: `adr-database-choice.md`
- Use the appropriate type prefix (adr, cdr, etc.)
- Use kebab-case for the title

## Context Discovery for Agents

When working with a project:

1. **Navigate to domain folder**: `cd <domain>/`
2. **Find the project slug**: Check `project-slugs.md` in relevant month
3. **Start from latest entry**: Find newest dated folder with matching slug
4. **Use project's snapshots**: Reference `_reference/` and `_templates/` inside the project folder
5. **Work backwards if needed**: Only explore older entries if current context is insufficient

## What Goes Where

| Content Type                     | Location                         |
| -------------------------------- | -------------------------------- |
| Decisions, requirements, "why"   | This repo (dated entries)        |
| Code                             | GitHub repos                     |
| Business artifacts (PDFs, decks) | Google Drive                     |
| Operational data                 | Specialized platforms (CRM, etc) |

## Cross-References

- **Repo references**: Use `repo-name/path` format
- **Internal references**: Use `/path` from root
- **External references**: Use full URLs or platform-specific paths

See [CROSS_REFERENCES.md](./CROSS_REFERENCES.md) for detailed patterns.

## Large Document Breakdown

When a document becomes unwieldy, break it down. See [FOLDER_STRUCTURE.md](./FOLDER_STRUCTURE.md) for more info.

## For Agents Creating New Projects

1. Create dated folder: `YYYY-MM-DD-project-slug/`
2. Copy `_reference/` folder from domain
3. Copy `_templates/` folder from domain
4. Add project slug to `project-slugs.md` in month folder
5. Create project files using copied templates
6. Follow [CONTRIBUTING.md](./CONTRIBUTING.md) checklist
