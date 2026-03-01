# Docker Compose: Operations & Troubleshooting

## Operations Quick Reference

### Management Commands
```bash
# Start/Restart
docker compose up -d --build

# Scale service
docker compose up -d --scale backend=3

# Stopping & Cleaning
docker compose down -v  # Stop and remove named volumes (destructive!)

# Config Validation
docker compose config   # Merges all files and prints active config
```

## Troubleshooting & Debugging

### Health Check Debugging
View status and failure logs for healthchecks.
```bash
# Status check
docker inspect --format='{{json .State.Health}}' <container_id>

# Log view
docker inspect --format='{{range .State.Health.Log}}{{.Output}}{{end}}' <container_id>
```

### Common Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `undefined service` | Missing dependency | Define service or use `--no-deps`. |
| `yaml syntax error` | Indentation | Validate with `docker compose config`. |
| `port in use` | Conflict | Check `lsof -i :PORT` or change YAML. |
| `health failing` | Not ready | Increase `start_period` or check service logs. |

### Debug Checklist
- [ ] Valid YAML? Run `docker compose config`.
- [ ] Images updated? Run `docker compose pull`.
- [ ] Dependencies healthy? Check `docker compose ps`.
- [ ] Variables set? Check `.env` presence and values.
