# Docker Networking: Drivers & Ports

## Network Driver Comparison

| Driver | Use Case | Multi-Host | Isolation Level |
|--------|----------|------------|-----------------|
| **bridge** | Default for single host. | No | High (internal subnet) |
| **host** | Max performance (bypass stack). | No | None (uses host IP) |
| **overlay** | Multi-host (Swarm/K8s). | Yes | High (encrypted VXLAN) |
| **macvlan** | Assign physical IP to container. | No | Very High |
| **none** | Total isolation. | No | Absolute |

## Custom Bridge Network
Create a dedicated subnet for your application to ensure clean service discovery and isolation.

```bash
# Create network
docker network create --driver bridge --subnet 172.28.0.0/16 my_network

# Run container on specific network
docker run -d --name app --network my_network nginx:alpine
```

## Port Mapping (Publishing)
Map container ports to the host machine.

```bash
# Map host:container
docker run -p 8080:80 nginx

# Bind to localhost ONLY (Recommended for Security)
docker run -p 127.0.0.1:8080:80 nginx

# UDP port mapping
docker run -p 53:53/udp dnsserver

# Random host port
docker run -P nginx
```
