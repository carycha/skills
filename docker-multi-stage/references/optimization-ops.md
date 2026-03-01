# Multi-Stage: Optimization & Operations

## Size Comparison Table
Multi-stage builds can reduce image sizes by 50-99%.

| Language | Standard Base | Multi-Stage Size | Typical Reduction |
|----------|---------------|------------------|-------------------|
| Node.js | ~1.2 GB | ~150 MB | 87% |
| Python | ~900 MB | ~120 MB | 87% |
| Go | ~800 MB | ~10 MB | 99% |
| Rust | ~1.5 GB | ~5 MB | 99.7% |
| Java | ~600 MB | ~200 MB | 67% |

## Debugging & Inspection Tools

### dive
Use `dive` to inspect each layer of your multi-stage build and see exactly what's taking up space.
```bash
dive <image_name>
```

### Docker Commands
```bash
# Check final image size
docker images <image_name>

# Inspect history (layer by layer)
docker history <image_name>
```

## Common Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| `COPY --from failed` | Named stage not found. | Verify `AS builder` name matches exactly. |
| `Binary not found` | Dynamic linking issue. | Use `ldd` to check dependencies; ensure `libc` exists or use static linking. |
| `Permission denied` | Non-root user permissions. | Use `COPY --chown=user:group` during transfer. |

## Fallback Strategy
If `scratch` or `distroless` fails due to missing dependencies, start with an `alpine` or `slim` base and add libraries incrementally until the application works.
