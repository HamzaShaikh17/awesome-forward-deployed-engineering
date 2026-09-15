# Horizontal Scaling

Horizontal scaling means adding instances rather than making one machine larger.

```text
Load Balancer
   ↓
API × N
   ↓
Queue
   ↓
Workers × N
```

## Stateless API requirement

Avoid relying on:

- local sessions
- local durable files
- local-only caches
- in-memory job state

Use shared systems:

- database
- Redis
- object storage
- queue

## Scaling signals

API:

- request rate
- latency
- CPU/memory

Workers:

- queue depth
- queue age
- processing latency
- concurrency
- GPU utilization

## AI-specific constraint

Scaling application instances can increase LLM provider traffic and spend.

Autoscaling must therefore be connected to:

- provider limits
- token budgets
- concurrency limits
- cost controls

## Principal question

What bottleneck appears after the first bottleneck is removed?

Possible answers:

```text
API → DB → Redis → queue → provider quota → GPU
```
