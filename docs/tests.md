# Tests: Appication tests

running tests on boolio-api

```yaml
# .gitlab-ci.yml
# ...

"Tests":
  stage: test
  image: $RUBY_IMAGE
  script:
    - bundle install
    - rails test

# ...
```
