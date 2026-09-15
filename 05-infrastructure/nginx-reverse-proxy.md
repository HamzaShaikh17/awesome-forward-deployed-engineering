# Nginx Reverse Proxy

A reverse proxy receives client traffic and forwards it to backend services.

```text
Internet
   ↓
Nginx
   ↓
Application
```

## Responsibilities

- TLS termination
- routing
- buffering
- connection management
- static assets
- access logs
- request size limits
- basic traffic controls

## Example

```nginx
server {
    listen 443 ssl;
    server_name api.example.com;

    location / {
        proxy_pass http://app:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

## AI-specific concerns

Tune:

- request body limits for uploads
- upstream timeouts
- streaming behavior
- buffering
- WebSocket support where needed
- connection limits

Do not set huge timeouts blindly; long-running AI jobs should often be asynchronous instead.

## Common architecture

```text
Cloud LB
  ↓
Nginx
  ↓
API containers
  ↓
Queue
  ↓
AI workers
```
