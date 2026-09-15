# Production Logging Structure

Logs should answer:

- What happened?
- Where?
- For whom/which tenant?
- Which request/job?
- How long?
- What failed?
- Is it retryable?

## Prefer structured JSON

```json
{
  "timestamp": "2026-09-08T10:00:00Z",
  "level": "INFO",
  "event": "llm_request_completed",
  "request_id": "req_123",
  "job_id": "job_456",
  "org_id": "org_789",
  "model": "example-model",
  "latency_ms": 1840,
  "input_tokens": 1200,
  "output_tokens": 400
}
```

## Never log

- passwords
- API keys
- access tokens
- refresh tokens
- raw secrets
- unnecessary PII
- full sensitive prompts

## Event names

Prefer stable event names:

- `request_started`
- `request_completed`
- `llm_request_started`
- `llm_request_completed`
- `job_failed`
- `webhook_delivery_failed`

## Correlation

Propagate:

- request_id
- trace_id
- job_id
- tenant/org identifier where safe

## AI observability

Track:

- latency
- tokens
- model
- provider
- retries
- cache hit/miss
- cost estimate
- safety/evaluation outcomes
