# Defining a pod using kubernetes
#pod #pod-yaml #config

A simple kubernetes pod description for an nginx pod will appear as below:
```yaml
# pod-definition.yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-name
  labels:
    app: myapp
    type: front-end
spec:
  containers:
    - name: nginx-container
      image: nginx
```

To run this configuration and create a pod use command `kubectl create -f pod-definition.yaml`

## significance of each field

- **apiVersion**
	- Specifies the version of kubernetes being used
- **kind**
	- Kind is used to identify the type of component that we are creating in kubernetes. Kind can have the following values Pod, Service, ReplicaSet, Deployment
- **metadata**
	- This is used to specify, information regarding the component, we can specify the ***name*** and labels. ***Labels*** are used to specify key value pairs which in future can be used to classify components.
	- In the above example ***app*** is used to specify the app name which will be present in the pod, ***type*** is used to specify what kind of application is being used in the pod.
- ***spec***
	- This is used to give information regarding the name and image of container
		- name is used for specifying the name of container
		- image is used for specifying name of the image in docker hub or some docker repository.

## Versions that can be specified for different kind

| Kind | Version |
| --- | --- |
| Pod | v1 |
| Service | v1 |
| ReplicaSet | app/v1 |
| Deployment | app/v1 |

`kubectl get pods` to get list of pods
`kubectl describe pod <<your-pod-name>>` is used to get details of a pod name.