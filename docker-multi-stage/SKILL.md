---
name: docker-multi-stage
description: Docker Image Size Optimizer. Use when the user asks to implement multi-stage builds to reduce image size, separate build/runtime environments, or harden images using Distroless/Alpine. 「Docker 多階段構建優化」
---

# Docker Multi-Stage Builds

Maximize efficiency and security by separating your build toolchain from your runtime environment.

## Core Principles

- **Build/Runtime Separation**: Use heavy images for building, and minimal images for running.
- **Artifact Copying**: Only transfer the final binary or distribution to the production stage.
- **Minimal Surface Area**: Prefer `distroless` or `scratch` to minimize vulnerability exposure.
- **Layer Optimization**: Order your commands from least frequent to most frequent changes to leverage caching.

## Detailed Guidance

- **Node.js & Python Patterns**: Distroless Node.js builds and virtual-env-based Python optimizations. See [node-python-patterns.md](references/node-python-patterns.md).
- **Compiled Languages (Go, Rust, Java)**: Static binaries on `scratch`, `musl` for Rust, and JRE-only runtimes for Java. See [compiled-languages.md](references/compiled-languages.md).
- **Optimization & Operations**: Image size comparison tables, debugging with `dive`, and common error handling. See [optimization-ops.md](references/optimization-ops.md).

## Related Resources

- Skill: `docker-optimization` - For general Dockerfile and layer caching optimizations.
- Skill: `dockerfile-basics` - For fundamental Dockerfile syntax and commands.
