# S3 Usage Patterns

Object storage is ideal for large, durable, unstructured data.

## AI use cases

- uploaded documents
- PDFs
- images
- audio/video
- model artifacts
- evaluation datasets
- generated files
- raw ingestion data

## Recommended flow

```text
Client
 ↓
API requests upload authorization
 ↓
Presigned upload
 ↓
S3
 ↓
Object-created event
 ↓
Processing queue
 ↓
AI worker
```

This avoids sending large files through your application server.

## Key design principles

- private buckets by default
- least-privilege IAM
- encryption
- lifecycle policies
- versioning where useful
- object key conventions
- metadata
- retention rules

## Multi-tenant key example

```text
orgs/{org_id}/documents/{document_id}/source.pdf
```

Do not rely on object naming alone for authorization; enforce access controls in the application and storage policy.

## AI-specific pattern

Store the original artifact in S3 and keep only metadata in the database.

Database:

```text
document_id
org_id
s3_key
content_type
size
status
created_at
```

## Avoid

- storing huge blobs directly in relational tables unless justified
- public buckets for private customer data
- passing large files through synchronous APIs unnecessarily
