## Maven Wrapper
#maven-wrapper
- Wrapper helps to use maven in machines without installing maven in a machine. This makes builds portable.
- Generally found in any maven project under `.mvn` folder.
- To install maven wrapper in any project the command is
```
mvn -N io.takari:maven:wrapper
```

- To find version of maven version in wrapper, on a mac use version `./mvnw --version` on windows `mvnw.cmd --version`
- The maven wrapper might use a different version of maven. to update the version use the following command `mvn wrapper:wrapper -Dmaven=<maven-version-you-prefer>` example `mvn wrapper:wrapper -Dmaven=3.8.4` alternatively we can use `mvn -N io.takari:maven:wrapper -Dmaven=3.8.4`

### Maven Archetype
- An Archetype is a project template. which can be reused.
- **Archetype:** An original pattern or model from which all other things of same kind are made.
- Apache maven provides many archetypes that can be used for java project starters.
- Archetypes are also available with third party plugins. Few archetypes are dated.
> Additional information about Archetypes are available at https://maven.apache.org/guides/introduction/introduction-to-archetypes.html



