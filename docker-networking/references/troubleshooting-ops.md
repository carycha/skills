# Docker: Networking Operations & Troubleshooting

## Troubleshooting Checklist
- [ ] Network created? `docker network ls`
- [ ] Container connected? `docker inspect <container_id>`
- [ ] DNS resolving? `docker exec app nslookup <target_service>`
- [ ] Correct port mapping? `docker port <container_id>`

## Diagnostic Commands
Use these commands to diagnose connectivity issues from *inside* a container.

```bash
# Verify DNS resolution
docker exec app nslookup backend_service

# Test connectivity to specific ports
docker exec app curl http://backend:3000/health

# Inspect a specific network's status and connected containers
docker network inspect my_network
```

## Common Networking Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `network not found` | Typo in name or deleted. | Create with `docker network create`. |
| `address already in use` | Port conflict on host. | Change host port in `-p` mapping. |
| `cannot reach service` | Wrong network membership. | Verify all containers are on the same network. |
| `DNS lookup failed` | Service not ready yet. | Check health checks or service logs. |

## Specialized Tooling: netshoot
Run a temporary container with full networking tools (`tcpdump`, `dig`, `nmap`) attached to the network being debugged.
```bash
docker run --rm -it --network <network_name> nicolaka/netshoot
```
