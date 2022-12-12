# Namespace

In Kubernetes, _namespaces_ provides a mechanism for isolating groups of resources within a single cluster. Names of resources need to be unique within a namespace, but not across namespaces. Namespace-based scoping is applicable only for namespaced objects _(e.g. Deployments, Services, etc)_ and not for cluster-wide objects _(e.g. StorageClass, Nodes, PersistentVolumes, etc)_.

## When to Use Multiple Namespaces[](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#when-to-use-multiple-namespaces)

Namespaces are intended for use in environments with many users spread across multiple teams, or projects. For clusters with a few to tens of users, you should not need to create or think about namespaces at all. Start using namespaces when you need the features they provide.

Namespaces provide a scope for names. Names of resources need to be unique within a namespace, but not across namespaces. Namespaces cannot be nested inside one another and each Kubernetes resource can only be in one namespace.

Namespaces are a way to divide cluster resources between multiple users (via [resource quota](https://kubernetes.io/docs/concepts/policy/resource-quotas/)).

It is not necessary to use multiple namespaces to separate slightly different resources, such as different versions of the same software: use [labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels) to distinguish resources within the same namespace.

**Note:** For a production cluster, consider _not_ using the `default` namespace. Instead, make other namespaces and use those.

## Initial namespaces[](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)

Kubernetes starts with four initial namespaces:

`default`

Kubernetes includes this namespace so that you can start using your new cluster without first creating a namespace.

`kube-node-lease`

This namespace holds [Lease](https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/lease-v1/) objects associated with each node. Node leases allow the kubelet to send [heartbeats](https://kubernetes.io/docs/concepts/architecture/nodes/#heartbeats) so that the control plane can detect node failure.

`kube-public`

This namespace is readable by _all_ clients (including those not authenticated). This namespace is mostly reserved for cluster usage, in case that some resources should be visible and readable publicly throughout the whole cluster. The public aspect of this namespace is only a convention, not a requirement.

`kube-system`

The namespace for objects created by the Kubernetes system.

## Working with Namespaces[](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#working-with-namespaces)

Creation and deletion of namespaces are described in the [Admin Guide documentation for namespaces](https://kubernetes.io/docs/tasks/administer-cluster/namespaces).

**Note:** Avoid creating namespaces with the prefix `kube-`, since it is reserved for Kubernetes system namespaces.

### Viewing namespaces[](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#viewing-namespaces)

You can list the current namespaces in a cluster using:

```shell
kubectl get namespace
```

```
NAME              STATUS   AGE
default           Active   1d
kube-node-lease   Active   1d
kube-public       Active   1d
kube-system       Active   1d
```

### Setting the namespace for a request[](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#setting-the-namespace-for-a-request)

To set the namespace for a current request, use the `--namespace` flag.

For example:

```shell
kubectl run nginx --image=nginx --namespace=<insert-namespace-name-here>
kubectl get pods --namespace=<insert-namespace-name-here>
```

### Setting the namespace preference[](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#setting-the-namespace-preference)

You can permanently save the namespace for all subsequent kubectl commands in that context.

```shell
kubectl config set-context --current --namespace=<insert-namespace-name-here>
# Validate it
kubectl config view --minify | grep namespace:
```

## Namespaces and DNS[](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#namespaces-and-dns)

When you create a [Service](https://kubernetes.io/docs/concepts/services-networking/service/), it creates a corresponding [DNS entry](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/). This entry is of the form `<service-name>.<namespace-name>.svc.cluster.local`, which means that if a container only uses `<service-name>`, it will resolve to the service which is local to a namespace. This is useful for using the same configuration across multiple namespaces such as Development, Staging and Production. If you want to reach across namespaces, you need to use the fully qualified domain name (FQDN).

As a result, all namespace names must be valid [RFC 1123 DNS labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#dns-label-names).

**Warning:**

By creating namespaces with the same name as [public top-level domains](https://data.iana.org/TLD/tlds-alpha-by-domain.txt), Services in these namespaces can have short DNS names that overlap with public DNS records. Workloads from any namespace performing a DNS lookup without a [trailing dot](https://datatracker.ietf.org/doc/html/rfc1034#page-8) will be redirected to those services, taking precedence over public DNS.

To mitigate this, limit privileges for creating namespaces to trusted users. If required, you could additionally configure third-party security controls, such as [admission webhooks](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/), to block creating any namespace with the name of [public TLDs](https://data.iana.org/TLD/tlds-alpha-by-domain.txt).

## Not all objects are in a namespace[](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#not-all-objects-are-in-a-namespace)

Most Kubernetes resources (e.g. pods, services, replication controllers, and others) are in some namespaces. However namespace resources are not themselves in a namespace. And low-level resources, such as [nodes](https://kubernetes.io/docs/concepts/architecture/nodes/) and [persistentVolumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/), are not in any namespace.

To see which Kubernetes resources are and aren't in a namespace:

```shell
# In a namespace
kubectl api-resources --namespaced=true

# Not in a namespace
kubectl api-resources --namespaced=false
```

## Automatic labelling[](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#automatic-labelling)

**FEATURE STATE:** `Kubernetes 1.21 [beta]`

The Kubernetes control plane sets an immutable [label](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels) `kubernetes.io/metadata.name` on all namespaces, provided that the `NamespaceDefaultLabelName` [feature gate](https://kubernetes.io/docs/reference/command-line-tools-reference/feature-gates/) is enabled. The value of the label is the namespace name.

## Creating a new namespace[](https://kubernetes.io/docs/tasks/administer-cluster/namespaces/#creating-a-new-namespace)

**Note:** Avoid creating namespace with prefix `kube-`, since it is reserved for Kubernetes system namespaces.

1.  Create a new YAML file called `my-namespace.yaml` with the contents:
    
    ```yaml
    apiVersion: v1
    kind: Namespace
    metadata:
      name: <insert-namespace-name-here>
    ```
    
    Then run:
    
    ```
    kubectl create -f ./my-namespace.yaml
    ```
    
2.  Alternatively, you can create namespace using below command:
    
    ```
    kubectl create namespace <insert-namespace-name-here>
    ```
    

The name of your namespace must be a valid [DNS label](https://kubernetes.io/docs/concepts/overview/working-with-objects/names#dns-label-names).

There's an optional field `finalizers`, which allows observables to purge resources whenever the namespace is deleted. Keep in mind that if you specify a nonexistent finalizer, the namespace will be created but will get stuck in the `Terminating` state if the user tries to delete it.

More information on `finalizers` can be found in the namespace [design doc](https://git.k8s.io/design-proposals-archive/architecture/namespaces.md#finalizers).

## Deleting a namespace[](https://kubernetes.io/docs/tasks/administer-cluster/namespaces/#deleting-a-namespace)

Delete a namespace with

```shell
kubectl delete namespaces <insert-some-namespace-name>
```

**Warning:** This deletes _everything_ under the namespace!

This delete is asynchronous, so for a time you will see the namespace in the `Terminating` state.

## Subdividing your cluster using Kubernetes namespaces[](https://kubernetes.io/docs/tasks/administer-cluster/namespaces/#subdividing-your-cluster-using-kubernetes-namespaces)

1.  Understand the default namespace
    
    By default, a Kubernetes cluster will instantiate a default namespace when provisioning the cluster to hold the default set of Pods, Services, and Deployments used by the cluster.
    
    Assuming you have a fresh cluster, you can introspect the available namespaces by doing the following:
    
    ```shell
    kubectl get namespaces
    ```
    
    ```
    NAME      STATUS    AGE
    default   Active    13m
    ```
    
2.  Create new namespaces
    
    For this exercise, we will create two additional Kubernetes namespaces to hold our content.
    
    In a scenario where an organization is using a shared Kubernetes cluster for development and production use cases:
    
    The development team would like to maintain a space in the cluster where they can get a view on the list of Pods, Services, and Deployments they use to build and run their application. In this space, Kubernetes resources come and go, and the restrictions on who can or cannot modify resources are relaxed to enable agile development.
    
    The operations team would like to maintain a space in the cluster where they can enforce strict procedures on who can or cannot manipulate the set of Pods, Services, and Deployments that run the production site.
    
    One pattern this organization could follow is to partition the Kubernetes cluster into two namespaces: `development` and `production`.
    
    Let's create two new namespaces to hold our work.
    
    Create the `development` namespace using kubectl:
    
    ```shell
    kubectl create -f https://k8s.io/examples/admin/namespace-dev.json
    ```
    
    And then let's create the `production` namespace using kubectl:
    
    ```shell
    kubectl create -f https://k8s.io/examples/admin/namespace-prod.json
    ```
    
    To be sure things are right, list all of the namespaces in our cluster.
    
    ```shell
    kubectl get namespaces --show-labels
    ```
    
    ```
    NAME          STATUS    AGE       LABELS
    default       Active    32m       <none>
    development   Active    29s       name=development
    production    Active    23s       name=production
    ```
    
3.  Create pods in each namespace
    
    A Kubernetes namespace provides the scope for Pods, Services, and Deployments in the cluster.
    
    Users interacting with one namespace do not see the content in another namespace.
    
    To demonstrate this, let's spin up a simple Deployment and Pods in the `development` namespace.
    
    ```shell
    kubectl create deployment snowflake --image=registry.k8s.io/serve_hostname  -n=development --replicas=2
    ```
    
    We have created a deployment whose replica size is 2 that is running the pod called `snowflake` with a basic container that serves the hostname.
    
    ```shell
    kubectl get deployment -n=development
    ```
    
    ```
    NAME         READY   UP-TO-DATE   AVAILABLE   AGE
    snowflake    2/2     2            2           2m
    ```
    
    ```shell
    kubectl get pods -l app=snowflake -n=development
    ```
    
    ```
    NAME                         READY     STATUS    RESTARTS   AGE
    snowflake-3968820950-9dgr8   1/1       Running   0          2m
    snowflake-3968820950-vgc4n   1/1       Running   0          2m
    ```
    
    And this is great, developers are able to do what they want, and they do not have to worry about affecting content in the `production` namespace.
    
    Let's switch to the `production` namespace and show how resources in one namespace are hidden from the other.
    
    The `production` namespace should be empty, and the following commands should return nothing.
    
    ```shell
    kubectl get deployment -n=production
    kubectl get pods -n=production
    ```
    
    Production likes to run cattle, so let's create some cattle pods.
    
    ```shell
    kubectl create deployment cattle --image=registry.k8s.io/serve_hostname -n=production
    kubectl scale deployment cattle --replicas=5 -n=production
    
    kubectl get deployment -n=production
    ```
    
    ```
    NAME         READY   UP-TO-DATE   AVAILABLE   AGE
    cattle       5/5     5            5           10s
    ```
    
    ```shell
    kubectl get pods -l app=cattle -n=production
    ```
    
    ```
    NAME                      READY     STATUS    RESTARTS   AGE
    cattle-2263376956-41xy6   1/1       Running   0          34s
    cattle-2263376956-kw466   1/1       Running   0          34s
    cattle-2263376956-n4v97   1/1       Running   0          34s
    cattle-2263376956-p5p3i   1/1       Running   0          34s
    cattle-2263376956-sxpth   1/1       Running   0          34s
    ```
    

At this point, it should be clear that the resources users create in one namespace are hidden from the other namespace.

As the policy support in Kubernetes evolves, we will extend this scenario to show how you can provide different authorization rules for each namespace.

## Understanding the motivation for using namespaces[](https://kubernetes.io/docs/tasks/administer-cluster/namespaces/#understanding-the-motivation-for-using-namespaces)

A single cluster should be able to satisfy the needs of multiple users or groups of users (henceforth a 'user community').

Kubernetes _namespaces_ help different projects, teams, or customers to share a Kubernetes cluster.

It does this by providing the following:

1.  A scope for [Names](https://kubernetes.io/docs/concepts/overview/working-with-objects/names/).
2.  A mechanism to attach authorization and policy to a subsection of the cluster.

Use of multiple namespaces is optional.

Each user community wants to be able to work in isolation from other communities.

Each user community has its own:

1.  resources (pods, services, replication controllers, etc.)
2.  policies (who can or cannot perform actions in their community)
3.  constraints (this community is allowed this much quota, etc.)

A cluster operator may create a Namespace for each unique user community.

The Namespace provides a unique scope for:

1.  named resources (to avoid basic naming collisions)
2.  delegated management authority to trusted users
3.  ability to limit community resource consumption

Use cases include:

1.  As a cluster operator, I want to support multiple user communities on a single cluster.
2.  As a cluster operator, I want to delegate authority to partitions of the cluster to trusted users in those communities.
3.  As a cluster operator, I want to limit the amount of resources each community can consume in order to limit the impact to other communities using the cluster.
4.  As a cluster user, I want to interact with resources that are pertinent to my user community in isolation of what other user communities are doing on the cluster.