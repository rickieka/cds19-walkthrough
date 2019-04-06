# Blogging Series: Secure Pipelines

Container Objectives:
- Patch Management: container build process
- A/V: container scanning
- Secure/Trusted Delivery: Registry promotion

Host Objectives:
- Kubernetes node

## Patch Management
patch management is the ability to apply software "patches" to your environment. With containerization this is a culmination of two parts - the containers themselves and the nodes they reside on.

Objectives:
- base images
- branch image
- project image
- node updates

### Containers

#### Base Image
alpine FTW

### Nodes
in a managed solution, access to the Node isn't always permitted, as such you rely on the vendor to keep your nodes up to date. In a non-managed solution it is important to understand how to safetly pull a node out of the cluster, upgrade it and put it back in the cluster.


