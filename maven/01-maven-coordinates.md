## Maven Coordinates
#maven-coordinates
Generally used for identifying artifacts (project-name). These will help in identifying a location of the artifact in maven repository(https://mvnrepository.com/) to fetch them.

**groupId:** Name of organization or reverse domain name is mentioned.
**artifactId:** Project name or A descriptor for the artifact.
**version:** Refers to a specific version of a project from its version control.

> groupId and Version can be referenced from another POM file also know as parent pom

### Versioning in Maven
#maven-version
An example maven version looks like this `4.9.49-309-beta`
- **Major Version** - the first number - 4
- **Minor Version** - second number - 9
- **Patch Version** - third number - 49
- **Build number** - from CI build or revision - 309
- **Qualifier** - is a string qualifier - beta

> General notation used is **Major.Minor.patch**

## Maven Repositories
**Local** - Repository on local system
**Central** - Hosted by Maven community
**Remote** - Other locations which can be public or private. an organization can have its on repository hosted with nexus or antifactory.

When we ask for an artifact as a dependency -> it will be searched in local machine in the users/m2 folder -> if it is not present it will go search in the repository configured -> if it is not found then it will go for other repositories. -> if not found in any repository we will not be able to download it.

## Maven Wagon
- A Unified maven api which is used for send files or packages in and out of maven repositories. 
- Allows different providers for communications to access Maven repos. 
	- Generally https and http are used most.
- In corporate environments we might be using proxy to access repositories.


