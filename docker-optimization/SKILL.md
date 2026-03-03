---
name: docker-optimization
description: Docker Performance Optimizer. Use when the user asks to reduce image size, accelerate build times using BuildKit cache mounts, implement resource limits, or analyze layer efficiency. 「Docker 效能與建置優化」
---

# Docker Optimization

Comprehensive techniques for building faster, smaller, and more performant Docker containers.

## Core Principles

- **Minimal Base Images**: Always start with the smallest viable base image (`scratch`, `distroless`, `alpine`).
- **Layer Efficiency**: Combine `RUN` commands and order them by change frequency to maximize cache hits.
- **BuildKit Power**: Leverage persistent cache mounts (`--mount=type=cache`) to avoid re-downloading dependencies.
- **Explicit Resource Limits**: Prevent container crashes (OOM) and resource contention by defining memory and CPU limits.

## Detailed Guidance

- **Size & Layering**: Base image selection table, layer flattening, package manager cache cleaning, and `.dockerignore` strategies. See [size-layer-optimization.md](references/size-layer-optimization.md).
- **Build Speed & Caching**: Advanced BuildKit cache mounts, parallel build stages, and dependency-first layering. See [build-speed-cache.md](references/build-speed-cache.md).
- **Runtime & Analysis**: Resource constraints (Limits/Reservations), performance tuning, and analysis tools (`dive`, `docker history`). See [runtime-perf-analysis.md](references/runtime-perf-analysis.md).

## Related Resources

- Skill: `docker-multi-stage` - For language-specific multi-stage build templates.
- Skill: `dockerfile-basics` - For fundamental Dockerfile instructions and best practices.
- Skill: `docker-production` - For higher-level orchestration and reliability optimizations.
