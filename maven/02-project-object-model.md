## POM
#pom
- Project object model is and xml document which describes a maven project.
- Must comply with xml schema definition `maven-4.0.0.xsd`
- pom can inherit properties from parent pom.
- Effective pom is a pom completed with inherited properties from parent pom. command to see it is 
```
mvn help:effective-pom
```

> To see effective pom in intellij Idea open pom.xml right click -> maven -> show effective pom 

To go to declaration or usage of any referencing artifact `ctrl + rightclick` or `ctrl + b`
#xml-usage-shortcut #xml-reference-shortcut