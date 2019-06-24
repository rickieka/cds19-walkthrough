# Private Registry (Harbor)

## Helm

using the helm method to install, if you need helm go [here](https://helm.sh/docs/)

make sure to be on helm `2.14.1` because of [this](https://github.com/helm/helm/issues/5750)

## Cert Installation

The cert can be handled multiple ways, regardless of how it is done you should end up with a secret containing the certificate

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: harbor-tls # the name I chose for my secret
type: kubernetes.io/tls
data:
  tls.key: [KEY] # base64 encoded
  tls.crt: [CERT_FROM_CA] # base64 encoded
  ca.crt: [BUNDLE_FROM_CA] # base64 encoded
```

### Cert-Manager (Using Let's Encrypt)

[Cert-Manager](https://github.com/jetstack/cert-manager) by [JetStack](https://www.jetstack.io)

[Quick Start](https://github.com/jetstack/cert-manager/blob/master/docs/tutorials/acme/quick-start/index.rst)
More specifically: [Installing Cert-Manager](https://github.com/jetstack/cert-manager/blob/master/docs/tutorials/acme/quick-start/index.rst#step-5---deploy-cert-manager)

### Purchase your own cert

setup secret names `harbor-tls`

When purchasing your own cert, you will use the combination of the server key and the certificate that you are provided

```sh
# basic generation of a new CSR and private key
openssl req -new -newkey rsa:2048 -nodes -keyout server.key -out server.csr
```

Uploading the certificate to Kubernetes
```
kubectl create secret tls harbor-tls --key harbor_server_private.key --cert harbor_secpipe_stmpy_me.crt
```

### Self-Signed

Always an option - great for testing things out

## Harbor Installation

[Installing via Helm](https://github.com/goharbor/harbor-helm)

Create `values.yaml`

```yaml
# values.yaml
expose:
  tls:
    secretName: harbor-tls
  ingress:
    annotations:
       kubernetes.io/ingress.class: "nginx"
#       Cert-Manager
#       certmanager.k8s.io/issuer: "letsencrypt-staging"
#       certmanager.k8s.io/acme-challenge-type: http01
    hosts:
      core: "harbor.secpipe.stmpy.me"
      notary: "notary.secpipe.stmpy.me"
externalURL: "https://harbor.secpipe.stmpy.me"
persistence:
  persistentVolumeClaim:
    registry:
      size: 50Gi
```
Install using Helm

```sh
helm install -f values.yaml --name secpipe-lab harbor/harbor
```

## Notes:
- Harbor Homepage: https://goharbor.io
- Docs: https://github.com/goharbor/harbor/tree/master/docs
- Insecure Registry: https://docs.docker.com/registry/insecure/
