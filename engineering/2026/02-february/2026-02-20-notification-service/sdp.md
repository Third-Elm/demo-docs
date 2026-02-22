# SDP: Notification Service

## 0. Context and Scope

### 0.1 Related Documents

| Document                | Link                       | Purpose                               |
| ----------------------- | -------------------------- | ------------------------------------- |
| **PRD**                 | `prd.md`                   | Requirements and correctness criteria |
| **ADR: Email Provider** | `adr-channel-selection.md` | Email provider decision               |

### 0.2 What We're Building

A notification service that accepts notification requests via API, routes them through appropriate channels (email, SMS, push), and tracks delivery status. Uses queue-based processing for reliability.

### 0.3 Implementation Approach

API accepts requests → Queue for processing → Worker delivers via provider → Track status in database. Retry failed deliveries with exponential backoff.

---

## 1. Scope of Implementation

### 1.1 Services and Repositories

| Service/Repo           | Involvement | Changes Required     |
| ---------------------- | ----------- | -------------------- |
| `notification-service` | New         | Complete new service |

### 1.2 External Providers and Systems

| Provider       | Purpose            | Interaction Type |
| -------------- | ------------------ | ---------------- |
| SendGrid       | Email delivery     | REST API         |
| Twilio         | SMS delivery       | REST API         |
| Firebase (FCM) | Push notifications | SDK              |
| Redis          | Job queue          | Protocol         |

---

## 2. Core Contracts and Types

### 2.1 Notification Request

**File**: `notification-service/src/types.ts`

```typescript
interface NotificationRequest {
  user_id: string;
  type: NotificationType;
  channel: Channel;
  template_id: string;
  data?: Record<string, string>;
  priority?: "normal" | "high";
}

type Channel = "email" | "sms" | "push";
type NotificationType = "alert" | "reminder" | "transactional";
```

**Purpose**: Request body for creating a notification.

### 2.2 Notification Status

```typescript
interface NotificationStatus {
  id: string;
  status: "pending" | "sent" | "delivered" | "failed";
  channel: Channel;
  created_at: string;
  updated_at: string;
  error?: string;
  retry_count: number;
}
```

**Purpose**: Response for status queries.

---

## 3. System Architecture

### 3.1 Component Overview

| Component  | Purpose                      | Dependencies              |
| ---------- | ---------------------------- | ------------------------- |
| API Server | Accept notification requests | Redis, PostgreSQL         |
| Worker     | Process queue and deliver    | Redis, External Providers |
| Scheduler  | Retry failed notifications   | Redis                     |

### 3.2 Architecture Visual

```
                    ┌─────────────┐
                    │   Client    │
                    │  Services   │
                    └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │  API Layer  │
                    │  (Fastify)  │
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
        ┌──────────┐ ┌──────────┐ ┌──────────┐
        │PostgreSQL│ │  Redis   │ │  Redis   │
        │  (State) │ │ (Queue)  │ │ (Cache)  │
        └──────────┘ └────┬─────┘ └──────────┘
                        │
                        ▼
                 ┌─────────────┐
                 │   Worker    │
                 │  (BullMQ)   │
                 └──────┬──────┘
                        │
        ┌───────────────┼───────────────┐
        ▼               ▼               ▼
   ┌─────────┐    ┌─────────┐    ┌─────────┐
   │SendGrid │    │ Twilio  │    │ Firebase│
   │ (email) │    │  (sms)  │    │  (push) │
   └─────────┘    └─────────┘    └─────────┘
```

---

## 4. Implementation Phases

### Phase 1: Core Infrastructure

**Goal**: Set up service skeleton and database.

**Tasks**:

- [ ] Initialize `notification-service` repo
- [ ] Set up PostgreSQL schema (notifications, templates)
- [ ] Set up Redis connection
- [ ] Create basic API server with health check

**Success Criteria**: Service starts, health check returns 200.

---

### Phase 2: Email Channel

**Goal**: Implement email notification flow.

**Tasks**:

- [ ] Implement notification API endpoint
- [ ] Set up SendGrid integration
- [ ] Create email template system
- [ ] Implement worker for email processing
- [ ] Add status tracking

**Success Criteria**: Can send email via API, status tracked correctly.

---

### Phase 3: Additional Channels

**Goal**: Add SMS and push notification support.

**Tasks**:

- [ ] Add Twilio integration for SMS
- [ ] Add Firebase integration for push
- [ ] Update worker for multi-channel routing
- [ ] Add channel-specific validation

**Success Criteria**: All three channels work via single API.

---

### Phase 4: Reliability

**Goal**: Add retry logic and monitoring.

**Tasks**:

- [ ] Implement exponential backoff retry
- [ ] Add dead letter queue for failed notifications
- [ ] Set up monitoring and alerting
- [ ] Add delivery webhooks (optional)

**Success Criteria**: Failed notifications retry correctly, 99.5% delivery rate.

---

## 5. Detailed Task Breakdown

| #   | Task                  | Description                                 | Effort |
| --- | --------------------- | ------------------------------------------- | ------ |
| 1   | Initialize repo       | Set up TypeScript, Fastify, basic structure | 1 day  |
| 2   | Database schema       | Create tables for notifications, templates  | 1 day  |
| 3   | SendGrid integration  | API client, template rendering              | 2 days |
| 4   | Queue setup           | BullMQ with Redis                           | 1 day  |
| 5   | Worker implementation | Process jobs, call providers                | 3 days |
| 6   | SMS integration       | Twilio client                               | 1 day  |
| 7   | Push integration      | Firebase client                             | 1 day  |
| 8   | Retry logic           | Exponential backoff, dead letter            | 2 days |
| 9   | Monitoring            | Metrics, alerts, dashboards                 | 2 days |
| 10  | Documentation         | OpenAPI, integration guide                  | 1 day  |

**Total**: ~15 days

---

## 6. Data Structures

### 6.1 Notifications Table

**Table**: `notifications`

```sql
CREATE TABLE notifications (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id VARCHAR(255) NOT NULL,
  type VARCHAR(50) NOT NULL,
  channel VARCHAR(20) NOT NULL,
  template_id VARCHAR(255) NOT NULL,
  data JSONB,
  priority VARCHAR(20) DEFAULT 'normal',
  status VARCHAR(20) DEFAULT 'pending',
  error TEXT,
  retry_count INTEGER DEFAULT 0,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE INDEX idx_notifications_user ON notifications(user_id);
CREATE INDEX idx_notifications_status ON notifications(status);
CREATE INDEX idx_notifications_created ON notifications(created_at);
```

### 6.2 Templates Table

**Table**: `templates`

```sql
CREATE TABLE templates (
  id VARCHAR(255) PRIMARY KEY,
  channel VARCHAR(20) NOT NULL,
  subject TEXT,
  body TEXT NOT NULL,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);
```

---

## 7. Risk Mitigation

| Risk            | Probability | Impact | Mitigation Strategy                   |
| --------------- | ----------- | ------ | ------------------------------------- |
| Provider outage | Medium      | High   | Abstract provider interface, can swap |
| Queue backlog   | Medium      | Medium | Scale workers, alert on queue depth   |
| Template errors | Low         | Low    | Validate variables before sending     |

---

## 8. Success Criteria

This initiative is complete when:

1. **API**: Single endpoint accepts notifications for all channels
2. **Delivery**: Email, SMS, and push all functional with provider integrations
3. **Tracking**: Status queryable for any notification
4. **Reliability**: Retry logic handles transient failures
5. **Performance**: P99 enqueue latency < 100ms, 10K notifications/minute
