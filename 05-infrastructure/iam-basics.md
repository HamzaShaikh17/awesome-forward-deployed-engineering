# IAM Basics

IAM controls who or what can access which cloud resources and perform which actions.

## Core model

```text
Principal
  + Action
  + Resource
  + Conditions
  → Allow/Deny
```

## AWS-style concepts

- users
- roles
- policies
- groups
- resource policies

## Prefer roles for workloads

An EC2/Lambda/container workload should generally receive temporary credentials through a role rather than hardcoded access keys.

## Least privilege

Bad:

```text
s3:*
```

Better:

```text
s3:GetObject
```

restricted to the required bucket/path.

## AI example

A document worker may need:

```text
S3: read document objects
SQS: receive/delete jobs
Database: update job state
Secrets: read provider configuration
```

It should not automatically have administrator permissions.

## Principal-level topics

- policy evaluation
- explicit deny
- role assumption
- temporary credentials
- cross-account access
- identity vs resource policies
- conditions
- audit logging
