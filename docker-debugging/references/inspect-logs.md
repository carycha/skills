# Docker Debugging: Inspection & Logging

## Advanced Logging
Use these flags to filter and focus on relevant log output.

```bash
# Follow logs with timestamps
docker logs -f -t <container>

# Filter by time range
docker logs --since 1h --until 15m <container>

# Get the last 100 lines
docker logs --tail 100 <container>
```

## Deep Inspection
Extract specific state information using Go templates.

```bash
# Get container status
docker inspect --format='{{.State.Status}}' <container>

# Get healthcheck status
docker inspect --format='{{.State.Health.Status}}' <container>

# Get network settings as JSON
docker inspect --format='{{json .NetworkSettings}}' <container>
```

## Event Monitoring
Monitor real-time events from the Docker daemon to catch crashes or restarts.

```bash
# Filter events for a specific container
docker events --filter 'container=<name>' --since 1h
```
