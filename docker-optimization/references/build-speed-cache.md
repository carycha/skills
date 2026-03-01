# Docker Optimization: Build Speed & Caching

## BuildKit Advanced Caching
Mount a persistent cache for your package manager during the build to avoid re-downloading dependencies.

```dockerfile
# syntax=docker/dockerfile:1
FROM node:20-alpine

# Use npm cache mount (BuildKit only)
RUN --mount=type=cache,target=/root/.npm 
    npm ci

# Python example
RUN --mount=type=cache,target=/root/.cache/pip 
    pip install -r requirements.txt
```

## Layer Caching Strategy
Order your commands from **least frequently changed** to **most frequently changed**.

### ✅ Good: Dependencies First
```dockerfile
COPY package*.json ./
RUN npm ci # Cached unless package.json changes

COPY . . # Changes on every build
RUN npm run build
```

### ❌ Bad: Redundant Rebuilds
```dockerfile
COPY . .
RUN npm ci # Re-runs on EVERY code change
```

## Parallel Build Stages
BuildKit can build independent multi-stage stages in parallel, significantly reducing total build time.

```dockerfile
FROM node:20-alpine AS deps
COPY package*.json ./
RUN npm ci

# These two stages will build simultaneously
FROM deps AS builder
COPY . .
RUN npm run build

FROM deps AS linter
COPY . .
RUN npm run lint
```
