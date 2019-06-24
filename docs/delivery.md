# Setting up Delivery

This step is the culmination of taking a Docker image and using the the Harbor robot user to push our image to the Harbor registry

## 

https://gitlab.com/stmpy/[PROJECT]/-/settings/ci_cd

## Building docker file and pushing images to harbor

```yaml
# Changed to use HARBOR instead of GitLab registry
.registry: &registry
  image: docker:stable
  services:
    - name: docker:dind
      command: ["--insecure-registry=$HARBOR_REGISTRY"]
  before_script:
    - echo "$HARBOR_PASSWORD" | docker login -u $HARBOR_USER $HARBOR_REGISTRY --password-stdin

# ...
# Add deploy stage
stages:
  - test
  - deploy

# ...

# add to existing variables top level declaration or create one if it doesn't exist
# define image name for ease of use
variables:
    IMAGE_NAME: $HARBOR_REGISTRY/$HARBOR_PROJECT_NAME/$CI_PROJECT_NAME

# run docker build, and push image to harbor registry
"Docker Build":
    <<: *registry
    stage: deploy
    script:
        - docker build -t $IMAGE_NAME:$CI_COMMIT_SHA ./
        - docker push $IMAGE_NAME:$CI_COMMIT_SHA
```

## Notes

- [GitLab CI Variables](https://docs.gitlab.com/ee/ci/variables/)