# PRD: Task API

## 1. Purpose and Scope

### 1.1 Purpose

Build a REST API for task management that internal services can use to create, track, and complete tasks. This provides a unified task system instead of each service implementing its own.

### 1.2 Scope Inclusions

- CRUD operations for tasks
- Task filtering and pagination
- Task assignment to users
- Due date tracking

### 1.3 Scope Exclusions

- Real-time notifications (future phase)
- Mobile SDK (out of scope)
- Public API access (internal only for now)

---

## 2. Functional Requirements

### 2.1 Task Management

#### 2.1.1 Create Task

**Requirement**: Users must be able to create a new task with title, description, and optional due date.

**Correctness Criteria**:

- POST to `/v1/tasks` returns 201 with created task
- Required fields: `title` (string, 1-200 chars)
- Optional fields: `description`, `due_date`, `assignee_id`
- `created_at` and `id` are auto-generated

#### 2.1.2 List Tasks

**Requirement**: Users must be able to list tasks with filtering and pagination.

**Correctness Criteria**:

- GET `/v1/tasks` returns paginated list
- Filter by: `status`, `assignee_id`
- Default sort: `created_at` descending
- Maximum 100 results per page

#### 2.1.3 Update Task

**Requirement**: Users must be able to update task properties.

**Correctness Criteria**:

- PATCH `/v1/tasks/{id}` returns 200 with updated task
- Partial updates supported
- `updated_at` timestamp auto-updated

#### 2.1.4 Complete Task

**Requirement**: Users must be able to mark a task as complete.

**Correctness Criteria**:

- PATCH `/v1/tasks/{id}` with `{"status": "completed"}` works
- `completed_at` timestamp auto-set
- Cannot reopen completed tasks (future requirement)

---

## 3. Non-Functional Requirements

### 3.1 Performance

#### 3.1.1 Response Time

**Requirement**: API must respond within acceptable latency thresholds.

**Correctness Criteria**:

- P95 latency < 200ms for all read operations
- P95 latency < 500ms for all write operations
- Measured at the API gateway

### 3.2 Reliability

#### 3.2.1 Availability

**Requirement**: API must be highly available.

**Correctness Criteria**:

- 99.9% uptime SLA
- Automatic failover within 30 seconds
- Health check endpoint at `/health`

---

## 4. Definition of Done

This initiative is complete when:

1. **CRUD Operations**: Create, read, update, delete tasks via REST API
2. **Filtering**: Filter by status and assignee, with pagination
3. **Performance**: P95 latency under 200ms for reads
4. **Documentation**: OpenAPI spec published and accurate
5. **Testing**: >90% code coverage, all endpoints tested

---

## Appendix: Context

**Open Questions**:

- Should we support bulk operations in v1?
- What's the retention policy for completed tasks?

**Dependencies**:

- Auth service must be available for token validation

**Risks**:

- Database choice affects scalability (see ADR)
