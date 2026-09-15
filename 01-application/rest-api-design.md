# REST API Design with Proper HTTP Semantics

## Core principle

An API should model resources and use HTTP semantics correctly rather than turning every operation into an RPC endpoint.

Example:

```http
POST /documents
GET /documents/{document_id}
PATCH /documents/{document_id}
DELETE /documents/{document_id}
```

## HTTP methods

### GET
Retrieve a representation.

- Safe
- Idempotent
- Should not mutate server state

### POST
Create a resource or trigger an operation that is not naturally idempotent.

- Not inherently idempotent
- Usually returns `201 Created` for resource creation

### PUT
Replace a resource representation.

- Idempotent

### PATCH
Partially modify a resource.

- Semantics depend on the patch design
- Design for idempotency when practical

### DELETE
Remove a resource.

- Idempotent from the client's perspective

## Important status codes

- `200 OK` — successful request with a response
- `201 Created` — resource created
- `202 Accepted` — accepted for asynchronous processing
- `204 No Content` — success with no response body
- `400 Bad Request` — malformed/invalid request
- `401 Unauthorized` — authentication required or invalid
- `403 Forbidden` — authenticated but not permitted
- `404 Not Found` — resource not found
- `409 Conflict` — state conflict
- `422 Unprocessable Content` — syntactically valid but semantically invalid input
- `429 Too Many Requests` — rate limit exceeded
- `500 Internal Server Error` — unexpected server failure
- `503 Service Unavailable` — temporarily unable to serve

## AI example

A long-running document analysis should not block the HTTP request.

```http
POST /documents/doc_123/analyses
```

Response:

```http
HTTP/1.1 202 Accepted
Location: /analyses/job_456
```

The client can then query the job or receive a webhook.

## Production checklist

- Correct method semantics
- Correct status codes
- Consistent error schema
- Pagination
- Filtering/sorting conventions
- Idempotency for retryable writes
- Request IDs
- Authentication and authorization
- Rate limiting
- API versioning
