## What is Kubernetes
A container orchestration technology. When your application depends on multiple containers we need to handle how those containers are connected, resources are shared across them. A container orchestration tool helps with that. Few container orchestration tools are Kubernetes, Docker Swarm, MESOS
- Docker swarm is from docker
- Kubernetes is from google
- MESOS is from Apache

## Components in Kubernetes

### Node
Node is a machine physical or virtual, on which kubernetes is installed. Node is a worker machine on which containers are run. Nodes are also called as minions. If a node fails the application running on the node will fail hence we need more number of nodes.

### Cluster
A cluster is set of nodes grouped together. Even if one node fails others will still be serving the application. having multiple nodes will help in load balancing as well.

### Master Node or Controller Node
This is the node which maintains the data regarding the worker nodes and manages them. Master node is responsible for actual orchestration of containers in nodes.

## What do we get when we install Kubernetes in a machine

**API-Server**
This acts as a front-end for kubernetes service. The user, management devices, cli all talk to the api server to interact with kubernetes cluster.

**etcd:**

etcd is a distributed reliable key-value store used by kubernetes to store all data required to manage kubernetes cluster. When we have multiple master nodes and multiple worker nodes, etcd will store the information in a distributed way over all the nodes. It is also responsible to maintain locks between containers to not have any conflicts between clusters.

**Scheduler:**
This is responsible for distributing containers across nodes. It looks for newly created containers and assigns nodes. 

**Controller:**
This is the brain behind orchestration. They are responsible for management when nodes containers or clusters goes down. They are the one to decide if a new container need to be brought up or not.

**Container Runtime:**
Container runtime is the underlying software that is required to run software. Docker is one such software, we have rkt or rocket, CRI-O.

**Kubelet:** 
This is an agent which runs on all nodes. This is responsible for making sure that the containers are running as expected on a node.

## What does master node contain
- Kube api server
- etcd
- controller
- scheduler

## What does worker node contain
- kubelet
- Container runtime

> [!Info]
> Kubelet will connect to api-server to send info regarding the containers in the node.

## kubectl
 
kubectl is a command line utility used  deploy to mange nodes on a kubernetes cluster, to get cluster information, information about other clusters.

`kubectl run` command is used to deploy an application on the cluster. eg: `kubectl run hello-minikube`
`kubectl cluster-info` is used to get the information of a cluster.
`kubectl get nodes` is used to get all the nodes in a cluster.





