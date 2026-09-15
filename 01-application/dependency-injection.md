# Dependency Injection for AI Systems

Dependency injection means a component receives its dependencies instead of constructing them internally.

## Why it matters

AI systems have many replaceable dependencies:

- LLM provider
- Embedding provider
- Vector store
- Database
- Redis
- Queue
- Object storage
- Telemetry

## Bad

```python
class Summarizer:
    def __init__(self):
        self.client = OpenAIClient()
```

The class is tightly coupled to one implementation.

## Better

```python
class Summarizer:
    def __init__(self, llm):
        self.llm = llm

    async def summarize(self, text):
        return await self.llm.generate(text)
```

Production code can inject:

```python
OpenAIAdapter()
AnthropicAdapter()
LocalModelAdapter()
FakeLLM()
```

## Principal-level rule

Depend on interfaces/contracts at application boundaries.

```text
Use Case
   |
   v
LLMPort
   |
   +--> OpenAIAdapter
   +--> AnthropicAdapter
   +--> LocalModelAdapter
```

## AI scenarios

### Provider failover

Inject a router rather than hardcoding one provider.

### Testing

Inject a deterministic fake model.

### Cost optimization

Inject a model-selection policy.

### Enterprise deployment

Inject a private/local inference adapter.

## Production checklist

- Dependency inversion
- Interfaces/protocols
- Composition root
- Test doubles
- Configuration injection
- Provider abstraction without over-abstraction
