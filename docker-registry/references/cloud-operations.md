# Docker: Cloud Registry Operations

## Multi-Provider Login Reference

| Provider | Authentication Command |
|----------|------------------------|
| **Docker Hub** | `docker login` |
| **GHCR** | `echo $GITHUB_TOKEN | docker login ghcr.io -u USER --password-stdin` |
| **AWS ECR** | `aws ecr get-login-password --region REGION | docker login --username AWS --password-stdin ACCOUNT.dkr.ecr.REGION.amazonaws.com` |
| **Google GCR**| `gcloud auth configure-docker` |
| **Azure ACR** | `az acr login --name REGISTRY_NAME` |

## Repository Lifecycle: AWS ECR
```bash
# 1. Create Repository
aws ecr create-repository --repository-name myapp

# 2. Login
aws ecr get-login-password --region us-east-1 | 
  docker login --username AWS --password-stdin <account_id>.dkr.ecr.us-east-1.amazonaws.com

# 3. Tag & Push
docker tag myapp:latest <account_id>.dkr.ecr.us-east-1.amazonaws.com/myapp:latest
docker push <account_id>.dkr.ecr.us-east-1.amazonaws.com/myapp:latest
```

## Push/Pull Best Practices
Always use specific tags instead of `latest` for production pulls to ensure build reproducibility.
