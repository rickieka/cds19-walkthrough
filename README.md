# Blogging Series: Secure Pipelines

Code Objectives:
- signing commits

Container Objectives:
- Patch Management: container build process
- Authenticity: signing
- A/V: container scanning
- Secure/Trusted Delivery: Registry promotion

Host Objectives:
- Kubernetes node

## Code Objectives

### Signing Commits
[Git Signing](https://git-scm.com/book/en/v2/Git-Tools-Signing-Your-Work)
get the ID of your gpg key `gpg --list-keys` and configure git to use that key

    # had to do this to import keybase pgp key, only for the import
    export GPG_TTY=$(tty)
    # configure git
    git config --global user.signingkey [KEYID]
    git config --global commit.gpgsign true
    # if having issues w/ gpg
    gpgconfg --kill gpg-agent

when you commit, add in the `-S` tag to make sure you sign the commit

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


