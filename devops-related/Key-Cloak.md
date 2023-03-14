
Running key-cloak with docker

Key cloak will run on port 8081
```bash
docker run -p 8081:8080 --name keycloak -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:21.0.1 start-dev
```
