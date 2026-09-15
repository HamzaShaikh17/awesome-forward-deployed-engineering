# Domain + SSL/TLS Setup

A production API normally looks like:

```text
https://api.example.com
```

## DNS

A domain maps names to infrastructure.

Common records:

- A / AAAA
- CNAME
- TXT

## TLS

HTTPS uses TLS to provide:

- encryption
- server authentication
- integrity

## Typical deployment

```text
Domain
 ↓
DNS
 ↓
Load Balancer / Nginx
 ↓
TLS certificate
 ↓
Application
```

## Certificate management

Prefer automated certificate issuance and renewal.

Managed cloud load balancers can terminate TLS without requiring the application to handle certificates directly.

## Redirect HTTP

Redirect:

```text
http://example.com
→
https://example.com
```

## Production checklist

- certificate automation
- renewal monitoring
- secure TLS configuration
- DNS validation
- correct forwarded-proto handling
- HSTS where appropriate
- no secrets in URLs
