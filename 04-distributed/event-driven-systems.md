# Event-Driven Systems

An event is a fact that something happened.

Examples:

- `document.uploaded`
- `embedding.completed`
- `analysis.completed`
- `job.failed`

## Basic architecture

```text
Producer
   ↓
Broker
   ↓
Consumer
```

## AI workflow

```text
DocumentUploaded
      ↓
Embedding Worker
      ↓
EmbeddingCompleted
      ↓
Analysis Worker
      ↓
AnalysisCompleted
      ↓
Webhook Worker
```

## Events should contain

- event ID
- event type
- version
- timestamp
- entity ID
- tenant context where appropriate
- payload

## Idempotency

Consumers must tolerate duplicate delivery.

Use a durable processed-event record or idempotent state transition.

## Delivery

Most practical systems should be designed around at-least-once delivery.

## Failure handling

Use:

- retries
- exponential backoff
- dead-letter queues
- poison-message handling

## Observability

Track:

- publish rate
- consumer lag
- processing latency
- retries
- DLQ volume
- trace/correlation IDs
