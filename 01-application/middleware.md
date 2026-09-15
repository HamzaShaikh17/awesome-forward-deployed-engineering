# Middleware

Middleware is code that runs around request processing.

```text
Request
  ↓
Middleware
  ↓
Route
  ↓
Use case
  ↓
Response
```

## Good middleware responsibilities

- Request ID / correlation ID
- Authentication context extraction
- Access logging
- CORS
- Security headers
- Rate limiting
- Timing metrics
- Request size limits

## Avoid putting business logic in middleware

Do not put:

- quota calculations
- document ownership rules
- model eligibility
- complex domain decisions

in generic middleware.

## Ordering matters

A typical pipeline:

```text
TLS / edge
→ request ID
→ security
→ authentication
→ rate limit
→ validation
→ route
→ application
```

Exact ordering depends on the framework and threat model.

## AI-specific example

A request ID should flow through:

```text
HTTP request
→ API
→ queue message
→ worker
→ LLM provider call
→ webhook
```

This enables end-to-end tracing.
