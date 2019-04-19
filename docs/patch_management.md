# Patch Management
patch management is the ability to apply software "patches" to your environment. With containerization this is a culmination of two parts - the containers themselves and the nodes they reside on.

__Objectives:__
- base images
- branch image
- project image
- node updates

## Base Image

- alpine FTW
- alpine install virtual
- alpine cleanup install cache
- Docker multi-stage images

### Alpine Virtual Install
```bash
apk --update --no-cache .build-utils add \
  gcc \
  build-base

apk del .build-utils
```


## Branch Image

## Project Image

## Node Updates
