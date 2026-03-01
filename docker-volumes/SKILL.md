---
name: docker-volumes
description: Implement persistent storage with Docker volumes, bind mounts, and backup strategies. Use when configuring data persistence for databases, setting up bind mounts for local development, managing memory-based tmpfs storage, or performing volume backup and restore operations.
---

# Docker Volumes

Master the strategies for persistent and temporary storage in containerized environments.

## Core Principles

- **Separation of Data**: Never store persistent data inside the container's writable layer; always use volumes or bind mounts.
- **Named Volumes for Production**: Use Docker-managed named volumes for reliability and easier migration.
- **Bind Mounts for Dev**: Use host-path mapping for source code to enable hot-reloading.
- **Security & Permissions**: Always verify UID/GID compatibility between the host and container to avoid "Permission Denied" errors.

## Detailed Guidance

- **Storage Mount Types & Operations**: Comparison of Named, Bind, and Tmpfs mounts, lifecycle commands, and CLI usage. See [mount-types-ops.md](references/mount-types-ops.md).
- **Compose Configuration & Backups**: Defining volumes in Compose, and specific recipes for backing up, restoring, and cloning data. See [compose-backups.md](references/compose-backups.md).
- **Storage Troubleshooting & Permissions**: Fixing UID/GID mismatches, disk space analysis, and common error resolution. See [permissions-troubleshooting.md](references/permissions-troubleshooting.md).

## Related Resources

- Skill: `docker-compose-setup` - For basic service and volume definitions in multi-container apps.
- Skill: `docker-production` - For high-availability storage strategies and monitoring.
