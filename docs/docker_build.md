# Docker build

Now lets actually build our docker image and make sure that happens successfully

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

At this point, the image is building, but nothing is happening with it - lets get an image registry setup now
