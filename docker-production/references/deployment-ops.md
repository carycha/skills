# Docker Production: Deployment & Operations

## Deployment Strategies

### Rolling Update (Zero Downtime)
Update one replica at a time and automatically rollback on failure.
```yaml
deploy:
  update_config:
    parallelism: 1
    delay: 10s
    failure_action: rollback
    order: start-first # Start new container before stopping old one
  rollback_config:
    parallelism: 1
    delay: 10s
```

### Blue-Green (Traffic Switching)
1. Deploy new version (Green stack).
2. Switch Nginx/Load-balancer target to Green.
3. Remove old version (Blue stack).

## Production Operations

### Diagnostic Quick Reference
```bash
# Live resource usage
docker stats --format "table {{.Name}}	{{.CPUPerc}}	{{.MemUsage}}"

# Check restart history
docker inspect --format='{{.RestartCount}}' <container_id>

# Monitor recent lifecycle events
docker events --filter 'container=<name>' --since 1h
```

### Common Issues in Production

| Error | Cause | Solution |
|-------|-------|----------|
| `Unhealthy` | App endpoint failing or startup slow. | Check logs; increase `start_period`. |
| `OOMKilled` | Process exceeded hard memory limit. | Increase limit or fix memory leak. |
| `Restart Loop`| Immediate crash upon start. | Use `docker logs --tail 50` to debug. |
