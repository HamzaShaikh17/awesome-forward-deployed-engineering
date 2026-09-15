# Environment Variables and Configuration

Configuration should be external to application code.

## Categories

### Non-secret configuration

Examples:

```text
APP_ENV=production
LOG_LEVEL=INFO
MAX_CONCURRENCY=20
LLM_TIMEOUT_SECONDS=30
```

### Secrets

Examples:

```text
DATABASE_PASSWORD
API_PROVIDER_KEY
WEBHOOK_SECRET
```

Secrets require stronger handling than ordinary configuration.

## Twelve-factor principle

The application should receive environment-specific configuration at runtime rather than embedding it in source code.

## Never

- commit `.env` files containing secrets
- hardcode provider keys
- print secrets in logs
- bake secrets into Docker images

## Better

```text
Secret manager
      ↓
Deployment platform
      ↓
Container environment
      ↓
Application
```

## Configuration validation

Fail fast for required production settings.

Example:

```python
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    database_url: str
    llm_api_key: str
    max_concurrency: int = 20
```

Validate at startup rather than discovering a missing variable during a request.
