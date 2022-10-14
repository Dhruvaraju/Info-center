## Kubectl-command Reference

`kubectl run` command is used to deploy an application on the cluster. eg: `kubectl run hello-minikube`
`kubectl cluster-info` is used to get the information of a cluster.
`kubectl get nodes` is used to get all the nodes in a cluster.
`kubectl run <application-name>` this will create a new pod, add the container to the pod and bring it up.
`kubectl get pods` to get all pods information.
`kubectl describe pod <pod_name` will provide additional information about the pod
`kubectl get pods -o wide` will provide additional information about pods like internal ip address