# AI Deployment Production Checklist

## API

- [ ] Correct HTTP semantics
- [ ] Authentication
- [ ] Authorization
- [ ] Input validation
- [ ] Request IDs
- [ ] Rate limiting
- [ ] Timeouts
- [ ] Consistent error responses

## AI calls

- [ ] Provider timeout
- [ ] Token limits
- [ ] Concurrency limits
- [ ] Retry policy
- [ ] Idempotency
- [ ] Cost tracking
- [ ] Model/provider observability
- [ ] Fallback strategy where appropriate

## Storage

- [ ] Database indexes
- [ ] Connection pooling
- [ ] S3/object storage for large artifacts
- [ ] Lifecycle/retention policy
- [ ] Tenant isolation

## Async

- [ ] Queue
- [ ] DLQ
- [ ] Retry/backoff
- [ ] Worker idempotency
- [ ] Queue depth monitoring
- [ ] Graceful worker shutdown

## Infrastructure

- [ ] Containerized application
- [ ] Non-root container
- [ ] Image scanning
- [ ] CI/CD
- [ ] Health/readiness checks
- [ ] Autoscaling
- [ ] TLS
- [ ] DNS

## Security

- [ ] IAM least privilege
- [ ] No secrets in source
- [ ] No secrets in images
- [ ] Secret manager
- [ ] Audit logs
- [ ] Tenant isolation
- [ ] Signed webhooks

## Observability

- [ ] Structured logs
- [ ] Metrics
- [ ] Distributed traces
- [ ] LLM latency
- [ ] Token usage
- [ ] Cost
- [ ] Cache hit rate
- [ ] Queue age
- [ ] Error rate

## Disaster readiness

- [ ] Backups
- [ ] Restore test
- [ ] Rollback strategy
- [ ] Provider outage strategy
- [ ] Redis failure behavior
- [ ] Queue failure behavior
- [ ] Database failure behavior
