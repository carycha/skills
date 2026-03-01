# Docker Debugging: Network & Health Checks

## Network Troubleshooting
Verify service discovery and connectivity between containers.

```bash
# Test DNS resolution for a service
docker exec <container> nslookup <service_name>

# Verify network connectivity
docker exec <container> ping -c 3 <target_service>

# Test specific API endpoint
docker exec <container> curl -f http://<service_name>:port/health
```

## Healthcheck Debugging
Investigate why a container is marked as "unhealthy".

```bash
# Check current health status
docker inspect --format='{{json .State.Health.Status}}' <container>

# View health check execution logs
docker inspect --format='{{range .State.Health.Log}}{{.Output}}{{end}}' <container>

# Test health command manually inside container
docker exec <container> /path/to/healthcheck/command
```

## General Network Check
Confirm the container is part of the expected networks.

```bash
docker network inspect <network_name>
# Or check the container's network membership directly
docker inspect --format='{{json .NetworkSettings.Networks}}' <container>
```
