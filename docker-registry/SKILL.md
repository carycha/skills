---
name: docker-registry
description: Docker Registry & Image Manager. Use when managing private registries (registry:2, ECR, GCR, GHCR), configuring auth (TLS/htpasswd), tagging strategies, or syncing images across registries using Skopeo.
---

# Docker Registry

Secure and efficient image distribution and management strategies for private registries.

## Core Principles

- **Security-First**: Always enforce authentication (htpasswd, IAM, OAuth) and TLS for private registries.
- **Repository Isolation**: Use separate repositories for different applications and environments.
- **Tag Management**: Use specific, immutable tags for production deployments; avoid overwriting tags.
- **Minimal Transfers**: Use tools like Skopeo for cross-registry synchronization to avoid the overhead of the local Docker daemon.

## Detailed Guidance

- **Private Registry Setup**: Self-hosted `registry:2` Compose configuration, htpasswd authentication, and TLS certificate setup. See [private-setup.md](references/private-setup.md).
- **Cloud Registry Operations**: Authentication reference for GHCR, AWS ECR, GCR, and ACR, including repository lifecycle examples. See [cloud-operations.md](references/cloud-operations.md).
- **Management & Sync**: Registry V2 API for cataloging and tag listing, and cross-registry sync using Skopeo. See [management-sync.md](references/management-sync.md).

## Related Resources

- Skill: `docker-optimization` - For optimizing images before pushing them to the registry.
- Skill: `docker-ci-cd` - For automating the push of images to private registries during the build process.
- Skill: `docker-security` - For hardening images and ensuring registry access control.
