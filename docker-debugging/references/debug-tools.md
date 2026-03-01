# Docker Debugging: Specialized Tools & Best Practices

## Debug Containers (e.g., netshoot)
Run a sidecar container with diagnostic tools (curl, dig, nmap, tcpdump) in the same network as your target.

```bash
docker run --rm -it --network <network_name> nicolaka/netshoot
```

## Troubleshooting Workflow

1. **Won't Start?** Check `docker logs`, exit code, and verify image existence.
2. **Unhealthy?** Review health logs and manually test endpoints.
3. **High Resources?** Monitor `docker stats`, increase limits, and profile code.
4. **Network Failed?** Check DNS (`nslookup`), connectivity (`ping`/`curl`), and network membership.

## Common Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| `container not found` | Invalid name or ID. | Run `docker ps -a` to find the correct ID. |
| `exec failed` | Container is stopped. | Start the container before executing. |
| `no such file/directory`| Binary missing or bad PATH. | Verify image content; ensure binary exists. |

## Tips for Better Debugging
- **Name your containers**: Makes `docker exec` and `docker logs` much easier.
- **Use meaningful healthchecks**: Avoid just `exit 0`; test the actual service.
- **Keep images minimal**: But include basic tools (`sh`, `curl`, `wget`) for dev images.
