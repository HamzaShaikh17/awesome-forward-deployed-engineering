# Input Validation

Input validation is the first boundary protecting application correctness, security, and AI cost.

## Two layers

### Syntactic validation

- type
- required fields
- format
- length
- enum
- payload size

### Semantic validation

- tenant ownership
- quota
- allowed model
- workflow state
- resource existence

Keep business rules out of generic schema validation.

## Pydantic example

```python
from pydantic import BaseModel, Field

class SummarizeRequest(BaseModel):
    text: str = Field(min_length=1, max_length=20_000)
    model: str
```

## AI-specific controls

Validate:

- maximum input size
- estimated token count
- maximum output tokens
- allowed model
- file size/type
- number of uploaded documents
- tool/function arguments

## Security

Do not assume validation prevents prompt injection. Treat untrusted model input and tool arguments separately from application instructions.

## Production checklist

- Reject oversized payloads early
- Validate file MIME/type and content
- Validate IDs
- Validate enums
- Enforce tenant ownership
- Enforce quotas
- Bound LLM token usage
