# Create kubernetes environment

## Create Namespace inside lab environment

__Everyone should use the link provided by the instructor from gethandouts to create their own namespace__

![Create Lab Environment](images/create_lab_environment.png)

Afterwards you should get a page with a kubernetes configuration file, copy the contents of the config file and put them in a file at `~/.kube/config`

![Lab Environment Configuration](images/lab_environment_configuration.png)

### Configure multiple config files
**-- IF you already have a `~/.kube/config` file and don't want to mess with it there are ways around that :-)**

`kubectl` allows context switching, so it is possible to combine multiple configurations together, and switch between them.

#### Option 1: Temporarily change `$KUBECONFIG` in your shell
`kubectl` ultimately will use an environment variable `$KUBECONFIG` when looking for configurations, if you export this variable in your shell, you'll use the lab configuration for the duration of your shell session.

```bash
export KUBECONFIG="/path/to/lab/config/file"
# /path/to/lab/config/file can be anywhere, even in your home directory, or downloads, just make sure if you don't use absolute pathing to stay in the same directory as the config file
```

#### Option 2: Smash everything together in 1 file
The yaml file allows for muliple items to exist for the `cluster`, `context`, and `user` you can just copy those parts over from the lab config into your `~/.kube/config` file. e.g. ...

```yaml
# ...
# Multiple Clusters
clusters:
- cluster:
    certificat-authority-data: <REDACTED_CERT_DATA>
    server: <REDACTED_SERVER_ADDRESS>
  name: my-work-cluster
    
- cluster:
    certificate-authority-data: <REDACTED_CERT_DATA>
    server: <REDACTED_SERVER_ADDRESS>
  name: lab-environment-security-pipe-travis


# Multiple Contexts
contexts:
- context:
    cluster: my-work-cluster
    namespace: default
    user: my-creds-for-work
  name: work-cluster

- context:
    cluster: lab-environment-security-pipe-travis
    namespace: security-pipe-travis
    user: lab-environment-security-pipe-travis-default
  name: lab-environment

# Multiple users
users:
- user:
    client-certificate-data: <REDACTED_CERT>
    client-key-data: <REDACTED_DATA>
  name: my-creds-for-work

- user:
    token: <REDACTED_ACCOUNT_TOKEN>
  name: lab-environment-security-pipe-travis-default
```

#### Option 3: My favorite, drop all configs in a folder

This is probably the most complex option, but once it's done you never have to touch it again, and you can add contexts (clusters) by just dropping their config files into a single directory

The way I go about doing this is by creating a new directory `mkdir ~/.kube/configs/` then adding the following snippet to my shell `.rc` file, I use ZSH, so in `~/.zshrc`, or for bash `~/.bashrc` ... etc ...

```bash
if [ -d "$HOME/.kube/configs" ]; then

  _configs=""

  for f in $HOME/.kube/configs/*
  do
    _configs="$f:$_configs"
  done
  export KUBECONFIG="$_configs"
fi
```

#### Option 4: Find one you like

Kubernetes has a page completely about [this topic](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/) they also explain how to do the same with windows, which I'm not so familiar with

## Checking cluster access and permissions

At this point, we should be able to use our config file to access our kubernetes clusters.

```bash
$ kubectl get pods
No resources found.
```

If you type the above, and see the same result then GREAT!!! we're good to go

[Back](README.md)
