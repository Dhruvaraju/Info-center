- Every node machine we have to install container runtime 
- On a worker node kubelet  agent will run & kube-proxy
- Kube Api server is component of kubernetes control plane
- Kube-api-server will scale horizontally
- ETCD is a key value database
- Logical Volume Manager LVM

To get Namespace
```sh
kubectl get ns
```

Default is a default name space.
Arch components are present in system namespace

```
kubectl get pod -n kube-system
```

Pod-network need to be installed additionally.

```
kubectl get service
```

ls -l  /etc/yum.repos.d

yum-config-manager --add-repo

To explain about a kubernetes object
```
kubectl explain <<kubernetes_object>>
```

### Kubernetes job
A one time run object, which will check if deployment of specified number for pods are successful or not. A job's final status is completed.