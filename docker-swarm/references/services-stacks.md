# Docker Swarm: Services & Stacks

## Service Deployment (CLI)
Deploy and scale individual services directly from the command line.

```bash
# Create service with 3 replicas
docker service create --name webapp --replicas 3 --publish 80:80 nginx:alpine

# Scale service up or down
docker service scale webapp=5

# Perform rolling update
docker service update --image nginx:1.25-alpine webapp

# Rollback to previous version
docker service rollback webapp
```

## Stack Deployment (YAML)
Use a Compose-like file to deploy multi-service applications.

```yaml
# stack.yaml
services:
  api:
    image: myapi:latest
    deploy:
      replicas: 3
      placement:
        constraints: [node.role == worker]
      update_config:
        parallelism: 1
        delay: 10s
        failure_action: rollback
      resources:
        limits: { cpus: '0.5', memory: 512M }
    networks: [backend]

networks:
  backend: { driver: overlay }
```

### Stack Commands
- **Deploy/Update**: `docker stack deploy -c stack.yaml myapp`
- **List Services**: `docker stack services myapp`
- **Remove Stack**: `docker stack rm myapp`
