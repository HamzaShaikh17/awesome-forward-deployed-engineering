# Authentication and Authorization

## Authentication

Answers:

> Who are you?

Examples:

- session
- OAuth/OIDC
- access token
- API key

## Authorization

Answers:

> What are you allowed to do?

Examples:

- read this document
- use this model
- administer this organization

## JWT

A JWT commonly contains:

```json
{
  "sub": "user_123",
  "org_id": "org_456",
  "role": "developer",
  "exp": 1770000000
}
```

Never trust claims until the token's signature, issuer, audience, and expiration are validated.

## Access and refresh tokens

Use short-lived access tokens and a secure refresh strategy where appropriate.

## API keys for AI products

Store only a secure representation of the key, not plaintext.

A useful model:

```text
api_keys
  id
  org_id
  key_hash
  created_at
  last_used_at
  revoked_at
```

Support:

- rotation
- revocation
- scopes
- usage attribution

## Multi-tenancy

Never trust a client-provided `org_id` alone.

Derive identity from authenticated credentials and verify resource ownership.

## Principal-level questions

- How are tokens revoked?
- How are compromised credentials contained?
- Can a user access another tenant's data?
- Can one API key exceed organization quota?
- Which actions require elevated privileges?
