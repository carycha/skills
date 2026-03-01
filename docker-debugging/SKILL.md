---
name: docker-debugging
description: Container debugging and troubleshooting techniques for production and development. Use when diagnosing container crashes (OOM, Segfault), performance issues (high CPU/Mem), networking failures (DNS, connectivity), or healthcheck status problems.
---

# Docker Debugging

Master the art of diagnosing and resolving container issues in any environment.

## Core Principles

- **Observability First**: Use logs and events to understand what happened.
- **Inspect, Don't Guess**: Query the container's state directly via `docker inspect`.
- **Reproduce in Context**: Test connectivity and health from *within* the same network.
- **Resource Aware**: Monitor stats and limits to catch OOMKilled and performance bottlenecks.

## Detailed Guidance

- **Inspection & Logging**: Advanced logging, time-based filters, and Go-template-based inspection. See [inspect-logs.md](references/inspect-logs.md).
- **Runtime Diagnosis**: Interactive shell (exec), stats monitoring, and exit code reference. See [runtime-diagnosis.md](references/runtime-diagnosis.md).
- **Network & Health Checks**: Connectivity tests, DNS troubleshooting, and healthcheck log review. See [network-health.md](references/network-health.md).
- **Specialized Tools & Best Practices**: Debug sidecars (netshoot), troubleshooting workflows, and common error fixes. See [debug-tools.md](references/debug-tools.md).

## Related Resources

- Skill: `docker-production` - For optimizing resource limits and reliability in production.
- Skill: `docker-networking` - For deeper understanding of container network bridges.
