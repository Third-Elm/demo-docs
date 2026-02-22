# ADR: Database Choice for Task API

## Context and Problem Statement

We need to choose a database for the Task API. The database must support CRUD operations, filtering, and scale to millions of tasks.

**Current Situation**:

- No existing task database
- Other services use PostgreSQL
- Task data is relational (tasks, users, assignments)

**Drivers**:

- Need to support complex queries (filter by status, assignee, date range)
- Must scale to millions of tasks
- Team has PostgreSQL experience

---

## Decision

Use PostgreSQL as the primary database for Task API.

**The chosen approach**: PostgreSQL with standard indexing strategy.

**Implementation outline**:

- Use managed PostgreSQL (RDS)
- Create indexes on frequently queried columns
- Use connection pooling (PgBouncer)

---

## Alternatives Considered

### Alternative 1: MongoDB

**Description**: Document store with flexible schema.

**Pros**:

- Flexible schema for task metadata
- Horizontal scaling built-in

**Cons**:

- Less mature transaction support
- Team has less experience
- Query patterns are well-known (relational fits better)

**Why not chosen**: Our data is relational, and team expertise is in PostgreSQL.

### Alternative 2: DynamoDB

**Description**: Managed NoSQL database.

**Pros**:

- Fully managed, no server maintenance
- Predictable performance at scale

**Cons**:

- Limited query flexibility
- Requires careful access pattern design upfront
- Vendor lock-in

**Why not chosen**: Query patterns require flexibility (filtering by multiple attributes) that's harder with DynamoDB.

---

## Consequences

### Positive Consequences

- Team can leverage existing PostgreSQL expertise
- Consistent with other services in our stack
- Mature tooling and ecosystem

### Negative Consequences

- Vertical scaling limits (can be mitigated with read replicas)
- Requires manual index management

### Risks and Mitigations

| Risk                         | Impact | Mitigation                                 |
| ---------------------------- | ------ | ------------------------------------------ |
| Slow queries on large tables | High   | Proactive index strategy, query monitoring |
| Connection exhaustion        | Medium | Use PgBouncer for connection pooling       |

---

## Related Decisions

- **ADR: API Versioning** (`adr-api-versioning.md`) - How we version the API

---

## References

- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
