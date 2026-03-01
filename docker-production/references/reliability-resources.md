# Docker Production: Reliability & Resources

## Health Checks
Define health checks in both Dockerfile (for general readiness) and Compose (for service-aware readiness).

### Dockerfile Pattern
```dockerfile
HEALTHCHECK --interval=30s --timeout=3s --retries=3 --start-period=60s 
  CMD curl -f http://localhost:3000/health || exit 1
```

### Compose Pattern
Wait for backend to be healthy before starting dependent services.
```yaml
services:
  app:
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 60s
```

## Resource Management
Prevent a single container from starving the host or other services.

```yaml
services:
  app:
    deploy:
      resources:
        limits:
          cpus: '1.0'
          memory: 1G
        reservations:
          cpus: '0.5'
          memory: 512M
      restart_policy:
        condition: on-failure
        delay: 5s
        max_attempts: 3
```

## Restart Policies
- `always`: Restart regardless of exit status.
- `unless-stopped`: Restart unless the user manually stopped it.
- `on-failure`: Restart only if the container exits with an error.
