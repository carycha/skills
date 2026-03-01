# Docker Debugging: Runtime Diagnosis

## Interactive Debugging (Exec)
Execute commands within a running container to verify environment state.

```bash
# Get a shell (sh or bash)
docker exec -it <container> /bin/sh

# Run as root user for debugging
docker exec -u 0 -it <container> /bin/sh

# Check active processes
docker exec <container> ps aux
```

## Resource Monitoring (Stats)
Track CPU, memory, and network usage in real-time.

```bash
# Live stats formatted as a table
docker stats --format "table {{.Name}}	{{.CPUPerc}}	{{.MemUsage}}	{{.NetIO}}"
```

## Exit Code Reference
Exit codes provide clues for why a container stopped prematurely.

| Code | Meaning | Action |
|------|---------|--------|
| **0** | Success | Normal exit; no action needed. |
| **1** | General error | Check logs; application failure. |
| **137** | OOMKilled | Container hit memory limit; increase memory. |
| **139** | Segfault | Segmentation fault; check application code. |
| **143** | SIGTERM | Normal termination via signal. |

### How to Check Exit Code
```bash
docker inspect --format='{{.State.ExitCode}}' <container>
```
