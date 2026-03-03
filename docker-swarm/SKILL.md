---
name: docker-swarm
description: Docker Swarm Orchestration Expert. Use when initializing clusters, managing manager/worker nodes, deploying high-availability services/stacks, or managing encrypted secrets and configs in multi-host environments.
---

# Docker Swarm

Master native Docker container orchestration for scalable and resilient production environments.

## Core Principles

- **High Availability**: Deploy redundant manager nodes to ensure cluster quorum and service continuity.
- **Declarative State**: Define your desired service state (replicas, networks, ports) and let Swarm maintain it.
- **Zero-Downtime Updates**: Use rolling update strategies to ship new images without service interruption.
- **Secure by Default**: Leverage overlay network encryption and built-in secret management.

## Detailed Guidance

- **Cluster & Node Management**: Initializing clusters, managing join tokens, promoting/demoting managers, and maintenance modes (Drain). See [cluster-nodes.md](references/cluster-nodes.md).
- **Services & Stacks**: Multi-host service deployment, `docker stack` YAML configuration, placement constraints, and update/rollback policies. See [services-stacks.md](references/services-stacks.md).
- **Secrets, Configs & Troubleshooting**: Encrypted data storage, configuration management, aggregated logging, and quorum recovery strategies. See [secrets-configs-ops.md](references/secrets-configs-ops.md).

## Related Resources

- Skill: `docker-networking` - For deep understanding of overlay networks used in Swarm.
- Skill: `docker-production` - For higher-level production best practices applicable to any orchestrator.
- Skill: `docker-security` - For hardening the images and configurations used in your services.
