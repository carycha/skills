# Docker Production: Observability Stack

## Logging Configuration
Prevent logs from filling up your disk by setting a maximum size and file rotation.

```yaml
services:
  app:
    logging:
      driver: json-file
      options:
        max-size: "10m" # Max 10MB per log file
        max-file: "3"    # Keep 3 most recent files
        labels: "app,env"
```

## Monitoring Stack (Prometheus + Grafana)
Deploy a sidecar monitoring stack to track CPU, RAM, and application metrics.

```yaml
services:
  prometheus:
    image: prom/prometheus:latest
    volumes: [./prometheus.yml:/etc/prometheus/prometheus.yml]
    ports: ["9090:9090"]

  grafana:
    image: grafana/grafana:latest
    ports: ["3000:3000"]
    environment: { GF_SECURITY_ADMIN_PASSWORD: ${GRAFANA_PASSWORD} }

  cadvisor: # Collects container metrics
    image: gcr.io/cadvisor/cadvisor:latest
    volumes:
      - /:/rootfs:ro
      - /var/run:/var/run:ro
      - /sys:/sys:ro
      - /var/lib/docker/:/var/lib/docker:ro
    ports: ["8080:8080"]
```

## Prometheus Config (Scraping)
```yaml
# prometheus.yml
global: { scrape_interval: 15s }

scrape_configs:
  - job_name: 'docker-containers'
    docker_sd_configs:
      - host: unix:///var/run/docker.sock
```
