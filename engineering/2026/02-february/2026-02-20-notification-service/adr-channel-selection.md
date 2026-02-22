# ADR: Email Provider Selection

## Context and Problem Statement

We need to select an email provider for the notification service that can handle transactional emails with high deliverability.

**Current Situation**:

- No existing email infrastructure
- Need to send ~100K emails/day initially
- Deliverability is critical (password resets, alerts)

**Drivers**:

- High deliverability rate (>98%)
- Easy integration via API
- Reasonable pricing at our scale

---

## Decision

Use SendGrid as the primary email provider.

**The chosen approach**: SendGrid with dedicated IP and domain authentication.

**Implementation outline**:

- Integrate via REST API
- Set up SPF, DKIM, DMARC for domain authentication
- Use dedicated IP for better reputation control
- Webhook for delivery status tracking

---

## Alternatives Considered

### Alternative 1: Amazon SES

**Description**: AWS email service.

**Pros**:

- Lower cost ($0.10 per 1000 emails vs SendGrid $14.95/1000 at our volume)
- Integrated with existing AWS infrastructure

**Cons**:

- Higher learning curve for deliverability
- Less robust analytics
- Support is AWS-standard (can be slow)

**Why not chosen**: SendGrid has better deliverability tools and analytics for our use case.

### Alternative 2: Mailgun

**Description**: Email API provider with good deliverability.

**Pros**:

- Good API and documentation
- Competitive pricing

**Cons**:

- Less market presence than SendGrid
- Smaller community

**Why not chosen**: SendGrid has larger ecosystem and better long-term outlook.

### Alternative 3: Postmark

**Description**: Transactional email focused provider.

**Pros**:

- Excellent deliverability reputation
- Simple, focused on transactional email

**Cons**:

- Higher cost at scale
- Fewer features (templates less flexible)

**Why not chosen**: SendGrid's template system better matches our needs.

---

## Consequences

### Positive Consequences

- High deliverability with proven provider
- Good analytics and debugging tools
- Template editor for non-technical users

### Negative Consequences

- Higher cost than SES
- Vendor lock-in (mitigated by abstraction layer)

### Risks and Mitigations

| Risk            | Impact | Mitigation                                            |
| --------------- | ------ | ----------------------------------------------------- |
| Provider outage | High   | Build abstraction layer to switch providers if needed |
| Cost growth     | Medium | Monitor usage, evaluate alternatives at scale         |

---

## Related Decisions

- **PRD: Notification Service** (`prd.md`) - Overall requirements
- **SDP: Notification Service** (`sdp.md`) - Implementation details

---

## References

- [SendGrid API Documentation](https://docs.sendgrid.com/api-reference)
