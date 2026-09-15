# Rate Limiting

Rate limiting protects availability, providers, and AI spend.

## Dimensions

Rate limit by more than IP:

- user
- organization
- API key
- endpoint
- model
- tokens
- concurrent jobs

## Algorithms

### Fixed window

Simple but allows boundary bursts.

### Sliding window

More accurate traffic smoothing.

### Token bucket

Allows controlled bursts while maintaining a refill rate.

### Leaky bucket

Smooths processing at a controlled rate.

## AI-specific limits

```text
requests/minute
tokens/minute
concurrent LLM calls
documents/hour
GPU jobs
monthly spend
```

## Response

Use:

```http
429 Too Many Requests
Retry-After: 30
```

## Distributed implementation

Use shared state such as Redis when multiple application instances enforce a common limit.

## Rate limiting is not concurrency limiting

Rate limit controls frequency.

Concurrency limit controls work happening simultaneously.

For AI, you often need both.
