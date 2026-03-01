# Docker: Private Registry Setup

## Self-Hosted Registry (registry:2)
Run a private registry in your own infrastructure using Docker Compose.

```yaml
services:
  registry:
    image: registry:2
    ports: ["5000:5000"]
    volumes:
      - registry_data:/var/lib/registry
      - ./auth:/auth
      - ./certs:/certs
    environment:
      REGISTRY_AUTH: htpasswd
      REGISTRY_AUTH_HTPASSWD_REALM: Registry Realm
      REGISTRY_AUTH_HTPASSWD_PATH: /auth/htpasswd
      REGISTRY_HTTP_TLS_CERTIFICATE: /certs/domain.crt
      REGISTRY_HTTP_TLS_KEY: /certs/domain.key
    restart: unless-stopped

volumes:
  registry_data:
```

## Authentication (htpasswd)
Create an encrypted credentials file for the registry.
```bash
docker run --rm --entrypoint htpasswd 
  httpd:alpine -Bbn admin your_password > auth/htpasswd
```

## Local Trusted Certificates
If using a self-signed certificate, you must add it to the Docker daemon's trusted certificates directory:
`/etc/docker/certs.d/registry.example.com:5000/ca.crt`
