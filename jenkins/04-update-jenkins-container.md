## Updating Jenkins container 
First identify your image.
```console
$ docker ps --format "{{.ID}}: {{.Image}} {{.Names}}"
3d2fb2ab2ca5: jenkins-docker jenkins-container
```

Then login into the image as root.
```console
$ docker container exec -u 0 -it jenkins-container /bin/bash
```

Now you are inside the container, download the `jenkins.war` file from the official site like.
```console
# wget wget http://updates.jenkins-ci.org/download/war/2.176.1/jenkins.war
```

Replace the version with the one that fits to you.

The next step is to move that file and replace the oldest one.
```console
# mv ./jenkins.war /usr/share/jenkins/
```

Then change permissions.
```console
# chown jenkins:jenkins /usr/share/jenkins/jenkins.war
```

The last step is to logout from the container and restart it.
```console
$ docker restart jenkins-docker_1
```

You can verify that update was successful by access to you Jenkins URL.