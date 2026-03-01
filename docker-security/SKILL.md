---
name: docker-security
description: Secure Docker containers and images with hardening, scanning, and secrets management. Use when configuring non-root users, implementing read-only filesystems, dropping Linux capabilities, running vulnerability scans (Trivy/Scout), or managing sensitive credentials via Docker Secrets.
---

# Docker Security

Implement robust security measures for your containerized applications following industry standards.

## Core Principles

- **Rootless by Default**: Never run container processes as root; use dedicated non-privileged users.
- **Least Privilege Runtime**: Drop unnecessary capabilities and enforce an immutable, read-only filesystem.
- **Continuous Scanning**: Integrate automated vulnerability checks into every step of the CI/CD pipeline.
- **Secure Secrets**: Avoid environment variables for sensitive data; use temporary mounts or dedicated secret stores.

## Detailed Guidance

- **Dockerfile Hardening**: Mandatory non-root user setup, `--chown` best practices, and Distroless base images. See [hardening-dockerfile.md](references/hardening-dockerfile.md).
- **Runtime Protection**: Secure execution parameters (`--read-only`, `--cap-drop`), and Compose Secrets integration. See [runtime-security.md](references/runtime-security.md).
- **Scanning & Compliance**: Vulnerability scanning with Trivy/Scout and automated CIS Benchmark validation. See [scanning-compliance.md](references/scanning-compliance.md).

## Related Resources

- Skill: `dockerfile-basics` - For basic image construction before applying security hardening.
- Skill: `docker-production` - For higher-level reliability and monitoring in secured environments.
- Skill: `docker-ci-cd` - For automating security scans within build workflows.
