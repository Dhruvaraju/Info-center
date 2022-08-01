## Maven Dependencies
#maven-dependency

**Dependency:** 
An artifact which maven project depends upon it can be a jar or another pom file.

**Transitive Dependency:** 
- A dependency of an artifact which a project might depend on.
Example: Project A depends on Artifact B and Artifact B depends on Artifact C
A -> B -> C, so C is a transitive dependency.
- It can go much deeper also.
- Cyclic dependency is not accepted by maven. A->B->A is not allowed.

**Dependency Management:**
Which will allow a specific version of an artifact to be used by mentioned in the pom.

**Dependency Mediation:**
Determines which version of dependency to be used when multiple versions of same dependency is encountered. Generally 'Nearest dependency'  in dependency tree is used.
*Example:* A->B; A->D (2.0), B->D(1.5)
D version 2.0 is used in the final packaging.

**Excluded Dependencies:**
Ability to exclude specific dependencies.

**Optional Dependencies:** 
Ability to make dependencies optional.(Excluded by default for downstream projects)

> Classpath list of all the jars or dependency required to run a project or application. There will be 3 types of classpath
> Compile-time classpath: List of dependencies that are required during compile time.
> Runtime classpath: List of dependencies required during runtime. Maximum of compile dependencies will be present in this as well.
> test classpath: List of dependencies that are required when unit and integration tests are being run.
> #classpath #compile-classpath #runtime-classpath #test-classpath

### Dependency Scope
#dependency-scope

**Compile:**
This is a default scope, when compiling the project the dependency with compile scope will be referenced. Propagates for downstream as well.
**Provided:**
This is like compile scope but instead of some repository the dependency will be provided by jdk or container at runtime.
**Runtime:** 
Not required for compile time, only needed during runtime and test classpath.
**Test:**
Only available on test classpath, this is not transitive.
**System:**
Similar to provided but jar is directly added from system with file path.
**import:**
imports dependency of pom.

### Maven Dependency plugin
#dependency-plugin
Dependencies are managed by the maven dependency plugin, some of the goals are as below.
Goals:
- dependency:tree - shows the dependency tree and scope generally used for resolving conflicts.
- dependency:go-offline -  resolve all dependency prepare to go offline.
- dependency:purge-local-repository - clears all artifacts from local repository
- dependency:sources - get sources for all dependencies.

### Maven standard directory layout
https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html