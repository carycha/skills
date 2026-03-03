---
name: docker-production
description: Docker Production Deployment Expert. Use when the user asks to configure high-availability healthchecks, resource governance, monitoring stacks (Prometheus/Grafana), or rolling updates. 「Docker 生產環境部署專家」
---

# Docker Production

Architect and manage reliable, observable, and scalable container deployments.

## Core Principles

- **Observability by Design**: Always include healthchecks and external metrics exporters.
- **Resource Governance**: Explicitly define CPU and memory limits to ensure stability.
- **Persistent Logging**: Configure log rotation and external storage to prevent disk exhaustion.
- **Zero-Downtime Deployment**: Prefer rolling updates or blue-green strategies for production rollouts.

## Detailed Guidance

- **Reliability & Resources**: Production healthcheck parameters, resource limits/reservations, and restart policies. See [reliability-resources.md](references/reliability-resources.md).
- **Observability Stack**: Logging driver configuration, and Prometheus/Grafana/cAdvisor monitoring stacks. See [observability-stack.md](references/observability-stack.md).
- **Deployment & Operations**: Rolling updates, blue-green strategies, and production diagnostic commands. See [deployment-ops.md](references/deployment-ops.md).

## Related Resources

- Skill: `docker-debugging` - For resolving production issues when healthchecks or OOMKilled events trigger.
- Skill: `docker-ci-cd` - For automating the deployment of these production configurations.
- Skill: `docker-security` - For hardening production containers against attack.
