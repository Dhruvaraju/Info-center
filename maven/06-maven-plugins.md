## Maven Plugins Overview
#maven-plugins

### Clean Plugin
- Belongs to lifecycle - `CLEAN`
- Only one goal : `-clean`
- Used to remove files generated during build process.
- By default removes target directory from project root or all sub directory root

```xml
<build>  
    <plugins>  
        <plugin>  
            <groupId>org.apache.maven.plugins</groupId>  
            <artifactId>maven-clean-plugin</artifactId>  
            <version>3.2.0</version>  
            <executions>  
                <execution>  
                    <id>auto-clean</id>  
                    <phase>initialize</phase>  
                    <goals>  
                        <goal>clean</goal>  
                    </goals>  
                </execution>  
            </executions>  
        </plugin>
    </plugins> 
</build>
```
