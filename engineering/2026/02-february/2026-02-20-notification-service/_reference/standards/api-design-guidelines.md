# API Design Guidelines

This document outlines REST API conventions for consistency across services.

## URL Structure

### Resource Naming

- Use plural nouns for collections: `/tasks`, `/users`
- Use kebab-case for multi-word resources: `/payment-methods`
- Nest sub-resources logically: `/users/{id}/tasks`

### Versioning

- Include version in URL path: `/v1/tasks`
- Bump version only for breaking changes
- Support previous version for at least 6 months after deprecation

## HTTP Methods

| Method | Usage                     | Idempotent |
| ------ | ------------------------- | ---------- |
| GET    | Retrieve resource(s)      | Yes        |
| POST   | Create resource           | No         |
| PUT    | Replace resource entirely | Yes        |
| PATCH  | Partial update            | Yes        |
| DELETE | Remove resource           | Yes        |

## Response Codes

### Success

- `200 OK` - Successful GET, PUT, PATCH
- `201 Created` - Successful POST (include Location header)
- `204 No Content` - Successful DELETE

### Client Errors

- `400 Bad Request` - Invalid request body/parameters
- `401 Unauthorized` - Missing or invalid authentication
- `403 Forbidden` - Authenticated but not authorized
- `404 Not Found` - Resource doesn't exist
- `422 Unprocessable Entity` - Validation errors
- `429 Too Many Requests` - Rate limit exceeded

### Server Errors

- `500 Internal Server Error` - Unexpected server error
- `503 Service Unavailable` - Temporary unavailability

## Error Response Format

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "The request was invalid",
    "details": [
      {
        "field": "email",
        "message": "Must be a valid email address"
      }
    ]
  }
}
```

## Pagination

Use cursor-based pagination for large collections:

```
GET /v1/tasks?limit=50&after=abc123
```

Response:

```json
{
  "data": [...],
  "pagination": {
    "has_more": true,
    "next_cursor": "def456"
  }
}
```

## Rate Limiting

- Include rate limit headers in all responses:

```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1708684800
```

## Authentication

- Use Bearer tokens in Authorization header
- Tokens expire after 1 hour
- Refresh tokens available via dedicated endpoint
