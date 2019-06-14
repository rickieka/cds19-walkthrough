# Kubernetes Admission Controls

[Link to Kubernetes documentation](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/)

We will be setting up an admission control that only allows us to deploy images from our own (private) registry - this does mean that you won't be able to pull images straight from public registries such as docker hub.

NOTES:
- https://stackoverflow.com/questions/54463125/how-to-reject-docker-registries-in-kubernetes
- https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/
