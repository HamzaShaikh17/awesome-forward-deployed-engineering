# Async Programming

Async programming allows a program to make progress on other work while waiting for I/O.

## Best use cases

- HTTP calls
- Database I/O
- Redis
- Object storage
- LLM APIs
- Message brokers

## Python example

```python
import asyncio
import httpx

async def call_model(client, prompt):
    response = await client.post("/generate", json={"prompt": prompt})
    response.raise_for_status()
    return response.json()

async def main(prompts):
    async with httpx.AsyncClient() as client:
        return await asyncio.gather(
            *(call_model(client, prompt) for prompt in prompts)
        )
```

## Async does not mean parallel CPU execution

Async primarily improves utilization while tasks are waiting on I/O.

CPU-heavy work may require:

- multiprocessing
- worker processes
- job queues
- GPU workers

## AI considerations

Never create unlimited concurrent LLM calls.

Use:

- bounded concurrency
- timeouts
- cancellation
- retries with backoff
- provider rate limits
- token budgets

Example:

```python
semaphore = asyncio.Semaphore(20)

async def bounded_call(fn):
    async with semaphore:
        return await fn()
```

## Production checklist

- Explicit timeouts
- Bounded concurrency
- Cancellation handling
- Retry policy
- Connection pooling
- Backpressure
- Metrics for latency and concurrency
