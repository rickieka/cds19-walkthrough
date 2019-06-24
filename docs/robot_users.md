# Robot Users

Harbor provides the ability to generate users that are not tied to a human's account. This is beneficial for the fact that if permissions change for someone, it won't break build processes.

## Create Robot User

![Create Robot User](images/create_robot_account.png)
![Robot User Credentials](images/robot_user.png)

## Set Variables in GitLab

go to this URL https://gitlab.com/[USERNAME_OR_GROUP]/[PROJECT_NAME]/-/settings/ci_cd

```sh
# Make sure to add $$ to escape the username - or gitlab will try to do variable substitution to it
HARBOR_USER=robot$$gitlab-integration
HARBOR_PASSWORD=[AS_PROVIDED]
HARBOR_PROJECT_NAME=travis
HARBOR_REGISTRY=harbor.secpipe.stmpy.me
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

## Notes:
- https://stackoverflow.com/questions/50133073/gitlab-ci-docker-in-docker-access-to-insecure-registry#50133074
- https://docs.gitlab.com/ee/ci/variables/#gitlab-ciyml-defined-variables
