# Docker Security: Runtime Protection

## Secure Runtime Execution
Run your containers with a minimal set of privileges to mitigate potential compromises.

```bash
docker run 
  --security-opt no-new-privileges:true \ # Prevent privilege escalation
  --cap-drop ALL \                        # Drop all Linux capabilities
  --cap-add NET_BIND_SERVICE \             # Only add what's necessary
  --read-only \                           # Immutable root filesystem
  --tmpfs /tmp:rw,noexec,nosuid \          # Temporary writable paths
  --user 1001:1001 \                       # Hard-coded UID:GID
  myapp:latest
```

## Secret Management (Compose)
Use Docker Secrets to provide sensitive files to your containers without using environment variables.

```yaml
services:
  database:
    image: postgres:16-alpine
    secrets: [db_password]
    environment:
      POSTGRES_PASSWORD_FILE: /run/secrets/db_password

secrets:
  db_password:
    file: ./secrets/db_password.txt
```

## Hardened Compose Best Practices

| Setting | Recommendation |
|---------|----------------|
| `security_opt` | `no-new-privileges:true` |
| `read_only` | `true` (use `tmpfs` for writable folders) |
| `cap_drop` | `[ALL]` |
| `network_mode` | Isolated bridge or internal-only. |
| `pids_limit` | Set to prevent fork bombs (e.g., 100). |
