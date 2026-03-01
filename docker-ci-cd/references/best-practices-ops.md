# Docker CI/CD: Best Practices & Operations

## Caching Strategies
Improve build times by persisting Docker layer caches across pipeline runs.

### GitHub Actions (BuildKit)
```yaml
cache-from: type=gha
cache-to: type=gha,mode=max
```

### GitLab CI
```yaml
cache:
  key: docker-$CI_COMMIT_REF_SLUG
  paths: [.docker-cache]
```

## Security Best Practices
1. **Scan before push**: Always include a vulnerability scan (e.g., Trivy) in your pipeline.
2. **Sign images**: Use tools like `cosign` to verify image integrity.
3. **Least Privilege**: Use CI-specific registry tokens with limited scopes.

## Error Handling & Troubleshooting

### Common Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `unauthorized` | Bad credentials | Check registry secrets/tokens. |
| `rate limit` | Docker Hub limits | Authenticate pulls or use a mirror. |
| `cache miss` | First build | Normal on first run; cache will populate. |

### Debug Checklist
- [ ] Registry credentials valid?
- [ ] Docker daemon (DinD) running?
- [ ] Build context correct?
- [ ] Dockerfile present in root?
