# Setting up Delivery

## Create Harbor Robot User

## Create GitLab Variables in Project

https://gitlab.com/stmpy/[PROJECT]/-/settings/ci_cd

## Building docker file and pushing images to harbor

```yaml
"Docker Build":
    stage: build
    script:
        - docker build -t $HARBOR_REGISTRY_URL/$HARBOR_PROJECT_NAME:$CI_COMMIT_SHA ./
        - docker push $HARBOR_REGISTRY_URL/$HARBOR_PROJECT_NAME:$CI_COMMIT_SHA
```

## Help

- [GitLab CI Variables](https://docs.gitlab.com/ee/ci/variables/)
- 