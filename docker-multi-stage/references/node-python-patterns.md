# Multi-Stage: Node.js & Python Patterns

## Node.js (Alpine + Distroless)
Separate build tools from runtime. Distroless images contain only your application and its runtime dependencies, significantly reducing the attack surface.

```dockerfile
# Stage: builder
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build && npm prune --production

# Stage: runtime
FROM gcr.io/distroless/nodejs20-debian12 AS runtime
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
USER nonroot
CMD ["dist/index.js"]
```

## Python (Slim + Virtual Environment)
Use a builder stage to compile dependencies and a slim runtime stage to run them within a virtual environment.

```dockerfile
# Stage: builder
FROM python:3.12-slim AS builder
WORKDIR /app
RUN python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Stage: runtime
FROM python:3.12-slim AS runtime
WORKDIR /app
COPY --from=builder /opt/venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
COPY . .
USER nobody
CMD ["python", "main.py"]
```
