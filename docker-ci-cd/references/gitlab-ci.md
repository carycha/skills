# Docker CI/CD: GitLab CI

## Pipeline Configuration
Automated build, security scan, and deployment steps using GitLab CI and SSH.

```yaml
# .gitlab-ci.yml
stages:
  - build
  - scan
  - deploy

variables:
  DOCKER_IMAGE: $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA

build:
  stage: build
  image: docker:24
  services:
    - docker:24-dind
  script:
    - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY
    - docker build -t $DOCKER_IMAGE .
    - docker push $DOCKER_IMAGE

scan:
  stage: scan
  image:
    name: aquasec/trivy
    entrypoint: [""]
  script:
    - trivy image --exit-code 1 --severity CRITICAL $DOCKER_IMAGE

deploy:
  stage: deploy
  script:
    - ssh deploy@server "docker pull $DOCKER_IMAGE && docker compose up -d"
  only:
    - main
```

## Security
Always use authenticated pulls for your private images in the deploy stage.
