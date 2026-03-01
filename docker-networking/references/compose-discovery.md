# Docker: Service Discovery & Compose Networking

## Service Discovery (DNS)
Docker includes an internal DNS server that allows containers on the same network to resolve each other by **service name** (in Compose) or **container name**.

```yaml
services:
  app:
    environment:
      DATABASE_HOST: database # Resolves to the db container
  database:
    image: postgres:16-alpine
```

## Network Isolation in Compose
Segment your application into public and private networks for enhanced security.

```yaml
services:
  frontend:
    image: nginx:alpine
    networks: [public]

  backend:
    image: node:20-alpine
    networks: [public, private]
    expose: ["3000"] # Not mapped to host

  database:
    image: postgres:16-alpine
    networks: [private] # Fully isolated from frontend

networks:
  public: { driver: bridge }
  private: { driver: bridge, internal: true } # No internet access
```

## Overlay Network (Multi-Host)
Used for Docker Swarm to encrypt and route traffic between multiple physical nodes.

```bash
docker network create --driver overlay --attachable --opt encrypted my_overlay
```
