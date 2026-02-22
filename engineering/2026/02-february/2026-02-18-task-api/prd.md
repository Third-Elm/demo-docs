# PRD: Task API - Rate Limiting

**Previous Work**: [2026-02-10: Initial PRD](../2026-02-10-task-api/prd.md)

## Delta Summary

This update adds rate limiting and bulk operations to the Task API based on production learnings.

---

## 2. Functional Requirements (Additions Only)

### 2.2 Rate Limiting

#### 2.2.1 Rate Limit Enforcement

**Requirement**: API must enforce rate limits per client.

**Correctness Criteria**:

- Default limit: 1000 requests per minute per API key
- Returns 429 when limit exceeded
- Rate limit headers included in all responses (see API Design Guidelines)

#### 2.2.2 Bulk Task Creation

**Requirement**: Users must be able to create multiple tasks in a single request.

**Correctness Criteria**:

- POST `/v1/tasks/bulk` accepts array of up to 100 tasks
- Returns 207 Multi-Status with individual results
- Partial success supported (some can fail, others succeed)

---

## 3. Non-Functional Requirements (Additions Only)

### 3.3 Scalability

#### 3.3.1 Throughput

**Requirement**: API must handle increased load with rate limiting in place.

**Correctness Criteria**:

- Support 10,000 requests per second across all clients
- Rate limiter adds <10ms latency overhead

---

## 4. Definition of Done

**Supersedes**: Section 4 from 2026-02-10

This initiative is complete when:

1. **Rate Limiting**: All endpoints enforce per-client limits with headers
2. **Bulk Operations**: Create up to 100 tasks in single request
3. **Performance**: P95 latency still under 200ms (rate limiter overhead acceptable)
4. **Documentation**: OpenAPI spec updated with new endpoints and headers
5. **Testing**: Rate limit behavior tested at boundary conditions

---

## Appendix: Context

**Why This Update**:

- Production monitoring showed single client can overwhelm the API
- Users requested bulk creation for data migration scenarios

**Dependencies**:

- Redis cluster for distributed rate limiting
