- To check list of repositories from now on called as repos the command is 
```sh
helm repo list
```
- To Add a repo
```sh
helm repo add <name> <repo_url>
#example

helm repo add bitnami https://charts.bitnami.com/bitnami
```
- To search for a specific chart in a repo
```sh
helm search repo <chart_you_need>

#Example
helm search repo mysql
```
- To delete a repo
```sh
helm repo remove <repo_name>
```

## Installing an example chart
To install a mysql chart use command 
`helm install <name> <repo/chart_that_need_to_be_installed>`

Example:
`helm install mydb bitnami/mysql` on running the following command you will get below output:
```
NAME: mydb
LAST DEPLOYED: Fri Jun 16 07:31:18 2023
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: mysql
CHART VERSION: 9.10.4
APP VERSION: 8.0.33

** Please be patient while the chart is being deployed **

Tip:

  Watch the deployment status using the command: kubectl get pods -w --namespace default

Services:

  echo Primary: mydb-mysql.default.svc.cluster.local:3306

Execute the following to get the administrator credentials:

  echo Username: root
  MYSQL_ROOT_PASSWORD=$(kubectl get secret --namespace default mydb-mysql -o jsonpath="{.data.mysql-root-password}" | base64 -d)

To connect to your database:

  1. Run a pod that you can use as a client:

      kubectl run mydb-mysql-client --rm --tty -i --restart='Never' --image  docker.io/bitnami/mysql:8.0.33-debian-11-r17 --namespace default --env MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD --command -- bash

  2. To connect to primary service (read/write):

      mysql -h mydb-mysql.default.svc.cluster.local -uroot -p"$MYSQL_ROOT_PASSWORD"
```

- To see the pods created use `kubectl get po`
- The above commands can be used to identify the passwords and create a client to interact with the created pod.

>[!Info] installation name
>While using a name for an installation it should be unique for an installation.