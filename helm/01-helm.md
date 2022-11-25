# What is helm?
#helm

- Helm is a package manager for kubernetes.
- Like we have npm for managing node packages, Helm is used for kubernetes.
- We can use helm to
	- Install kubernetes objects
	- Uninstall 
	- Upgrade 
	- Rollback

>[!Info]
> Helm configuration files are called as charts and they fetched from a chart repo.
> Repo can be a public or private hosted repo.

Helm will get the charts from repo and submit them as kubernetes object yaml to kubernetes api.

## Example Helm commands:

Helm Install:
```sh
helm install apache bitnami/apache --namespace=mynamespace
```

Helm upgrade:
```sh
helm upgrade apache bitnami/apache --namespace=mynamespace
```

Helm rollback:
```sh
helm rollback apache 1 --namespace=mynamespace
```

Helm Install:
```sh
helm uninstall apache 
```

## Why should we use Helm?

- Helm is simple and easy to use, we can get predefined charts for popular applications like  mongodb, mysql.
- Helm provides revision history for charts.
	- All the kubernetes object(Deployment, Config-Map, Service, Ingress) templates are managed by revisions
- Dynamic Configurations can be provided with helm.
- Consistency 
- Intelligent Deployments (Helm understands the order in which we have to deploy objects)
- Life Cycle Hooks:
	- Helm provides lifecycle hooks, through which we can perform additional tasks on kubernetes.
- Security: Helm makes sure that the charts that are downloaded from repo signed with a hash and checks if they are genuinely from the repo and not being hampered with in the middle.

## What are charts and repos

### Chart 

Set of configuration files which are used to install an application on kubernetes cluster using helm.

### Repo

Repo is a place where the charts reside, we have to get a chart from repo when we install some application. Bitnami is one such repo, there are many public hosted repos for helm charts.
[Bitnami Helm Repos](https://bitnami.com/stacks/helm)
[Artifact Hub](https://artifacthub.io/)



