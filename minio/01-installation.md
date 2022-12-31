To run minio server in a docker container use the below command

```sh
docker run -p 9000:9000 -p 9001:9001 quay.io/minio/minio server /data --console-address ":9001"
```

https://www.youtube.com/watch?v=BZqXh9hLYTA