## mysql docker container
- MySql has an official container in docker hub.
- We can create a local docker container using the following command.

```commandline
docker run -d -p 3306:3306 --restart always -v my_sql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=admin -e MYSQL_DATABASE=testDatabase -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin --name mysql mysql:latest
```

- mysql by default exposes port 3306, we need to map it to the exposed port to access databases.
- Data will be written to `/var/lib/mysql`
- Set root password using `-e MYSQL_ROOT_PASSWORD=admin`
- Set a new user by using `-e MYSQL_USER=admin`
- Set password for the new created user by using `-e MYSQL_PASSWORD=admin`
- For connecting to this container add the following properties in application.properties

```properties
mysql.service.host=localhost
mysql.service.port=3306
mysql.service.username=admin
mysql.service.password=admin

spring.datasource.url=jdbc:msql://${mysql.service.host}:${mysql.service.port}/testdirector
spring.datasource.username=${mysql.service.username}
spring.datasource.password=${mysql.service.password}

spring.jpa.hibernate.ddl-auto=create
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
spring.jpa.show-sql=true
spring.jpa.database-platform=org.hibernate.dialect.MySQl8Dialect
```
