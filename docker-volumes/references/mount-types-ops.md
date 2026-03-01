# Docker: Storage Mount Types & Operations

## Comparison of Storage Types

| Type | Persistence | Use Case | Managed By |
|------|-------------|----------|------------|
| **Named Volume** | Yes | Databases, User Uploads. | Docker Engine |
| **Bind Mount** | Yes | Source code (hot reload), Configs. | Host OS |
| **tmpfs** | No (RAM) | Secrets, Temporary session data. | Docker (in-memory) |

## Named Volumes (Production Recommended)
Best for data that should persist across container recreations and be managed by Docker.

```bash
# Lifecycle
docker volume create my_data
docker volume ls
docker volume inspect my_data
docker volume prune # Remove all unused volumes

# Usage
docker run -d -v my_data:/var/lib/mysql mysql:8
```

## Bind Mounts (Development Recommended)
Map a specific path on your host to the container.

```bash
# Development: Map current source code
docker run -d -v $(pwd)/src:/app/src node:alpine

# Read-only configuration file
docker run -d -v /etc/myconfig.yaml:/app/config.yaml:ro myapp
```

## tmpfs (Memory-only)
Fast and secure storage that is never written to disk.

```bash
# CLI syntax
docker run -d --tmpfs /app/tmp:rw,noexec,nosuid,size=64m myapp
```
