# PRD: Notification Service

## 1. Purpose and Scope

### 1.1 Purpose

Build a notification service that sends alerts to users via multiple channels (email, SMS, push). This centralizes notification logic and provides a unified API for all services.

### 1.2 Scope Inclusions

- Multi-channel notification delivery (email, SMS, push)
- Template management
- Delivery status tracking
- Retry logic for failed deliveries

### 1.3 Scope Exclusions

- In-app notifications (future phase)
- User preference management (owned by user service)
- Marketing email campaigns (different system)

---

## 2. Functional Requirements

### 2.1 Notification Sending

#### 2.1.1 Send Notification

**Requirement**: Services must be able to send notifications through a single API.

**Correctness Criteria**:

- POST `/v1/notifications` accepts notification request
- Required: `user_id`, `type`, `channel`, `template_id`
- Optional: `data` (template variables), `priority`
- Returns 202 Accepted with notification ID

#### 2.1.2 Channel Selection

**Requirement**: System must deliver via specified channel.

**Correctness Criteria**:

- Supports: `email`, `sms`, `push`
- Returns 400 for unsupported channels
- Each channel has dedicated provider integration

#### 2.1.3 Template Rendering

**Requirement**: Notifications use templates with variable substitution.

**Correctness Criteria**:

- Templates support `{{variable}}` syntax
- Missing variables return validation error
- HTML templates for email, plain text for SMS

### 2.2 Delivery Tracking

#### 2.2.1 Status Tracking

**Requirement**: System must track delivery status for each notification.

**Correctness Criteria**:

- Statuses: `pending`, `sent`, `delivered`, `failed`
- GET `/v1/notifications/{id}` returns current status
- Webhook callback on status change (optional)

#### 2.2.2 Retry Logic

**Requirement**: Failed notifications must be retried automatically.

**Correctness Criteria**:

- Exponential backoff: 1m, 5m, 15m, 1h, 6h
- Max 5 retry attempts
- Mark as `failed` after max retries

---

## 3. Non-Functional Requirements

### 3.1 Reliability

#### 3.1.1 Delivery Guarantee

**Requirement**: Notifications must be delivered reliably.

**Correctness Criteria**:

- At-least-once delivery guarantee
- 99.5% delivery success rate
- Failed deliveries logged with reason

### 3.2 Performance

#### 3.2.1 Throughput

**Requirement**: System must handle notification volume.

**Correctness Criteria**:

- Support 10,000 notifications per minute
- Queue-based processing for async delivery
- P99 enqueue latency < 100ms

---

## 4. Definition of Done

This initiative is complete when:

1. **API**: Send notifications via email, SMS, push through single endpoint
2. **Templates**: Create and use templates with variable substitution
3. **Tracking**: Query delivery status for any notification
4. **Reliability**: Automatic retry with exponential backoff
5. **Documentation**: OpenAPI spec and integration guide for client services

---

## Appendix: Context

**Open Questions**:

- Priority queue implementation details?
- Provider SLA requirements for SLA-backed notifications?

**Dependencies**:

- Email provider (to be selected - see ADR)
- SMS provider (Twilio tentatively)
- Push provider (Firebase)

**Risks**:

- Provider outages may affect delivery (mitigate with fallback providers)
