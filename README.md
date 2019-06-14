# Blogging Series: Secure Pipelines

## Prerequisites

### Things you should already have (hopefully):
- A computer

![computer](images/bad_computer.jpg)

- A keyboard

![keyboard](images/bad_keyboard.jpg)

- Git

### Things to start downloading:
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

### Things we need to do
- Get everyone access to [Handouts](https://gethandouts.com)
- [Create Kubernetes Environment](docs/create_k8s.md)
- [Configure Admission Controls](docs/admission_controls.md)
- [Deploy Bookinfo Project](docs/deploy_bookinfo.md)

## Code Objectives

- [Setup demo project](docs/demo_project.md)
- [Signing Commits](docs/signing_commits.md)

## Container Objectives
- Authenticity: signing
- A/V: container scanning
- SAST: container security scanning
- DAST: container security scanning

## Registry Objectives

- [Signed Images](docs/signed_images.md)
- [Private Registry](docs/private_registry.md)
- [Image promotions](docs/image_promotions.md)
- [Configure Kubernetes to pull from private registry](docs/private_reg_k8s_config.md)

## Host Objectives:

- Kubernetes node restrictions
- Taints/Tolerances
- Runtime Security (falco)

Additional Objectives:

- Patch Management: container build process
- Notary
- Artifact Security (trust model)
- keybase GPG keys
- code quality

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
