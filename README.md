# Blogging Series: Secure Pipelines

Code Objectives:
- signing commits

Container Objectives:
- Authenticity: signing
- A/V: container scanning

Registry Objectives:
- Signing images
- Secure/Trusted Delivery: Registry promotion

Additional Objectives:
- Notary
- Patch Management: container build process
- Artifact Security (trust model)
- keybase GPG keys

Host Objectives:
- Kubernetes node

## Code Objectives

- [Signing Commits](docs/signing_commits.md)

## Container Objectives

- [Istio Docs](https://istio.io/docs/examples/bookinfo/)
- [Code](https://github.com/istio/istio/tree/master/samples/bookinfo/src)

We'll be modifying the details page

### Nodes
in a managed solution, access to the Node isn't always permitted, as such you rely on the vendor to keep your nodes up to date. In a non-managed solution it is important to understand how to safetly pull a node out of the cluster, upgrade it and put it back in the cluster.

## Regisry Objectives

### Signed Images

[Docker content trust](https://docs.docker.com/engine/security/trust/content_trust/)

## Aditional Objectives

- [Static Application Security Testing](docs/sast.md)
- [Patch Management](docs/patch_management.md)
- [Using Keybase](docs/keybase.md)
