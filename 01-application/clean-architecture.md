# Production Clean Architecture for AI

Clean Architecture separates business decisions from infrastructure details.

## Recommended structure

```text
src/
  domain/
    entities/
    value_objects/
    errors/

  application/
    use_cases/
    ports/
    commands/

  infrastructure/
    llm/
    database/
    redis/
    queues/
    storage/

  interfaces/
    http/
    workers/
    webhooks/

  config/
```

## Dependency direction

```text
Interfaces
    ↓
Application
    ↓
Domain

Infrastructure → implements application ports
```

The core should not depend on FastAPI, Redis, PostgreSQL, or a specific LLM vendor.

## AI example

The use case should express:

```python
result = await llm.generate(request)
```

It should not know how the provider HTTP request is constructed.

## Keep domain logic pure

Good domain responsibilities:

- quota rules
- job state transitions
- model eligibility
- tenant invariants

Infrastructure responsibilities:

- HTTP clients
- SQL
- Redis
- Kafka
- S3
- provider SDKs

## Production goal

Make expensive infrastructure replaceable and business rules testable without a network.
