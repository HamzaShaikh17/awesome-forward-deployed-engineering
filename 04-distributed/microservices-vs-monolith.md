# Microservices vs Monolith

## Monolith

One deployable application.

Advantages:

- simple deployment
- easy debugging
- low network overhead
- fast refactoring
- lower operational complexity

Disadvantages:

- coarse-grained scaling
- larger blast radius
- potential internal coupling

## Microservices

Independent deployable services.

Advantages:

- independent scaling
- fault isolation
- independent deployment
- domain/team boundaries
- technology flexibility

Disadvantages:

- distributed tracing
- network failures
- service discovery
- API contracts
- distributed transactions
- operational complexity

## AI recommendation

A strong default for a young AI product is often:

```text
Modular monolith
+
separate asynchronous AI worker pool
```

Extract services when there is a concrete reason:

- independent scaling
- independent SLA
- security isolation
- team ownership
- deployment bottleneck

Do not create microservices merely because the architecture diagram looks impressive.

## Principal decision framework

Ask:

1. Is the boundary stable?
2. Does it scale differently?
3. Does it need a different reliability boundary?
4. Is separate ownership useful?
5. Is the operational cost justified?
