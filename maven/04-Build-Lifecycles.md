## Maven Build Lifecycles
#maven-build-lifecycle
- Maven is based on build lifecycles.
- A lifecycle is a group of pre-defined steps called as phases.
- Each phase can be bound to one or more plugin goals.

> Every work done in maven will be done with help of plug-ins.

- Life cycle and phases provide a framework to call plugin goals in a sequence.

- There are three pre-defined lifecycles
	- clean
	- default
	- site

### Clean
- Does a clean of the project, removes all artifacts generated from working directory.
- Can be defined with plugin bindings

### Default
- Build and deployment of the project will be done.
- Defined without plugin bindings, bindings are defined for each packaging.

### Site
- Creates a website for the project, defined with plugin bindings.
- Generally not used, All maven websites are build using maven site lifecycle.

### Clean Lifecycle
Has three phases

| step. no| phase | default plugin binding|
|----|----|----|
|1| pre-clean | None |
|2| clean | **Maven Clean plugin with goal clean** |
|3| post-clean | None |

### Default Lifecycle
1) Validate : Verify if project is correct, like folder structure, valid pom.
3) Compile: Compiles source code.
4) Test: Tests compiled source code.
6) Package: Package compiled files to a packaging type like jar or pom.
7) Verify: Runs integration tests.
9) Install: Installs to local maven repository.
10) Deploy: Deployed to shared maven repository like maven central.

#### All the phases in default lifecycle
1) Validate
2) Initialize
3) Generate Sources
4) Process Sources
5) Generate Resources
6) Process Resources
7) Compile
8) Process Classes
9) Generate Test Sources
10) Process Test Sources
11) Generate Test Resources
12) Process Test Resources
13) Test Compile
14) Process Test classes
15) Test
16) Prepare Package
17) Package
18) Pre-integration test
19) Integration test
20) Post Integration test
21) Verify
22) Install Deploy

### Default Lifecycle - JAR Packaging
Phases in sequence

| No | Phase | Plugin |
|----|----|----|
| 1 | process-resources | maven-resources-plugin: resources |
| 2 | compile | maven-compiler-plugin: compile |
| 3 | process-test-resources | maven-resources-plugin: testResources |
| 4 | test-compile | maven-compiler-plugin: testCompile |
| 5 | test | maven-surefire-plugin: test |
| 6 | package | maven-jar-plugin: jar |
| 7 | install | maven-install-plugin: install |
| 8 | deploy | maven-deploy-plugin: deploy |

### Site Build Lifecycle
| No | Phase | Plugin |
|----|----|----|
| 1 | pre-site | none |
| 1 | Site | maven-site-plugin: site |
| 1 | Post-site | none |
| 1 | Site-deploy | maven-site-plugin: deploy |





