# Robot Users

Harbor provides the ability to generate users that are not tied to a human's account. This is beneficial for the fact that if permissions change for someone, it won't break build processes.

## Create Robot User

![Create Robot User](images/create_robot_account.png)
![Robot User Credentials](images/robot_user.png)

## Set Variables in GitLab

go to this URL https://gitlab.com/[USERNAME_OR_GROUP]/[PROJECT_NAME]/-/settings/ci_cd

```sh
HARBOR_USER=robot$gitlab-integration
HARBOR_PASSWORD=[AS_PROVIDED]
HARBOR_PROJECT_NAME=travis
HARBOR_REGISTRY_URL=https://harbor.secpipe.stmpy.me
```

![Setting variables in GitLab](images/set_variables_in_gitlab.png)

## Using these variables in GitLab CI

you can call the variables just as they are declared in the CI/CD settings within your `gitlab-ci.yml` file

```yaml
# ...
"Some Job":
    script:
        - echo $HARBOR_REGISTRY_URL
# ...
```

## Building Docker images

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