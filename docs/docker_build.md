# Building Docker images

```yaml
# .gitlab-ci.yml
# This will help us reduce duplication later on in the process
# gitlab runs off of stages: test, build, deploy, right now we only want to build
stages:
 - build

# ...

.registry: &registry
  image: docker:stable
  services:
    - docker:dind
  before_script:
    - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY

# ...

# The job that runs the build process
"Docker build":
  <<: *registry
  stage: build
  script:
    - docker build -t $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA .

# ...
```

We want to use these to push our docker images to Harbor, first we need to setup