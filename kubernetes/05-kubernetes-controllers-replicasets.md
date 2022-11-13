# Controllers and Replica Sets
#replicasets

- Kubernetes controllers monitor kubernetes objects and respond accordingly.
- Controllers are the brain behind kubernetes.

## What is Replication Controller?

Replication controller helps in managing the number of pods based on the specified number.
- If we are running one pod and due to some reason the pod is down, Replication will spawn up a pod instance to make the pod available for users.
- Replication controller also helps in creating multiple pods for sharing load.
- It will also help in scaling up the number of pods based on user traffic.
- If the resources in a node is exhausted replication controller will spawn new pods in a different node.
- So Replication controller can handle load balancing and scaling across different nodes at same time.

## Creating a Replication Controller
- Create a yaml with 4 sections as earlier like apiVersion, kind, metadata, spec
- Add a template section under spec, copy and paste the pod definition used to create pod.
- Copy everything from metadata and align them as per yaml
- add a new parameter `replicas` which is sibling of `template` it will determine the number of pod replicas

```yml
# replication-controller.yml
apiVersion: v1
kind: ReplicationController
metadata:
  name: replication-controller-01
  labels:
    name: sample-replication-controller
    type: front-end
spec:
  template:
    metadata:
      name: nginx
      labels:
        name: nginx
        type: front-end
    spec:
      containers:
        - name: nginx
          image: nginx
  replicas: 3
```

- 3 replicas of nginx will be created.

Command to create this replication controller
```bat
kubectl create -f replication-controller.yml
```

To get details of replication controller use
```sh
kubectl get replicationcontroller
```

## What is replica set
#replicaset
- In the newer version of kubernetes `replicasets`  are used to create replicas
- The `apiVersion` field will have value as `apps/v1`
- `kind` field will have `ReplicaSet` as value
- Other than the `replicas` field we also add `selector` field under which we add the labels that nee to be matched example
```yml
selector:
  matchLabels:
    type: front-end
```

- It will search all pods to see if pod having label field `type` as `front-end`. if the kubernetes finds same number of running pods with the number mentioned as `replicas`, then  kubernetes will not spawn new pods, if they are less then it will spawn up the remaining number of replicas.
- A ReplicaSet definition yml is mentioned below


```yml
# replicaSet.yml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replica-set-01
  labels:
    name: sample-replica-set
    type: front-end
spec:
  template:
    metadata:
      name: nginx
      labels:
        name: nginx
        type: front-end
    spec:
      containers:
        - name: nginx
          image: nginx
  replicas: 3
  selector:
    matchLabels:
      type: front-end
```

Command to create this replication set
```sh
kubectl create -f replicaSet.yml
```

To get list of Replica Sets

```sh
kubectl get replicaset
```

## Scaling Replica Sets
#scale-replicaset

- Update the number of replicas in replica-set definition file and use 
```sh
kubectl replace -f replicaset-definition-file.yml
```

- To update replicas using command line parameter
```sh
kubectl scale --replicas=6 -f replicaset-def-file.yml
```

- To update using the name of replica set
```sh
kubectl scale --replicas=6 replicaset <replicaset-name>

#eample
kubectl scale --replicas=6 replicaset replicaset-definition.yml
```

>[!Info]
> Replica set is the latest supported feature, Replication Controllers are not used extensively anymore.
> 

