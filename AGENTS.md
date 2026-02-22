# Agent Guidelines

This file contains operational information agents need when working with this repository.

## First Step

**Always read [README.md](./README.md) before starting any task.** It provides core principles and quick start context.

Then read [PROJECT_STRUCTURE.md](./PROJECT_STRUCTURE.md) to understand the repository organization and patterns for working with projects.

## Context Discovery Pattern

When you need context about a project, the repo uses an event-sourcing pattern. Navigate to the appropriate domain folder, then start from the LATEST dated entry for the project slug you need. Work backwards in time only if you need more historical context.

The project slug remains consistent across dates (e.g., `task-api` appears as `2026-02-10-task-api/`, `2026-02-18-task-api/`, etc.).

Use `project-slugs.md` in month folders to quickly discover projects in that month.

## Creating Documentation

Before creating documentation: read [CONTRIBUTING.md](./CONTRIBUTING.md) for content principles and checklist.
