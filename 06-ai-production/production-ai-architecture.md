# Production AI Architecture — Synthesis

A production AI product combines the concepts in this repository.

## Reference architecture

```text
                    Internet
                       |
                 DNS + TLS
                       |
                L7 Load Balancer
                       |
                 API containers
                       |
        +--------------+--------------+
        |              |              |
      Auth          Redis          Postgres
        |              |              |
        +--------------+--------------+
                       |
                     Queue
                       |
              +--------+--------+
              |                 |
        CPU workers       GPU/AI workers
              |                 |
              +--------+--------+
                       |
              Model / LLM Providers
                       |
                Usage + tracing
                       |
                Webhook service
```

## Request path

```text
Request
→ TLS
→ load balancer
→ authentication
→ rate limit
→ validation
→ use case
→ cache/database
→ queue or LLM
→ response
```

## Production controls

### Reliability

- timeouts
- retries
- circuit breakers where justified
- queues
- DLQs
- health/readiness checks
- graceful shutdown

### Security

- IAM
- least privilege
- tenant isolation
- secret management
- signed webhooks
- TLS

### AI cost

- token limits
- concurrency limits
- rate limits
- caching
- model routing
- usage accounting

### Observability

- structured logs
- metrics
- traces
- request/job IDs
- model/provider dimensions
- token usage
- queue latency

## Principal-level objective

For every component, be able to answer:

1. What happens when it is slow?
2. What happens when it fails?
3. What happens when it receives 10x traffic?
4. What happens when the same request is delivered twice?
5. What is the blast radius?
6. How is it observed?
7. How much does it cost?
8. How is it secured?
