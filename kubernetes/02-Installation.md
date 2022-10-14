## Installing kubectl and minikube
We can find installation instructions under https://kubernetes.io. Under tasks we can see a location for installation.

To install kubectl on windows goto: https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

### Install kubectl binary with curl on Windows[](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/#install-kubectl-binary-with-curl-on-windows)

1.  Download the [latest release v1.25.0](https://dl.k8s.io/release/v1.25.0/bin/windows/amd64/kubectl.exe).
    
    Or if you have `curl` installed, use this command:
    
    ```powershell
    curl -LO "https://dl.k8s.io/release/v1.25.0/bin/windows/amd64/kubectl.exe"
    ```
    
    **Note:** To find out the latest stable version (for example, for scripting), take a look at [https://dl.k8s.io/release/stable.txt](https://dl.k8s.io/release/stable.txt).
    
2.  Validate the binary (optional)
    
    Download the `kubectl` checksum file:
    
    ```powershell
    curl -LO "https://dl.k8s.io/v1.25.0/bin/windows/amd64/kubectl.exe.sha256"
    ```
    
    Validate the `kubectl` binary against the checksum file:
    
    -   Using Command Prompt to manually compare `CertUtil`'s output to the checksum file downloaded:
        
        ```cmd
        CertUtil -hashfile kubectl.exe SHA256
        type kubectl.exe.sha256
        ```
        
    -   Using PowerShell to automate the verification using the `-eq` operator to get a `True` or `False` result:
        
        ```powershell
        $($(CertUtil -hashfile .\kubectl.exe SHA256)[1] -replace " ", "") -eq $(type .\kubectl.exe.sha256)
        ```
        
3.  Append or prepend the `kubectl` binary folder to your `PATH` environment variable.
    
4.  Test to ensure the version of `kubectl` is the same as downloaded:
    
    ```cmd
    kubectl version --client
    ```
    
    Or use this for detailed view of version:
    
    ```cmd
    kubectl version --client --output=yaml
    ```
    

**Note:** [Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/#kubernetes) adds its own version of `kubectl` to `PATH`. If you have installed Docker Desktop before, you may need to place your `PATH` entry before the one added by the Docker Desktop installer or remove the Docker Desktop's `kubectl`.


## Installing Minikube
Installation instructions available at https://minikube.sigs.k8s.io/docs/start/
After install add the minikube path to environment variables `path` variable. 

To start minikube use `minikube start` first time it will give some output as below and might take sometime to complete.

```
😄  minikube v1.27.1 on Microsoft Windows 10 Pro 10.0.19044 Build 19044
✨  Automatically selected the docker driver
📌  Using Docker Desktop driver with root privileges
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
💾  Downloading Kubernetes v1.25.2 preload ...
    > preloaded-images-k8s-v18-v1...:  385.41 MiB / 385.41 MiB  100.00% 13.33 M
    > gcr.io/k8s-minikube/kicbase:  387.11 MiB / 387.11 MiB  100.00% 7.59 MiB p
    > gcr.io/k8s-minikube/kicbase:  0 B [________________________] ?% ? p/s 31s
🔥  Creating docker container (CPUs=2, Memory=6100MB) ...
🐳  Preparing Kubernetes v1.25.2 on Docker 20.10.18 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

```

## Interact with your cluster

If you already have kubectl installed, you can now use it to access your shiny new cluster:

```shell
kubectl get po -A
```

Alternatively, minikube can download the appropriate version of kubectl and you should be able to use it like this:

```shell
minikube kubectl -- get po -A
```

You can also make your life easier by adding the following to your shell config:

```shell
alias kubectl="minikube kubectl --"
```

Initially, some services such as the storage-provisioner, may not yet be in a Running state. This is a normal condition during cluster bring-up, and will resolve itself momentarily. For additional insight into your cluster state, minikube bundles the Kubernetes Dashboard, allowing you to get easily acclimated to your new environment:

```shell
minikube dashboard
```

## **4**Deploy applications

Create a sample deployment and expose it on port 80:

```shell
kubectl create deployment hello-minikube --image=docker.io/nginx:1.23
kubectl expose deployment hello-minikube --type=NodePort --port=80
```

It may take a moment, but your deployment will soon show up when you run:

```shell
kubectl get services hello-minikube
```

The easiest way to access this service is to let minikube launch a web browser for you:

```shell
minikube service hello-minikube
```

Alternatively, use kubectl to forward the port:

```shell
kubectl port-forward service/hello-minikube 7080:80
```

Tada! Your application is now available at [http://localhost:7080/](http://localhost:7080/).

You should be able to see the request metadata from nginx such as the `CLIENT VALUES`, `SERVER VALUES`, `HEADERS RECEIVED` and the `BODY` in the application output. Try changing the path of the request and observe the changes in the `CLIENT VALUES`. Similarly, you can do a POST request to the same and observe the body show up in `BODY` section of the output.

### LoadBalancer deployments[](https://minikube.sigs.k8s.io/docs/start/#loadbalancer-deployments)

To access a LoadBalancer deployment, use the “minikube tunnel” command. Here is an example deployment:

```shell
kubectl create deployment balanced --image=docker.io/nginx:1.23
kubectl expose deployment balanced --type=LoadBalancer --port=80
```

In another window, start the tunnel to create a routable IP for the ‘balanced’ deployment:

```shell
minikube tunnel
```

To find the routable IP, run this command and examine the `EXTERNAL-IP` column:

```shell
kubectl get services balanced
```

Your deployment is now available at <EXTERNAL-IP>:80

## **5**Manage your cluster

Pause Kubernetes without impacting deployed applications:

```shell
minikube pause
```

Unpause a paused instance:

```shell
minikube unpause
```

Halt the cluster:

```shell
minikube stop
```

Change the default memory limit (requires a restart):

```shell
minikube config set memory 9001
```

Browse the catalog of easily installed Kubernetes services:

```shell
minikube addons list
```

Create a second cluster running an older Kubernetes release:

```shell
minikube start -p aged --kubernetes-version=v1.16.1
```

Delete all of the minikube clusters:

```shell
minikube delete --all
```