# Database Indexing

Indexes speed up data access by allowing the database to avoid scanning every row.

## Common index

```sql
CREATE INDEX idx_documents_org_id
ON documents(org_id);
```

## Composite index

For:

```sql
SELECT *
FROM usage
WHERE org_id = $1
  AND created_at >= $2
ORDER BY created_at DESC;
```

A useful candidate is:

```sql
CREATE INDEX idx_usage_org_created
ON usage(org_id, created_at DESC);
```

Column order matters.

## AI SaaS patterns

Common query dimensions:

- `org_id`
- `user_id`
- `status`
- `created_at`
- `job_id`
- API key hash
- document ID

## Verify with query plans

Use:

```sql
EXPLAIN ANALYZE ...
```

Do not assume an index is helping.

## Trade-off

Indexes improve reads but add:

- storage
- write overhead
- maintenance cost

Avoid over-indexing.

## Large tables

Consider:

- partitioning
- archival
- retention policies
- time-based partitions
- careful indexing strategy
