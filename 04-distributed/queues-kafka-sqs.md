# Queues — Kafka and SQS

A queue decouples producers from workers.

```text
API → Queue → Worker
```

## SQS

Good when you want:

- managed infrastructure
- simple work queues
- AWS integration
- visibility timeout
- DLQ support

Worker flow:

```text
Receive
→ process
→ delete
```

If processing fails before deletion, the message can become visible again.

## Kafka

Kafka is a distributed log with:

- topics
- partitions
- offsets
- consumer groups

It is useful when you need:

- high throughput
- replay
- multiple independent consumers
- event streaming

## Key distinction

SQS is primarily a managed queue.

Kafka is a durable distributed event log/streaming platform.

## AI worker design

Message:

```json
{
  "job_id": "job_123",
  "org_id": "org_42",
  "document_id": "doc_77"
}
```

Worker must be idempotent because duplicate delivery can happen.

## Production concerns

- visibility timeout
- retry backoff
- DLQ
- idempotency
- queue age
- consumer lag
- concurrency limits
- poison messages
- graceful shutdown
