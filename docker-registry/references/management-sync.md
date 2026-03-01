# Docker: Registry Management & Sync

## Cross-Registry Sync (Skopeo)
`skopeo` is a powerful tool to copy, inspect, and sync images without requiring a full `docker pull`/`push` cycle (no Docker daemon needed).

```bash
# Copy between registries
skopeo copy 
  docker://source-registry/image:tag 
  docker://dest-registry/image:tag

# Sync all tags from source to dest
skopeo sync --src docker --dest docker 
  source-registry/repo dest-registry/
```

## Image & Tag Management (API)
You can query the Registry V2 API directly for catalog and tags.

```bash
# List all repositories in a private registry
curl -X GET https://registry.example.com/v2/_catalog

# List tags for a specific image
curl -X GET https://registry.example.com/v2/myapp/tags/list

# Delete an image by digest
curl -X DELETE https://registry.example.com/v2/myapp/manifests/<digest>
```

## Error Handling Checklist

| Error | Cause | Solution |
|-------|-------|----------|
| `unauthorized` | Credentials expired or missing. | Run `docker login` again. |
| `manifest unknown`| Image or tag not in registry. | Check spelling and `docker tag` history. |
| `denied: access` | Role or policy missing (RBAC). | Check IAM roles or registry permissions. |
| `TLS handshake` | Unknown CA certificate. | Add CA cert to `/etc/docker/certs.d`. |
