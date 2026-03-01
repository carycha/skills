# Docker Swarm: Secrets, Configs & Troubleshooting

## Secrets & Config Management
Swarm provides encrypted storage for sensitive data (Secrets) and non-sensitive files (Configs).

### Using Secrets
```bash
# 1. Create secret from file or stdin
echo "mypassword" | docker secret create db_password -

# 2. Add to existing service
docker service update --secret-add db_password my_service
```

### Rotating Secrets
Update a secret by creating a new version and replacing it in the service.
```bash
docker secret create db_password_v2 ./new_pass.txt
docker service update 
  --secret-rm db_password 
  --secret-add source=db_password_v2,target=db_password 
  my_service
```

## Troubleshooting Swarm

### Common Status Commands
```bash
# List all services across cluster
docker service ls

# View task placement and status (crucial for finding crashes)
docker service ps <service_name>

# View aggregated logs for all replicas
docker service logs -f <service_name>
```

### Quorum Recovery (Emergency)
If more than half of your managers are down, the cluster loses its leader.
```bash
# Force a new cluster from a single manager
docker swarm init --force-new-cluster --advertise-addr <CURRENT_NODE_IP>
```

### Common Errors
- `No suitable node`: Check `placement` constraints and node resources.
- `Task not converging`: Usually a healthcheck failure or application crash on startup. Check `service ps` and `service logs`.
