# Folder Structure and Naming Conventions

## Domain Folder Template

Each domain follows the same pattern:

```
<domain>/
├── _templates/         # Document templates for this domain
├── _reference/         # Static reference materials
└── YYYY/
    └── MM-month/
        ├── project-slugs.md
        ├── YYYY-MM-DD-initiative-name/
        │   ├── _reference/         # Snapshot of domain _reference at creation time
        │   ├── _templates/         # Snapshot of domain _templates at creation time
        │   ├── <domain-specific-docs>
        │   ├── <decision-records>
        │   └── retro.md
        └── _independent/
            └── YYYY-MM-DD-small-change.md
```

## File Naming Conventions

### Initiative Folders

- Format: `YYYY-MM-DD-descriptive-name/`
- Example: `2026-02-10-task-api/`
- Use kebab-case
- Make the name descriptive but concise

### Independent Changes

- Format: `YYYY-MM-DD-description.md`
- Example: `2026-02-15-fix-api-timeout-bug.md`
- Used for small changes that don't need a full folder structure
- Located in `_independent/` subdirectory within each month

### Decision Records

- Format: `NNN-decision-title.md`
- Example: `{type}-database-choice.md`
- Use kebab-case for the title

## Large Document Breakdown

When a single document becomes too large, convert it to a folder with the template sections as individual files (and break it down as necessary):

```
2026-02-20-large-initiative/
├── _reference/
├── _templates/
├── prd.md
├── sdp/
│   ├── 00-context.md
│   ├── 01-architecture.md
│   ├── 02-data-models.md
│   └── ...
├── adr-database-choice/
│   ├── 00-context.md
│   └── 01-decision.md
└── retro.md
```

**Guidelines:**

- Convert a file to a folder when it becomes difficult to navigate or edit
- The folder name matches the original file name
- Files follow the source template structure
- Sub-folders can be nested as deep as needed
- Link between files using relative paths: `[Data Modeling](./data-modeling.md)`

## Example Initiative Structure

```
engineering/2026/02-february/
├── 2026-02-10-task-api/
│   ├── _reference/                   # Snapshot from domain
│   ├── _templates/                   # Snapshot from domain
│   ├── prd.md                        # Product requirements
│   ├── adr-database-choice.md        # Architecture decision record
│   └── adr-api-versioning.md         # Another decision
│
├── 2026-02-18-task-api/
│   ├── _reference/                   # Snapshot from domain
│   ├── _templates/                   # Snapshot from domain
│   ├── prd.md                        # New requirements based on feedback
│   └── adr-rate-limiting.md          # New decision
│
└── 2026-02-20-notification-service/
    ├── _reference/                   # Snapshot from domain
    ├── _templates/                   # Snapshot from domain
    ├── prd.md
    ├── adr-channel-selection.md
    └── sdp.md
```

## Key Rule

Old files are never updated. When things change, create a new dated entry. This preserves history and reduces maintenance.
