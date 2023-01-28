# Configuration in kubernetes
- If we need to run a command once a container starts like sleep command on ubuntu.
- While creating a docker image we add the command as an entry point
- Arguments are passed as CMD
example dockerfile
```dockerfile
FROM ubuntu
ENTRYPOINT ["sleep"]
CMD ["10"]
```
- On building and running this image. A ubuntu image is started and sleeps for 10 seconds and exists
- Same can be achieved by `docker run --entrypoint sleep ubuntu:ubuntu 10`

The same changes in a pod definition file
```yml
apiVersion: v1
kind: pod
metadata:
spec:
	containers:
		- name: ubuntu sleeper
		  image: ubuntu:ubuntu
		  command: ["sleep"]
		  args: ["10"]
```
