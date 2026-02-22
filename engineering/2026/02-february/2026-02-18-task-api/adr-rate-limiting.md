# ADR: Rate Limiting Implementation

## Context and Problem Statement

We need to implement rate limiting to prevent any single client from overwhelming the Task API.

**Current Situation**:

- No rate limiting in place
- Single aggressive client can degrade service for all users
- Production incident on 2026-02-15 caused by runaway client

**Drivers**:

- Need to protect service availability
- Must provide fair access across clients
- Clients need visibility into their usage

---

## Decision

Implement token bucket rate limiting using Redis as the backing store.

**The chosen approach**: Redis-based distributed rate limiter with sliding window.

**Implementation outline**:

- Use Redis for rate limit state (shared across API instances)
- Token bucket algorithm with configurable limits per client
- Include rate limit headers in all responses per API Design Guidelines
- Default: 1000 requests/minute per API key

---

## Alternatives Considered

### Alternative 1: In-Memory Rate Limiting

**Description**: Store rate limit counters in application memory.

**Pros**:

- No external dependency
- Lowest latency

**Cons**:

- Doesn't work with multiple API instances
- Rate limits not truly per-client across the service

**Why not chosen**: We run multiple API instances; in-memory won't provide accurate limits.

### Alternative 2: Database-Based Rate Limiting

**Description**: Store rate limit counters in PostgreSQL.

**Pros**:

- Uses existing infrastructure
- Durable

**Cons**:

- High write load on database
- Latency impact on every request

**Why not chosen**: Redis is better suited for high-frequency counter operations.

---

## Consequences

### Positive Consequences

- Accurate rate limiting across all instances
- Redis provides sub-millisecond latency
- Scales horizontally with API instances

### Negative Consequences

- New infrastructure dependency (Redis)
- Added complexity in deployment

### Risks and Mitigations

| Risk                        | Impact | Mitigation                                                     |
| --------------------------- | ------ | -------------------------------------------------------------- |
| Redis unavailability        | High   | Fail-open: allow requests if Redis unreachable (with alerting) |
| Clock skew across instances | Low    | Use Redis timestamps, not local clocks                         |

---

## Related Decisions

- **PRD: Task API Rate Limiting** (`prd.md`) - Requirements for this feature
- **ADR: Database Choice** (`../2026-02-10-task-api/adr-database-choice.md`) - Original database decision

---

## References

- [Redis Rate Limiting Pattern](https://redis.io/glossary/rate-limiting/)
- [API Design Guidelines](../_reference/standards/api-design-guidelines.md)
