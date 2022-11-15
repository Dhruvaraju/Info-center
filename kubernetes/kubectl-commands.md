## Kubectl-command Reference

- `kubectl run` command is used to deploy an application on the cluster. eg: `kubectl run hello-minikube`
- `kubectl cluster-info` is used to get the information of a cluster.
- `kubectl get nodes` is used to get all the nodes in a cluster.
- `kubectl run <application-name>` this will create a new pod, add the container to the pod and bring it up.
- `kubectl get pods` to get all pods information.
- `kubectl describe pod <pod_name` will provide additional information about the pod
- `kubectl get pods -o wide` will provide additional information about pods like internal ip address
-  `kubectl create -f pod-definition.yaml` To start a pod using configuration file
- We can also use `kubectl apply -f pod-definition.yaml` to get the same result as `create`.
- `kubectl get pods` to get list of pods
- `kubectl describe pod <<your-pod-name>>` is used to get details of a pod name.
- `kubectl delete pod <pod_name>` delete the provided pod name

- Command to create this replication controller
```
kubectl create -f replication-controller.yml
# replication-controller.yml is the file which contains replication contoller configuration
```

- To get details of replication controller use
```
kubectl get replicationcontroller
```

Command to create this replication set
#replicaset
```sh
kubectl create -f replicaSet.yml
```

To get list of Replica Sets
#get-replicasets

```sh
kubectl get replicaset
```

 Update the number of replicas in replica-set definition file and use 
 #replace
```sh
kubectl replace -f replicaset-definition-file.yml
```

To update replicas using command line parameter
#scale #replicas
```sh
kubectl scale --replicas=6 -f replicaset-def-file.yml
```

To update using the name of replica set
```sh
kubectl scale --replicas=6 replicaset <replicaset-name>

#eample
kubectl scale --replicas=6 replicaset replicaset-definition.yml
```

To delete a replica set use below
#delete-replicaset
```sh
kubectl delete replicaset <replicaset-name>
```
 > This will delete all underlying pods
 
To edit a running configuration of a replica-set use

```sh
kubectl edit replicaset <replicaset-name>
# This will update the running configuration no the real file which we used
```

Command used to see the status of a rollout:  
#rollout-status
```sh
kubectl rollout status deployment.apps/<<deployment-name>>
```

Command to see the rollout history and revisions 
#rollout-history
```sh
kubectl rollout history deployment.apps/<<deployment_name>>
```

We can update the deployment definition yaml and use 
#deployment-update

```sh
kubectl apply -f deployment-definition-file.tml
```

 We can update the image name directly using set image 
 #set-image
```sh
kubectl set image deployment/<deployment-name> image-name-given-in-deployment=<Name-of-image-from-docker-hub>

#example
kubectl set image deployment/deployment.yml nginx=nginx:1.8.0
```

To rollback to a previous revision of deployment use 
#rollback
```sh
kubectl rollout undo deploymnet/deployment-name
```