# Docker Security: Dockerfile Hardening

## Non-Root User (Mandatory)
Never run your application as `root`. Create a dedicated user with a specific UID/GID.

```dockerfile
# 1. Create non-root user
RUN addgroup -g 1001 app && 
    adduser -u 1001 -G app -D app

# 2. Set ownership during copy
COPY --chown=app:app . /app

# 3. Switch user before CMD
USER app
```

## BuildKit Secret Mounts
Protect sensitive build-time credentials (like `.npmrc` or AWS keys) without persisting them in image layers.

```dockerfile
# syntax=docker/dockerfile:1
# The secret is mounted temporarily at runtime and never stored in the final image
RUN --mount=type=secret,id=npmrc,target=/root/.npmrc 
    npm install
```
**Build command:** `docker build --secret id=npmrc,src=.npmrc .`

## Minimal Surface Area (Distroless)
Distroless images contain only your app and its runtime dependencies. They lack shells and package managers, making them significantly harder to exploit.

```dockerfile
FROM gcr.io/distroless/nodejs20-debian12
COPY --from=builder /app/dist ./dist
USER nonroot
CMD ["dist/index.js"]
```
