# First signed commit with gpg key

## Verified status & CI
Lets add CI to our details project

```yaml
# .gitlab-ci.yml
"Hello CI World":
  script:
    - echo "Hello World"
```

Now lets do a signed commit and push the ci file to our repo

```bash
# if you setup auto signing you can leave off the -S flag
# but we'll leave it on to make sure we really do sign it
git add .gitlab-ci.yml
git commit -S -m "Signing commit, and setting up CI"
```

Navigate to your project to see both the _Verified_ status and that CI is running

![verified ci](images/verified_ci.png)

[Back](README.md)
