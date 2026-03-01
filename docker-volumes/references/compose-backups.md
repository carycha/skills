# Docker: Compose Configuration & Backups

## Volume Configuration in Compose
Define your storage layer for multi-container apps.

```yaml
services:
  db:
    image: postgres:16-alpine
    volumes:
      - db_data:/var/lib/postgresql/data
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql:ro

  app:
    image: myapp
    volumes:
      - uploads:/app/uploads
      - type: tmpfs
        target: /app/tmp

volumes:
  db_data: # Docker-managed named volume
  uploads: { external: true } # Already created by another process
```

## Backup & Restore Strategies
Docker volumes are stored in host system paths (usually `/var/lib/docker/volumes`). Use a temporary container to access and back them up safely.

### Backup to Tarball
```bash
# Backup a volume named 'app_data' to a local .tar.gz
docker run --rm 
  -v app_data:/source:ro 
  -v $(pwd)/backups:/backup 
  alpine tar czvf /backup/app_data_$(date +%Y%m%d).tar.gz -C /source .
```

### Restore from Tarball
```bash
docker run --rm 
  -v app_data:/dest 
  -v $(pwd)/backups:/backup:ro 
  alpine tar xzvf /backup/app_data_20240101.tar.gz -C /dest
```

### Clone/Sync Volume
```bash
docker run --rm 
  -v source_vol:/from:ro 
  -v target_vol:/to 
  alpine cp -av /from/. /to/
```
