# CI/CD Basics

CI/CD automates software validation and delivery.

## CI

Typical pipeline:

```text
Commit
 ↓
Lint
 ↓
Unit tests
 ↓
Integration tests
 ↓
Security checks
 ↓
Build image
```

## CD

```text
Build
 ↓
Push image
 ↓
Deploy staging
 ↓
Smoke tests
 ↓
Production
```

## AI-specific checks

Include:

- API tests
- prompt/evaluation regression tests
- dependency vulnerability scanning
- container scanning
- infrastructure validation
- model configuration validation

## Deployment strategies

### Rolling

Gradually replace old instances.

### Blue/green

Maintain two environments and switch traffic.

### Canary

Send a small percentage of traffic to the new version.

Canary is especially useful for AI because model/provider changes can alter:

- quality
- latency
- cost
- failure rate

## Production principles

- immutable artifacts
- reproducible builds
- environment promotion
- rollback
- migrations are deliberate
- secrets injected at deploy/runtime
- observability gates deployment
