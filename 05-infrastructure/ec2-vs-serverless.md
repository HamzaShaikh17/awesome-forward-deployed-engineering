# EC2 vs Serverless

## EC2 / VM model

You manage a virtual machine and choose:

- OS
- runtime
- CPU/memory
- networking
- scaling
- deployment

Good for:

- long-running services
- custom runtimes
- GPU workloads
- predictable sustained traffic
- fine-grained control

## Serverless

You deploy functions or managed execution units while the provider manages servers.

Good for:

- event-driven tasks
- bursty workloads
- short-lived operations
- low operational overhead

## AI constraints

Serverless may be a poor fit for:

- GPU inference
- large model loading
- long-running model processes
- specialized runtimes

Serverless can work well for:

- API glue
- lightweight preprocessing
- event handlers
- queue consumers
- orchestration steps
- calls to external LLM APIs

## Hybrid

```text
API Gateway / ALB
       ↓
Serverless API
       ↓
SQS
       ↓
Container/GPU Workers
       ↓
LLM / model
```

Choose based on workload characteristics rather than ideology.
