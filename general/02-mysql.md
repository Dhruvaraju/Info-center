## mysql docker container
#mysql
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

Log in to bash on container use below command:
```commandline
docker exec -it -u root mysql /bin/bash
```

Log in to mysql #login-to-mysql
```
mysql -uroot -p
# provide password here it will be admin
```

#mysql-commands
- use `show databases;` to see all databases.
- `use <<database-name>>` to got to a specific database.
-  `show tables;` to see all tables.
-  `desc <<table-name>>;` to see the fields and required values.

## Granting permissions on database
- Log in with mySql with root user `mysql -uroot -p` then provide password.
- Create a database
- Use the following command to give all access to an user named as admin ` GRANT ALL PRIVILEGES ON '<your_db_name>' . * TO '<user_name>'`
- Example: `GRANt ALL PRIVILEGES ON 'test-db' . * TO 'admin'`