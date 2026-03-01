# Docker Optimization: Runtime & Analysis

## Resource Constraints (Limits & Reservations)
Prevent "noisy neighbor" issues and OOM kills by defining limits and reservations in Docker Compose.

```yaml
services:
  app:
    deploy:
      resources:
        limits:
          cpus: '1.0'
          memory: 512M
        reservations:
          cpus: '0.25'
          memory: 256M
```

## CLI Performance Tuning
Control resource consumption directly from the `docker run` command.

```bash
# Hard memory limit with swap disabled
docker run --memory=512m --memory-swap=512m myapp

# Pin specific CPU shares
docker run --cpus=1.5 myapp

# Limit disk I/O
docker run --device-read-bps=/dev/sda:1mb myapp
```

## Analysis & Diagnostic Tools

### dive
Visually inspect image layers and detect wasted space (duplicate files).
```bash
dive <image_name>
```

### Docker History
Understand exactly how much space each Dockerfile instruction occupies.
```bash
docker history <image_name> --format "table {{.Size}}	{{.CreatedBy}}"
```

### Build Progress (BuildKit)
View detailed, non-interactive build progress to identify slow layers.
```bash
DOCKER_BUILDKIT=1 docker build --progress=plain .
```

## Runtime Optimization Checklist
- [ ] Is `DOCKER_BUILDKIT=1` enabled?
- [ ] Are memory and CPU limits defined for every production service?
- [ ] Have you tested the container for OOM errors under load?
- [ ] Is the filesystem read-only where possible?
