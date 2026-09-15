# CAP Theorem Basics

CAP describes a trade-off during a network partition in a distributed system.

- C — Consistency
- A — Availability
- P — Partition tolerance

The practical lesson is:

> When a partition occurs, a distributed system must choose whether to favor consistency or availability.

## Consistency

A read reflects the latest successful write according to the system's consistency model.

## Availability

The system continues returning responses despite some failures.

## Partition tolerance

The system continues operating despite communication failure between nodes.

In real distributed systems, network partitions must be expected, so the key design choice is often CP vs AP behavior.

## AI examples

Strong consistency is especially important for:

- billing
- quota enforcement
- critical authorization state

Eventual consistency can often work for:

- analytics
- dashboards
- non-critical notifications
- derived metrics

## Important nuance

CAP is not simply:

> Every database permanently chooses exactly two letters.

The trade-off becomes relevant when a partition prevents nodes from communicating.

Real systems also expose more detailed consistency models and failure behaviors.
