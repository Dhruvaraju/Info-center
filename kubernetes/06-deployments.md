:# Deployments
#kubernetes_deployments

## Rolling Update

When we deploy applications as pods in production, if we want to upgrade the container image, we have to stop all the pods and update them, during which users of the pod will have down time. So instead of bringing down all pods we can updated individual pod and let other pods continue working. This is called as rolling update.

In production Environment we might need few more features as well which are listed below.

- If the update fails due to some reason we should be able to **rollback** the changes those are made in rolling update as well.
- We should be able to pause the rolling out of changes and resume it as well.

# What is Deployment?

Deployment is a kubernetes object which is over replica-set in hierarchy, which provides capabilities as mentioned below on under laying objects such as: pods, replica sets.
- Rolling Update
- Rollback Changes
- Pause and resume changes 

## How to create deployment definition 

- Deployment definition looks same as a replica-set definition, except for attribute kind
- We will add `Deployment` for value of `kind` instead of `ReplicaSet`
- Example Deployment definition file

```yml
# deployment-def.yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment
  labels:
    name: sample-deployments
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

Command used to create the deployment
```sh
kubectl create -f deployment-def.yml
```

To get list of deployment
```yml
kubectl get deployments
```

Below deployments, replica-sets are created. Pods are created based on the number of replicas requested.

To get information about everything like deployment, replica-sets, pods use
```sh
kubectl get all
```