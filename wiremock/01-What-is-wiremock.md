# What is wiremock?
#wiremock

Wiremock is a flexible api mocking tool, which is opensource and freeware. It can be run standalone as well as few other options. It can be used as a library by any JVM application, or run as a standalone process either on the same host as the system under test or a remote server.

All of Wire Mock’s features are accessible via its REST (JSON) interface and its Java API. Additionally, stubs can be configured via JSON files.

Documentation for wiremock is present at https://wiremock.org/docs/

Standalone jar can be downloaded from:

https://repo1.maven.org/maven2/com/github/tomakehurst/wiremock-jre8-standalone/2.35.0/wiremock-jre8-standalone-2.35.0.jar

To start the stand alone version place the jar in a folder and run it using the following command

```commandline
java -jar wiremock-jre8-standalone-2.35.0.jar --port 9099
```

Wire mock will be up and running on port 9099, if you are using another version of jar replace it with name of jar file.

Additional command line augments explained at https://wiremock.org/docs/running-standalone/