---
name: docker-compose-setup
description: Docker Compose Orchestration Expert. Use when the user asks to design multi-container architectures, configure networks/volumes, implement healthchecks, or troubleshoot service startup sequences. 「Docker Compose 編排專家」
---

# Docker Compose Setup

Design and manage complex multi-container architectures with modern Docker Compose.

## Core Principles

- **Declarative Services**: All container configurations are defined in a single file.
- **Service Isolation**: Use internal networks for communication, exposing only what's necessary.
- **Ordered Startup**: Use health-based dependencies (`condition: service_healthy`) for reliable boot.
- **Environment Parity**: Maintain consistency across dev, staging, and production using overrides.

## Detailed Guidance

- **Modern Syntax & Stacks**: 2024-2025 Compose syntax, standard multi-service templates, and healthcheck configurations. See [modern-syntax-stacks.md](references/modern-syntax-stacks.md).
- **Environment Management & Profiles**: Override patterns, .env interpolation, and service profiles for conditional startup. See [env-profiles.md](references/env-profiles.md).
- **Operations & Troubleshooting**: Management commands (Scale, Config), healthcheck debugging, and error handling. See [ops-troubleshooting.md](references/ops-troubleshooting.md).

## Related Resources

- Skill: `docker-networking` - For deep dives into custom network bridges and isolation.
- Skill: `docker-volumes` - For advanced storage strategies and data persistence.
- Skill: `docker-production` - For optimizing Compose for high-availability environments.
