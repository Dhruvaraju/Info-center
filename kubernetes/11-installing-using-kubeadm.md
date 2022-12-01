# Installing kubernetes cluster with kubeadm

Reference:
Oracle VirtualBox:  [https://www.virtualbox.org/](https://www.virtualbox.org/)
Vagrant: [https://www.vagrantup.com/](https://www.vagrantup.com/)
Link to download VM images: [http://osboxes.org/](http://osboxes.org/)
Link to kubeadm installation instructions: [https://kubernetes.io/docs/setup/independent/install-kubeadm/](https://kubernetes.io/docs/setup/independent/install-kubeadm/)
The link to Vagrant file:  
[https://github.com/kodekloudhub/certified-kubernetes-administrator-course](https://github.com/kodekloudhub/certified-kubernetes-administrator-course)  
If you are new to VirtualBox or Vagrant, please follow this pre-requisites course to learn about it: [https://www.youtube.com/watch?v=Wvf0mBNGjXY](https://www.youtube.com/watch?v=Wvf0mBNGjXY)

## Steps Required in installing Kubernetes

- [ ] Add multiple virtual machines
- [ ] Designate one as master and others as worker
- [ ] Install container runtime on all nodes, here it is docker
- [ ] Install kubeadm on all nodes
- [ ] Initialize the master node, all the required components will be install in this step.
- [ ] Create a pod network
- [ ] Join worker nodes to master node

## What are required on which nodes
### Master node
- kube-apiserver
- etcd
- node-controller
- replica-controller
- Container Runtime

### Worker Node:
- Kubelet
- Container Runtime

https://github.com/mmumshad/kubernetes-the-hard-way