# Fix: API Timeout Bug

**Date**: 2026-02-15

**Status**: Resolved

## Problem

The `/v1/tasks` endpoint was timing out after 30 seconds when queries included filters with large result sets. Users reported seeing 504 Gateway Timeout errors.

## Root Cause

The database query was performing a full table scan when filtering by `status` because the composite index didn't include the `status` column as the leading column.

## Solution

Added a new composite index:

```sql
CREATE INDEX idx_tasks_status_created ON tasks(status, created_at DESC);
```

## Verification

- Query plan now shows index scan instead of sequential scan
- P95 latency reduced from 28s to 150ms
- No 504 errors in the 24 hours since deployment

## Related

- **PRD**: [2026-02-10-task-api](../2026-02-10-task-api/prd.md)
- **Commit**: `task-api@abc123`
