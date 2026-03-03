---
name: docker-networking
description: Docker Networking Expert. Use when the user asks to configure custom bridges, overlay networks, multi-tier isolation, service discovery, or troubleshoot connectivity. 「Docker 網路配置專家」
---

# Docker Networking

Master the flow of traffic and service discovery between your containers.

## Core Principles

- **Isolation by Default**: Containers on different networks cannot communicate.
- **Service Discovery**: Containers on the same network resolve each other by name (DNS).
- **Least Privilege Exposure**: Only map necessary ports to the host; keep backend services on internal networks.
- **Explicit Connectivity**: Always define networks in Compose to avoid relying on the default bridge.

## Detailed Guidance

- **Drivers & Ports**: Bridge, host, and overlay driver comparisons, port publishing, and custom subnets. See [drivers-ports.md](references/drivers-ports.md).
- **Service Discovery & Compose**: Internal DNS resolution, network isolation strategies, and multi-host overlay networks. See [compose-discovery.md](references/compose-discovery.md).
- **Operations & Troubleshooting**: Connectivity tests (Ping, Curl), DNS diagnosis, common error fixes, and netshoot. See [troubleshooting-ops.md](references/troubleshooting-ops.md).

## Related Resources

- Skill: `docker-compose-setup` - For basic multi-container service definitions.
- Skill: `docker-swarm` - For multi-host container orchestration using overlay networks.
