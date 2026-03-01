# Docker: Storage Troubleshooting & Permissions

## Permission Denied (UID/GID Mismatch)
If your container user (e.g., `node` or `postgres`) doesn't match the host UID/GID of a bind-mounted path, you will get permission errors.

### Diagnostics
```bash
# Check UID inside the container
docker exec <container_id> id

# Check folder ownership
docker run --rm -v my_volume:/data alpine ls -la /data
```

### Fix: Change Ownership
```bash
# Force the volume content to be owned by container user (e.g., UID 1000)
docker run --rm -v my_volume:/data alpine chown -R 1000:1000 /data
```

## Troubleshooting Checklist
- [ ] **Exists?** Run `docker volume ls` to verify the volume name.
- [ ] **Mounted?** Run `docker inspect <container> --format '{{json .Mounts}}'` to see active mount points.
- [ ] **Persistence?** Stop/Start the container; data in a volume should still be there.
- [ ] **Space?** Run `docker system df` to check for disk exhaustion.

## Common Storage Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `volume in use` | A container is still attached. | Stop the container before deleting the volume. |
| `no space left` | Volume partition or host is full. | Run `docker volume prune` or expand disk. |
| `path not found`| Bind mount source path missing. | Ensure the directory exists on the host. |
| `permission denied` | Incompatible UID/GID. | Use `chown` to match the container user. |
