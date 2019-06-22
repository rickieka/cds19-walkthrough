# Private Registry (Harbor)

## Helm

using the helm method to install, if you need helm go [here](https://helm.sh/docs/)

make sure to be on helm `2.14.1` because of [this](https://github.com/helm/helm/issues/5750)

## Cert Installation

setup secret names `harbor-tls`

## Harbor Installation

[Installing via Helm](https://github.com/goharbor/harbor-helm)

```
helm install --set expose.ingress.hosts.core=harbor.secpipe.stmpy.me \
  --set expose.ingress.hosts.notary=notary.secpipe.stmpy.me \
  --set externalURL=https://harbor.secpipe.stmpy.me \
  --set expose.tls.secretName=harbor-tls
  --name lab-harbor harbor/harbor
```


## Notes:
- Homepage: https://goharbor.io
- Docs: https://github.com/goharbor/harbor/tree/master/docs
- Helm Install: https://github.com/goharbor/harbor-helm
