# CDR: Adopt Agentic Documentation System

## Context and Problem Statement

We need a documentation system that preserves decision history and is navigable by AI agents. Current documentation in wikis and shared drives becomes stale quickly and loses the "why" behind decisions.

**Current Situation**:

- Documentation scattered across wikis, Drive, and repo READMEs
- No clear history of why decisions were made
- AI agents cannot effectively navigate our knowledge
- Documents updated in place, losing historical context

**Drivers**:

- Need to preserve decision rationale for future reference
- AI coding assistants need structured context to work effectively
- Team growth requires better knowledge preservation
- Regulatory requirements for decision auditability

---

## Decision

Adopt an event-sourced documentation system stored in a Git repository.

**The chosen approach**: Immutable, dated documentation entries organized by domain with template snapshots.

**Implementation outline**:

- Create `demo-docs` repository with domain structure
- Store decisions, requirements, and "why" (not operational data)
- Each project gets dated folder with snapshot of current standards
- Never update old files - create new dated entries instead

---

## Alternatives Considered

### Alternative 1: Continue with Wiki

**Description**: Keep using existing wiki with better maintenance discipline.

**Pros**:

- No migration effort
- Familiar to team

**Cons**:

- Wiki updates still erase history
- AI agents struggle with wiki navigation
- Discipline degrades over time

**Why not chosen**: Structural problem, not discipline problem. Wiki architecture doesn't support immutability.

### Alternative 2: Notion Database

**Description**: Use Notion with database views for documentation.

**Pros**:

- Good UI for non-technical users
- Built-in history tracking

**Cons**:

- Notion API limits AI agent access
- Lock-in to single vendor
- Doesn't integrate with code workflow

**Why not chosen**: Git-based approach works better with AI tools and existing developer workflows.

### Alternative 3: Documentation in Code Repos

**Description**: Put all docs alongside code in their respective repos.

**Pros**:

- Docs stay close to code
- Automatic versioning with code

**Cons**:

- Cross-project decisions have no natural home
- Company/business docs don't fit in code repos
- Harder for AI to discover across repos

**Why not chosen**: Need central location for cross-cutting decisions and non-technical documentation.

---

## Consequences

### Positive Consequences

- Complete audit trail of all decisions
- AI agents can navigate documentation effectively
- Reduced maintenance burden (no "update the docs" tasks)
- Clear separation between "why" (docs) and "what" (code/data)

### Negative Consequences

- Learning curve for team on new system
- Some duplication of standards in project snapshots
- Non-developers need to learn Git workflow

### Risks and Mitigations

| Risk               | Impact | Mitigation                                          |
| ------------------ | ------ | --------------------------------------------------- |
| Team doesn't adopt | High   | Training sessions, clear templates, make it easy    |
| Snapshot bloat     | Low    | Standards stay small, Git handles duplication well  |
| Non-dev access     | Medium | Web-based Git editors (GitHub.dev) for easy editing |

---

## Related Decisions

None yet - this is the foundational decision.

---

## References

- [Agentic Documentation System (Blog Post)](https://example.com/blog/agentic-documentation-system)
- [Event Sourcing Pattern](https://martinfowler.com/eaaDev/EventSourcing.html)
