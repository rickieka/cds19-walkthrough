# Configure Kubernetes to use private registry

Kubernetes has [docs on how to do this](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)

I prefer the first method - using an existing docker config file, but first you have to create it

```sh
# save current config to put back later
$ mv ~/.docker/config.json ~/.docker/config.json.bak
docker login harbor.secpipe.stmpy.me
Username: [ROBOT_USERNAME]
Password: [ROBOT_PASSWORD]
WARNING! Your password will be stored unencrypted in /home/stmpy/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded 
```

the resulting `~/.docker/config.json` file should contain something like this

```json
{
    "auths": {
        "harbor2.secpipe.stmpy.me": {
            "auth": "[SORT_OF_ENCODED_PASSWORD]"
        }
    }
}
```

we will now use this to create the secret in kubernetes

```sh
kubectl create secret generic harbor-creds \
    --from-file .dockerconfigjson=$HOME/.docker/config.json \
    --type kubernetes.io/dockerconfigjson
```

We can now inspect the secret and see that it contains our auth from the docker config file

```sh
kubectl get secret harbor-creds -o "jsonpath={.data.\.dockerconfigjson}" | base64 --decode
```

Now that is done, we can restore our previous config file

```sh
mv ~/.docker/config.json.bak ~/.docker/config.json
```

## NOTES:
- https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/
