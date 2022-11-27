# What are service

- Kubernetes services will enable communication between components and external.
- Services help in connecting applications with other applications are users.

Consider having few pods in a cluster, one delivering frontend, others delivering backend and database services. Service helps users to connect with frontend. Service helps frontend to connect with backend. Service also helps backend with database. Hence it helps in loosely coupling.

## Types of Service?

- [ ] NodePort
- [ ] ClusterIp
- [ ] LoadBalancer

###  NodePort

A nodeport service will map, a port on node to a port on  a pod, so a pod can be accessed by using a port on the node. 

- But a service is considered as a component by itself.
- Hence service has its own port.
- So there are 3 ports involved.
- a port on Node also know as Nodeport will be mapped to a port on service port and then it will be mapped to a port on Pod

**TargetPort:**  Port on Pod is called a target port.
**Port:** port number on service is called as a port.
**NodePort:** Port on node is called nodeport.

Definition for a service port:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: NodePort
  ports:
    - targetPort: 80
      port: 80
      nodePort: 30008
  selector:
    app: myapp
    type: front-end
```

> Nodeport will vary from 30000 to 32767

Command to create a service `kubectl create -f service-definition.yml`
To get information about service:
```sh
kubectl get services
# Or we can also use
kubectl get svc
```

Whether it is a multiple pods on a single node or a multiple pods on multiple nodes, service is created in the same way. Service selects the pods using the selector attribute of service definition which matches the metadata labels of the pod. Hence no additional configuration is required.


###  ClusterIp

In a multi tier application we have few pods running front-end and few pods running back-end, few pods running database services.

With help of a cluster ip service we can club all those pods to a service and expose them to other pods, similarly we can club all the databases and create a service for them.

A ClusterIP service definition looks something similar to this.
```yml
apiVersion: v1
kind: Service
metadata:
  name: back-end
spec:
  type: ClusterIp
  ports:
    - targetPort: 80
      port: 80
  selector:
    name: my-database
    type: back-end
```

Creating service:  `kubectl create -f clusterip-service-definition.ynl`
To get service: `kubectl get services`

### LoadBalancer

This type of service is similar to the node port service but it will extract the load balancing capability of an underlying cloud service.

This type of service is mainly useful with a supported cloud provider which supports load balancing service. But using this kind of service on an unsupported platform will simply make the implementation on node port.


```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: LoadBalancer
  ports:
    - targetPort: 80
      port: 80
      nodePort: 30008
  selector:
    app: myapp
    type: front-end
```

When we have multiple front-end facing apps, we will be hosting them from different ip addresses, but an end user expects it to be a domain address like google.com or some other domain. An external load balancer will take the domain address and map it to multiple pods on which the front-end facing app is running. This the reason for using an external load balancer.