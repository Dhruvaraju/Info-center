# Nexus

To bring up a nexus container:

```sh
docker run -d -p 9095:8081 --name nexus sonatype/nexus3
```

Your **admin** user password is located in  
**/nexus-data/admin.password** on the server.

```sh
docker exec -it nexus /bin/bash
```

to get admin password:
```sh
cat nexus-data/admin.password
```