# Docker Compose: Modern Syntax & Stacks

## 2024-2025 Syntax Guidelines
The `version` field is deprecated. Start your Compose files directly with top-level keys like `services`, `networks`, and `volumes`.

### Standard Multi-Container Stack
```yaml
services:
  frontend:
    build: { context: ./frontend, target: production }
    ports: ["80:80"]
    depends_on:
      backend: { condition: service_healthy }
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost/health"]
      interval: 30s
      timeout: 10s
      retries: 3
    restart: unless-stopped

  backend:
    build: ./backend
    expose: ["3000"]
    environment:
      DATABASE_URL: postgres://user:${DB_PASSWORD}@database:5432/app
    depends_on:
      database: { condition: service_healthy }
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 10s
      timeout: 5s
      retries: 5

  database:
    image: postgres:16-alpine
    volumes: [db_data:/var/lib/postgresql/data]
    environment:
      POSTGRES_PASSWORD: ${DB_PASSWORD}
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 5s
      timeout: 5s
      retries: 5

volumes:
  db_data:
```

## Service Dependencies
Use `depends_on` with `condition: service_healthy` to ensure proper startup order. This is superior to `service_started`, as it waits for the service to be actually ready for traffic.
