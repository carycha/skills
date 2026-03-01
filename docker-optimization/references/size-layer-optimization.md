# Docker Optimization: Size & Layering

## Base Image Selection
Choosing the right starting point is the most impactful decision for image size.

| Base | Size | Best For |
|------|------|----------|
| **scratch** | 0 MB | Static binaries (Go/Rust). |
| **distroless** | 2-20 MB | Production-ready (minimal CVEs). |
| **alpine** | 5 MB | Most general-purpose small images. |
| **slim** | 80-150 MB | Python/Node when apt is required. |

## Layer Optimization (Flattening)
Docker creates a new layer for every `RUN`, `COPY`, and `ADD`. Combine operations to keep the image small.

### ✅ Good: Single Layer
```dockerfile
RUN apt-get update && 
    apt-get install -y --no-install-recommends curl && 
    rm -rf /var/lib/apt/lists/*
```

### ❌ Bad: Multiple Layers (Large footprint)
```dockerfile
RUN apt-get update
RUN apt-get install -y curl
RUN rm -rf /var/lib/apt/lists/*
```

## Cleaning Package Manager Caches
Always clear temporary cache files within the same `RUN` layer they were created.

- **Node.js**: `npm cache clean --force`
- **Python**: `pip cache purge`
- **Alpine**: `apk add --no-cache`
- **Debian/Ubuntu**: `apt-get clean && rm -rf /var/lib/apt/lists/*`

## .dockerignore Strategy
Prevent sending large, unnecessary local files to the Docker daemon.
```text
node_modules
.git
dist
.env
*.log
tests/
```
