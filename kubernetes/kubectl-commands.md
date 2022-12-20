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

To get information about service: #service #svc
```sh
kubectl get services
# Or we can also use
kubectl get svc
```

Formatting output

The default output format for all **kubectl** commands is the human-readable plain-text format.
The -o flag allows us to output the details in several different formats.  

**kubectl [command] [TYPE] [NAME] -o <output_format>**

Here are some of the commonly used formats:

1.  `-o json`Output a JSON formatted API object.
2.  `-o name`Print only the resource name and nothing else. 
3.  `-o wide`Output in the plain-text format with any additional information. 
4.  `-o yaml`Output a YAML formatted API object.

Here are some useful examples:

-   **Output with JSON format:**
master $ kubectl create namespace test-123 --dry-run -o json

``` 
{
      "kind": "Namespace",
      "apiVersion": "v1",
     "metadata": {
          "name": "test-123",
          "creationTimestamp": null
      },
      "spec": {},
      "status": {}
  }
 master $
```

  

-   **Output with YAML format:**
    

1.  master $ kubectl create namespace test-123 --dry-run -o yaml
2.  apiVersion: v1
3.  kind: Namespace
4.  metadata:
5.    creationTimestamp: null
6.    name: test-123
7.  spec: {}
8.  status: {}

  

-   **Output with wide (additional details):**
    

Probably the most common format used to print additional details about the object:
```
  master $ kubectl get pods -o wide NAME      READY   STATUS    RESTARTS   AGE     IP          NODE    NOMINATED NODE   READINESSGATES
busybox   1/1     Running   0          3m39s   10.36.0.2   node01   <none>           <none>
ningx     1/1     Running   0          7m32s   10.44.0.1   node03   <none>           <none>
redis     1/1     Running   0          3m59s   10.36.0.1   node01   <none>           <none>
master $
```
  

For more details, refer:

[**https://kubernetes.io/docs/reference/kubectl/overview/**](https://kubernetes.io/docs/reference/kubectl/overview/)

[**https://kubernetes.io/docs/reference/kubectl/cheatsheet**](https://kubernetes.io/docs/reference/kubectl/cheatsheet)**/**

- Use `--dry-run=client` to check a command with out creating it.
- Use `-o  yaml` to get the definition files displayed on screen
example: 

```sh
kubectl run nginx --image=nginx --dry-run=client -o yaml
```

