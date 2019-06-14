# Kubernetes Admission Controls

[Link to Kubernetes documentation](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/)

We will be setting up an admission control that only allows us to deploy images from our own (private) registry - this does mean that you won't be able to pull images straight from public registries such as docker hub.

In Kubernetes v1.14 the `ValidatingAdmissionWebhook` is already enabled, which is what we need to run [OPA](https://www.openpolicyagent.org/). OPA will be the admission controller, that is doing the validations for us. We will go through the process of configuring OPA to whitelist the registry we will be using.

NOTES:
- https://stackoverflow.com/questions/54463125/how-to-reject-docker-registries-in-kubernetes
- https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/
- https://www.openpolicyagent.org/docs/latest/kubernetes-admission-control/

[BACK](README.md)
