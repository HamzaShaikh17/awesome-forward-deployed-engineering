# Docker — Deep Production Knowledge

Docker packages an application and its runtime dependencies into an image that runs as a container.

## Image vs container

Image:

> Immutable package/template.

Container:

> Running instance of an image.

## Production Dockerfile principles

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY pyproject.toml .
RUN pip install --no-cache-dir .

COPY src ./src

RUN useradd --create-home appuser
USER appuser

CMD ["python", "-m", "src"]
```

## Multi-stage builds

Use a builder stage for compilation/dependencies and a smaller runtime image.

Benefits:

- smaller attack surface
- faster deployment
- less storage

## Containers should be

- stateless
- immutable
- disposable
- configured externally
- run as non-root where practical

## Important concepts

You should deeply understand:

- layers
- build cache
- `.dockerignore`
- image tags/digests
- registries
- container networking
- volumes
- resource limits
- health checks
- signals and graceful shutdown
- PID 1 behavior
- filesystem permissions
- image scanning

## AI containers

For GPU workloads understand:

- NVIDIA Container Toolkit
- CUDA compatibility
- model download strategy
- image size
- startup time
- GPU resource requests
- model warm-up

## Production rule

Do not bake secrets into an image.

Use runtime configuration and secret management.
