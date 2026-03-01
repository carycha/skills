# Docker Swarm: Cluster & Node Management

## Cluster Initialization
Start a new Swarm cluster on your primary manager node.

```bash
# 1. Initialize cluster
docker swarm init --advertise-addr <MANAGER_IP>

# 2. Retrieve join tokens
docker swarm join-token worker
docker swarm join-token manager

# 3. Join from another node
docker swarm join --token <TOKEN> <MANAGER_IP>:2377
```

## High Availability (HA)
To maintain a stable quorum, always deploy an **odd number** of manager nodes (3 or 5).
- **3 managers**: Tolerates 1 failure.
- **5 managers**: Tolerates 2 failures.

## Node Lifecycle Operations

| Operation | Command | Purpose |
|-----------|---------|---------|
| **List Nodes** | `docker node ls` | View all nodes and status. |
| **Drain Node** | `docker node update --availability drain <ID>` | Evict all tasks for maintenance. |
| **Activate Node**| `docker node update --availability active <ID>` | Allow node to receive tasks again. |
| **Promote** | `docker node promote <ID>` | Upgrade worker to manager. |
| **Demote** | `docker node demote <ID>` | Downgrade manager to worker. |
| **Label Node** | `docker node update --label-add role=db <ID>` | Add metadata for placement constraints. |
