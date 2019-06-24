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

