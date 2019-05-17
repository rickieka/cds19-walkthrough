# Setting up our demo project

run:

```bash
# clone project
git clone https://gitlab.com/sbs-labs/secure-pipeline/bookinfo-details  details

# initialize our own details project
cd details
git init
git remote add origin [[PERSONAL_PROJECT_URL]]
git add .
git commit -m "Initial commit using key signing"
```

[GitLab Book Info Project](https://gitlab.com/sbs-labs/secure-pipeline/bookinfo-details)

We'll run the rest of the project through the upstream repositories from istio.
