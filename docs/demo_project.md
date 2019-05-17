# Setting up our demo project

Clone down [GitLab Book Info Project](https://gitlab.com/sbs-labs/secure-pipeline/bookinfo-details) this will be the application we work with throughout the lab, building a secure pipeline

There are other parts of the overall service which will already be available in our kubernetes clusters.

```bash
# clone project
git clone https://gitlab.com/sbs-labs/secure-pipeline/bookinfo-details  details

# initialize our own details project
cd details
git init
git remote add origin {PERSONAL_PROJECT_URL}
git add .
git commit -m "Initial commit using key signing"
```
