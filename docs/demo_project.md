# Setting up our demo project

## Setup GitLab Account

First off, lets create a gitlab account by [registering for Gitlab](https://gitlab.com/users/sign_in#register-pane)

![GitLab registration page](images/gitlab_registration.png)

We need to confirm our account now:

![Email confirmation page](images/gitlab_email_confirmation.png)

go to inbox and "Confirm your account"

![Email confirm](images/gitlab_email_confirm.png)

Login for the first time

![First Login](images/gitlab_first_login.png)


## Fork project
First fork [istio bookinfo details app](https://gitlab.com/sbs-labs/secure-pipeline/bookinfo-details)

![fork gitlab project](images/fork_selection.png)

```
# clone your fork
git clone git@gitlab.com:<USERNAME>/bookinfo-details details
```
## Make a change
lets change the details application to 

```
# initialize our own details project
cd details
git commit -m "Initial commit using key signing"
```
