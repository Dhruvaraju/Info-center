We start with pods assuming that the application that need to be deployed is already built and available as an image on docker-hub or any other docker repository. We assume that kubernetes cluster is already setup and working as expected.

## What is a pod
- As explained earlier we deploy the containers into worker nodes.
- But the applications are not directly deployed to worker nodes in kubernetes.
- They are encapsulated in a kubernetes object called pod.
- Pod is a single instance of an application. pod is also the smallest object that can be created in kubernetes.

- Generally pod and application has one to one relation.
- In a single pod we will have only one application container.
- If we want to scale an application will create a new pod in the node.
- If the node capacity is reached a new node is brought up to accommodate new pods.

#### Does the pod contain only one container?
No we can add as many containers as we can based on the capacity of a pod. But we do not add the same application container to the same pod when we have to scale up. We will add only helper containers to the pod.

### How to deploy pods
`kubectl run <application-name> --image <image_name>` this will create a new pod, add the container to the pod and bring it up.
example: `kubectl run nginx --image nginx`
> The image name mentioned should be present in dockerhub else the entire url where the image can be found need to be provided.

`kubectl get pods` to get all pods information.
`kubectl describe pod <pod_name` will provide additional information about the pod
`kubectl get pods -o wide` will provide additional information about pods like internal ip address





