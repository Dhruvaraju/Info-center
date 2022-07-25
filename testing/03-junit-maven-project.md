## Adding Junit to a maven project
- Create a new properties variable
```
<junit-platform.version>5.8.2</junit-platform.version>
```

Add the following dependency to pom.xml

```xml
<dependency>  
    <groupId>org.junit.jupiter</groupId>  
    <artifactId>junit-jupiter-api</artifactId>  
    <version>${junit-platform.version}</version>  
    <scope>test</scope>  
</dependency>  
<dependency>  
    <groupId>org.junit.jupiter</groupId>  
    <artifactId>junit-jupiter-engine</artifactId>  
    <version>${junit-platform.version}</version>  
    <scope>test</scope>  
</dependency>
```

To run the test in build phase we need to add couple of plugins in build.

```xml
<build>  
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>  
            <artifactId>maven-surefire-plugin</artifactId>  
            <version>2.22.2</version>  
        </plugin>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>  
            <artifactId>maven-failsafe-plugin</artifactId>  
            <version>2.22.2</version>  
        </plugin>
    </plugins>
</build>
```

>[!Info]
> Surefire for running unit tests.
> Failsafe for running integration tests.