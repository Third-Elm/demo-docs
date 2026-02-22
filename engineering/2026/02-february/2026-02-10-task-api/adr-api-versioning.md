# ADR: API Versioning Strategy

## Context and Problem Statement

We need a versioning strategy for the Task API that allows us to make breaking changes while maintaining backward compatibility for existing clients.

**Current Situation**:

- No existing versioning strategy
- Multiple internal services will consume this API
- Need to support multiple versions simultaneously

**Drivers**:

- Must not break existing clients when making changes
- Need clear deprecation policy
- Developers need to understand version they're using

---

## Decision

Use URL path versioning (e.g., `/v1/tasks`, `/v2/tasks`).

**The chosen approach**: Major version in URL path, support previous version for 6 months minimum.

**Implementation outline**:

- Include version in all endpoints: `/v1/tasks`
- Bump version only for breaking changes
- Add non-breaking changes to existing version
- Maintain both versions in same codebase using versioned handlers

---

## Alternatives Considered

### Alternative 1: Header-Based Versioning

**Description**: Version specified in custom header (e.g., `X-API-Version: 1`).

**Pros**:

- Cleaner URLs
- More flexible (can have minor versions)

**Cons**:

- Harder to debug (can't see version in URL)
- Caching proxies may not handle correctly
- Less common pattern

**Why not chosen**: URL versioning is more visible and easier to debug.

### Alternative 2: Query Parameter Versioning

**Description**: Version in query string (e.g., `/tasks?version=1`).

**Pros**:

- Simple to implement

**Cons**:

- Version feels like a filter rather than fundamental structure
- Easy to forget
- Caching complications

**Why not chosen**: URL path is more explicit and follows industry standards.

---

## Consequences

### Positive Consequences

- Clear which version clients are using
- Easy to route traffic between versions
- Follows common industry pattern

### Negative Consequences

- Multiple handlers to maintain during transition
- URL changes when version bumps

### Risks and Mitigations

| Risk                                | Impact | Mitigation                                                |
| ----------------------------------- | ------ | --------------------------------------------------------- |
| Long-lived v1 increases maintenance | Medium | Aggressive deprecation timeline with client communication |
| Client confusion during migration   | Low    | Clear documentation and migration guide                   |

---

## Related Decisions

- **ADR: Database Choice** (`adr-database-choice.md`) - Database selection for this API

---

## References

- [Stripe API Versioning](https://stripe.com/blog/api-versioning)
- [Microsoft REST API Guidelines](https://github.com/microsoft/api-guidelines)
