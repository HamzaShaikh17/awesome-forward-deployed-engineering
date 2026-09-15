# Redis Caching Strategies

Redis is useful for fast shared state and caching.

## Cache-aside

```text
Request
  ↓
Redis?
  ├─ hit → return
  └─ miss → DB/LLM → Redis → return
```

Example:

```python
value = await redis.get(key)

if value is None:
    value = await expensive_operation()
    await redis.set(key, value, ex=3600)
```

## AI caching

Useful candidates:

- deterministic LLM responses
- embeddings
- document metadata
- rate-limit counters
- idempotency records

Be careful caching sensitive prompts or outputs.

## Cache keys

Include relevant dimensions:

```text
llm:v2:{org_id}:{model}:{parameter_hash}:{prompt_hash}
```

Depending on the data, tenant isolation may require `org_id` in the key.

## Cache stampede

When a popular key expires, many requests may recompute simultaneously.

Mitigate with:

- distributed locks
- request coalescing
- stale-while-revalidate
- jittered TTLs

## Failure design

Redis should not become an accidental single point of failure for non-critical reads.

Define fail-open/fail-closed behavior per feature.
