# Webhooks

A webhook is an HTTP callback sent when an event occurs.

```text
Event
 ↓
Webhook queue
 ↓
Delivery worker
 ↓
Customer endpoint
```

## Why async?

The customer's endpoint may:

- timeout
- return 500
- be unavailable
- respond slowly

Never make the core transaction depend on synchronous webhook delivery.

## Payload

```json
{
  "id": "evt_123",
  "type": "analysis.completed",
  "version": "v1",
  "created_at": "2026-09-08T10:00:00Z",
  "data": {
    "job_id": "job_456"
  }
}
```

## Security

Sign payloads with an HMAC secret.

Conceptually:

```text
signature = HMAC-SHA256(secret, raw_request_body)
```

Verify using constant-time comparison.

## Retry

Use:

- exponential backoff
- jitter
- maximum attempts
- DLQ/manual replay

## Idempotency

Consumers should use the event ID to prevent duplicate effects.

## Operational data

Track:

- delivery attempt
- response status
- latency
- next retry
- final status
