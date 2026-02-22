# Agentic Documentation System Demo

This repository demonstrates an event-sourced documentation system designed for LLM agent navigation. It contains time-stamped records of decisions across Engineering, Company, and Marketing domains.

## Core Principles

1. **Date Everything** - Each significant change is a new dated entry. No retroactive updates.
2. **Context, Not Data** - Docs capture decisions and "why we got here." Data lives in domain systems.
3. **Single Source of Truth** - Code in repos, business data in platforms, docs for requirements/planning.

## Quick Start

Everything is organized by date under each domain:

```
engineering/2026/02-february/2026-02-10-task-api/
company/2026/02-february/2026-02-22-documentation-system/
marketing/2026/02-february/2026-02-12-product-launch-campaign/
```

When something changes, create a new dated entry. Never update old files.

## Where Things Go

| What                                | Where                             |
| ----------------------------------- | --------------------------------- |
| Decisions, requirements, "why"      | This repo (GitHub)                |
| Code                                | GitHub repos                      |
| Business artifacts (PDFs, decks)    | Google Drive                      |
| Operational data (customers, tasks) | Specialized platforms (CRM, etc.) |

## Domains

- [Engineering](./engineering/) - Technical decisions and architecture
- [Company](./company/) - Organizational structure and company-wide decisions
- [Marketing](./marketing/) - Campaigns, experiments, messaging

## More Information

- [Project Structure](./PROJECT_STRUCTURE.md) - Project file structure
- [Folder Structure](./FOLDER_STRUCTURE.md) - Organization patterns and naming conventions
- [Cross-Reference Pattern](./CROSS_REFERENCES.md) - How to link to Drive, repos, and issues
- [FAQ](./FAQ.md) - Common questions about using this system
