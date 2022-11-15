# Deployments Update and Rollbacks
#deployment #update #rollback

## What is rollout and versioning
- When will first create  a deployment a rollout will be triggered.
- A new rollout will create a new rollout revision.
- Once in future when we upgrade the image or push a new version a new rollout will be triggered and a new version that is a revision will be created.
- The creation of revisions or versions will help us to keep track of changes and if necessary will help in rolling back to previous version.

Command used to see the status of a rollout:
```sh
kubectl rollout status deployment.apps/<<deployment-name>>
```

Command to see the rollout history and revisions
```sh
kubectl rollout history deployment.apps/<<deployment_name>>
```

## Deployment strategy

There are two deployment strategies:
1)  Recreate
2)  Rolling Update

### Recreate
- All the replicas will be brought down 
- Then All the newly created replicas will be brought up

> Users will have a down time during this type of update Strategy

### Rolling Update
- A new replica is brought up
- An older replica is brought down.
- These steps will be done until all the older replicas are removed.

> Users of the pods will not have any downtime during this type of update.

>[!Info] Default StrategyType
>The default strategy type is `RollingUpdate`

## Making updates for images in deployment
- We can update the deployment definition yaml and use
	```sh
	kubectl apply -f deployment-definition-file.tml
	```
- We can update the image name directly using set image
```sh
kubectl set image deployment/<deployment-name> image-name-given-in-deployment=<Name-of-image-from-docker-hub>

#example
kubectl set image deployment/deployment.yml nginx=nginx:1.8.0
```

We can even see the difference in the deployment strategy when we use deployment describe command.

To rollback to a previous revision of deployment use
```sh
kubectl rollout undo deploymnet/deployment-name
```

Example yml for updating stratergy:


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
  strategy:
    type: Recreate
```
