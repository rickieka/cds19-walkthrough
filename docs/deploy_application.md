# Deploy demo application

## Kubernetes deployment manifest

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: boolio-app
  labels:
    app: boolio-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: boolio-app
  template:
    metadata:
      labels:
        app: boolio-app
    spec:
      containers:
      - name: boolio-app
        image: harbor.secpipe.stmpy.me/[HARBOR_PROJECT]/boolio-app
        ports:
        - containerPort: 3000
      imagePullSecrets:
        - name: harbor-creds
```

## Notes:
- https://kubernetes.io/docs/concepts/workloads/controllers/deployment/