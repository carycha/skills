# Docker Security: Scanning & Compliance

## Vulnerability Scanning (Trivy)
Regularly scan your images for vulnerabilities and fail CI builds on critical issues.

```bash
# Basic scan filtered by severity
trivy image --severity CRITICAL,HIGH myapp:latest

# CI/CD integration: Exit with error if CRITICAL found
trivy image --exit-code 1 --severity CRITICAL myapp:latest

# Scan Dockerfile directly
trivy config ./Dockerfile
```

## Docker Scout
Native Docker tool for identifying and remediating CVEs.

```bash
# Quick summary
docker scout cves myapp:latest

# Detailed Markdown report
docker scout cves --format markdown myapp:latest
```

## Compliance: CIS Docker Benchmark
Run a specialized tool to evaluate your Docker host and containers against the CIS standard.

```bash
# CIS Benchmark Check
docker run --rm --net host --pid host 
  -v /var/run/docker.sock:/var/run/docker.sock 
  docker/docker-bench-security
```

## Security Best Practices Checklist
- [ ] Non-root user with UID 1001 defined?
- [ ] Image scanned for vulnerabilities before release?
- [ ] No secrets in `ENV` or `ARG`?
- [ ] Runtime capabilities dropped (`ALL`)?
- [ ] Read-only filesystem configured?
