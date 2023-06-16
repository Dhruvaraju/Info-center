# Installing Helm

Instructions can be found at https://helm.sh/docs/intro/install/
**ubuntu:**

```console
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

Binary downloads of the Helm client can be found on [the Releases page](https://github.com/helm/helm/releases/latest).
Unpack the `helm` binary and add it to your PATH and you are good to go!

If you want to use a package manager:

- [Homebrew](https://brew.sh/) users can use `brew install helm`.
- [Chocolatey](https://chocolatey.org/) users can use `choco install kubernetes-helm`.
- [Scoop](https://scoop.sh/) users can use `scoop install helm`.
- [GoFish](https://gofi.sh/) users can use `gofish install helm`.
- [Snapcraft](https://snapcraft.io/) users can use `snap install helm --classic`

To rapidly get Helm up and running, start with the [Quick Start Guide](https://helm.sh/docs/intro/quickstart/).
See the [installation guide](https://helm.sh/docs/intro/install/) for more options, including installing pre-releases.

## On Windows

- Download binary
- Extract it
- Copy it to a desired location
- Add the path of folder in environment variable path

Use command `helm version` to check the version of helm installed.

> [!Note]
> Use package manager to install helm as upgrading or uninstalling and other environment setup will be easy.

- Helm uses the same config file that kubectl uses to interact with kubernetes
- To change it we can either set `KUBECONFIG` environment variable or change the config in `.kube/config` folder.
- `--debug`: If this is specified, `$HELM_DEBUG` is set to `1`
- `--registry-config`: This is converted to `$HELM_REGISTRY_CONFIG`
- `--repository-cache`: This is converted to `$HELM_REPOSITORY_CACHE`
- `--repository-config`: This is converted to `$HELM_REPOSITORY_CONFIG`
- `--namespace` and `-n`: This is converted to `$HELM_NAMESPACE`
- `--kube-context`: This is converted to `$HELM_KUBECONTEXT`
- `--kubeconfig`: This is converted to `$KUBECONFIG`

> To check perform operations on a specific kubernetes cluster we can pass the kube config file as a reference.
