# Load Balancing

Load balancing distributes traffic across healthy instances.

```text
Client
  ↓
Load Balancer
  ↓
API 1
API 2
API 3
```

## L4

Operates at transport level.

Useful for:

- TCP
- UDP
- high-throughput forwarding

## L7

Understands HTTP/application concepts.

Can route based on:

- host
- path
- headers
- cookies

## Algorithms

- round robin
- weighted round robin
- least connections
- hash/affinity

## AI nuance

AI requests have highly variable duration. Round robin can produce poor utilization when one request takes much longer than another.

For long-running AI jobs, a queue and worker pool is often better than direct request load balancing.

## Health checks

Load balancers should remove unhealthy instances.

Expose suitable health/readiness endpoints.

## Production checklist

- health checks
- timeouts
- connection draining
- TLS termination
- observability
- autoscaling integration
- retry policy without retry storms
