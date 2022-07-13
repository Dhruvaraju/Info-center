## Installing Gitlab
#install-gitlab

We cans start a git lab container either an enterprise version or community version
community version: `docker pull gitlab/gitlab-ce`
Enterprise Version: `docker pull gitlab/gitlab-ee`

Exposing gitlab urls:

```commandline
docker run -d -p 1443:443 -p 9091:80 -p 1001:22 --name gitlab --restart always -v gitlab_config:/etc/gitlab -v gitlab_logs:/var/log/gitlab -v gitlab_data:/var/opt/gitlab gitlab/gitlab-ce:latest
```

if you want to restrict size of the container you can use `--shm-size 2gb`

```commandline
docker run -d -p 1443:443 -p 9091:80 -p 1001:22 --name gitlab --restart always -v gitlab_config:/etc/gitlab -v gitlab_logs:/var/log/gitlab -v gitlab_data:/var/opt/gitlab --shm-size 2gb gitlab/gitlab-ce:latest
```

To get initial password for your login. open a terminal as root user using the following command

```
docker exec -it -u root gitlab /bin/bash
```
and read the file in location `/etc/gitlab/initial_root_password`

```
cat /etc/gitlab/initial_root_password
```

You can see your initial password, initial user will be root.