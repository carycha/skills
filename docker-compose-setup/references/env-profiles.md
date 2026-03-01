# Docker Compose: Environment Management & Profiles

## Environment Configuration

### Base + Override Pattern
Compose auto-loads `docker-compose.override.yaml` for local overrides. Use multiple `-f` flags for other environments.
```yaml
# docker-compose.prod.yaml
services:
  app:
    deploy: { replicas: 3 }
    restart: always
```

### Environment Variables
Use `.env` files for secrets and dynamic values.
```bash
# .env file
DB_PASSWORD=secret123
APP_VERSION=1.2.3
```
```yaml
environment:
  - DB_PASSWORD=${DB_PASSWORD}
  - VERSION=${APP_VERSION:-latest}  # Default value interpolation
```

## Service Profiles
Group services for specific use cases (debugging, testing).
```yaml
services:
  app: { image: myapp }
  
  debugger:
    image: debug-tools
    profiles: [debug]

  test-db:
    image: postgres:alpine
    profiles: [testing]
```

### Usage:
```bash
docker compose up                     # Starts "app" only
docker compose --profile debug up     # Starts "app" + "debugger"
```
