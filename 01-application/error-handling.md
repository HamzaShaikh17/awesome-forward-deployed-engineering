# Production Error Handling Patterns

Errors should be predictable, classified, observable, and safe to expose.

## Error categories

### Client errors

Examples:

- invalid input
- authentication failure
- authorization failure
- resource conflict
- rate limit

### Transient infrastructure errors

Examples:

- provider timeout
- Redis timeout
- database connection failure

These may be retryable.

### Permanent application errors

Examples:

- invalid workflow state
- unsupported model
- quota exhausted

Usually not retryable.

## Error contract

```json
{
  "error": {
    "code": "MODEL_UNAVAILABLE",
    "message": "The requested model is temporarily unavailable.",
    "request_id": "req_123"
  }
}
```

Do not expose:

- stack traces
- credentials
- provider secrets
- internal database details

## Retry rules

Retry only when the failure is likely transient.

Use:

- exponential backoff
- jitter
- maximum attempts
- deadlines

Avoid retrying:

- validation errors
- authentication errors
- deterministic business failures

## AI concern

A retry can create another LLM charge. Idempotency and cost controls therefore matter.
