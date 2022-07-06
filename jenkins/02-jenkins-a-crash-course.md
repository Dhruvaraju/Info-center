## Jenkins a crash course
- Install Docker
- To create a Jenkins container and use it #docker-cmd-to-start-jenkins

```commandline
docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11

```

> [!info] Example reference code available at:
>  https://github.com/addamstj/Jenkins-Course

- To get access to a terminal in a docker container use `docker exec -it -u root <container_id> /bin/bash`

### Creating a free style Jenkins project
#freestyle-jenkins-project
- Add new item on Jenkins ui once you log in.
- Provide a name and pick **Freestyle Project** click ok.
- Configure tab will appear go to **build steps** and click on **add build step**.
- Add `echo "First Build"` in the shell and save it.
- It will come to pipeline page, click on build now to run the pipeline.
- Under build history, you can find a build number, clicking on which you can see build status.
- You can check on console output for better logs.

### Installing maven in container
#install-maven-in-container
- Update apt-get by running `apt-get update`
- Install maven using command `apt-get install maven`
- This will persist if we are start and stopping the same container.
- If we are rebuilding from an image plugins will not persist.

### Building a Declarative pipeline
#declarative-pipeline
Declarative Pipeline presents a more simplified and opinionated syntax on top of the Pipeline sub-systems. More info on declarative pipelines present at [Jenkins Pipeline Syntax](https://www.jenkins.io/doc/book/pipeline/syntax/)

**Example:**
```Jenkinsfile
pipeline {
    agent any
    stages {
        stage("Clean Up"){
            steps {
                deleteDir()
            }
        }
        stage("Clone Repo"){
            steps {
                sh "git clone https://github.com/Dhruvaraju/api_for_test_automation.git"
            }
        }
        stage("Build"){
            steps{
                dir("api_for_test_automation"){
                    sh "mvn clean install"
                }
            }
        }
        stage("Test"){
            steps{
                dir("api_for_test_automation"){
                    sh "mvn test"
                }
            }
        }
    }
}
```

### Sample jenkins file
- All valid Declarative Pipelines must be enclosed within a `pipeline` block.
- Sections in Declarative Pipeline typically contain one or more [Directives](https://www.jenkins.io/doc/book/pipeline/syntax/#declarative-directives) or [Steps](https://www.jenkins.io/doc/book/pipeline/syntax/#declarative-steps).

#### Agent
- The `agent` section specifies where the entire Pipeline, or a specific stage, will execute in the Jenkins environment depending on where the `agent` section is placed. The section must be defined at the top-level inside the `pipeline` block, but stage-level usage is optional.
- If we want to run it in the same machine just mention `any`, else provide the machine info
#### stages[](https://www.jenkins.io/doc/book/pipeline/syntax/#stages)
- Containing a sequence of one or more [stage](https://www.jenkins.io/doc/book/pipeline/syntax/#stage) directives, the `stages` section is where the bulk of the "work" described by a Pipeline will be located. At a minimum, it is recommended that `stages` contain at least one [stage](https://www.jenkins.io/doc/book/pipeline/syntax/#stage) directive for each discrete part of the continuous delivery process, such as Build, Test, and Deploy.
#### steps[](https://www.jenkins.io/doc/book/pipeline/syntax/#steps)
- The `steps` section defines a series of one or more [steps](https://www.jenkins.io/doc/book/pipeline/syntax/#declarative-steps) to be executed in a given `stage` directive.

### Getting Jenkins file from Source code
- When choosing a pipeline project
- We can choose to add a pipeline script or get pipeline from SCM
- When we choose to get it from SCM, place the Jenkins file in source code, specify the path to get it.

> [!Info] Polling SCM
> We can run pipeline periodically or choose to run it when changes are made to source code.
> To check for changes and run it we need to poll SCM preferably every 2 minutes.
> Polling requires time as input in cron syntax
> We can get help for cron syntax from https://crontab.guru/ #cron_tab

### Parameterized pipelines
- We can add parameters to pipelines, Which can then be read as variables in each stage.
- A new section `parameters` will be added to Jenkinsfile
#### Boolean Var
- Boolean variables can be added using a function `booleanParam(defaultValue: false, description:"Enable Info", name: "myBoolean")`
- A default value true or false can be provided
- Description is to define what we are using the variable for.
- name specifies the name of variable
- We can access the variable by using `${variable_name}` syntax
**Example:**
```
pipeline{
    agent any
    parameters{
        booleanParam(defaultValue: false, description:"Enable Info", name: "myBoolean")
    }
    stages{
        stage("Clean Up"){
            steps{
                deleteDir()
            }
        }
        stage("Log Variable"){
            steps{
                echo "Value of boolean set to ${params.myBoolean}"
            }
        }
    }
}
```

#### String Var
- String variables can be added using a function `string(defaultValue: "TEST", description:"Deployment Environment", name: "deployEnv")`
- A default value can be provided
- Description is to define what we are using the variable for.
- name specifies the name of variable
- We can access the variable by using `${variable_name}` syntax
**Example:**
```
pipeline{
    agent any
    parameters{
        string(defaultValue: "TEST", description:"Deployment Environment", name: "deployEnv")
    }
    stages{
        stage("Clean Up"){
            steps{
                deleteDir()
            }
        }
        stage("Log Variable"){
            steps{
                echo "Value of boolean set to ${params.deployEnv}"
            }
        }
    }
}
```

#### Choice Var
- String variables can be added using a function `choice(choices: ["TEST"], description:"Deployment Environment", name: "deployEnv")`
- A default value is the first one in list.
- Description is to define what we are using the variable for.
- name specifies the name of variable
- We can access the variable by using `${variable_name}` syntax
**Example:**
```
pipeline{
    agent any
    parameters{
        choice(choices: ["TEST", "PROD", "UAT"], description:"Deployment Environment", name: "deployEnv")
    }
    stages{
        stage("Clean Up"){
            steps{
                deleteDir()
            }
        }
        stage("Log Variable"){
            steps{
                echo "Value of boolean set to ${params.deployEnv}"
            }
        }
    }
}
```

### Variables
- We can define own variables and use them in pipelines.
- We use environment section for it.
- Use `def` keyword to define a variables
- These can be accessed by using `${var_name}`

```
pipeline{
    agent any
    environment{
        def stringVar = "This is a string var"
        def booleanVar = true
        def numberVar = 20
    }
    stages{
        stage("Log Variables"){
            steps{
                echo "String var value is ${stringVar}"
                echo "boolean var value is ${booleanVar}"
                echo "Number var value is ${numberVar}"
            }
        }
    }
}
```

> [!Info] Jenkins Environment Variables
> Jenkins have its own variable names which can be used to access build parameters.
> These can are accessible at https://www.jenkins.io/doc/book/pipeline/jenkinsfile/#using-environment-variables

### If statements
- When we need some logic in stages we need to add it inside script
- An implementation of if condition is explained below.

```
pipeline{
    agent any
    parameters{
        booleanParam(defaultValue: false, description: "Example for if condition", name: "deployInfra")
    }
    stages{
        stage("Demo"){
            steps{
                script{
                    if(params.deployInfra == false){
                        currentBuild.result = "SUCCESS"
                        return
                    } else {
                        echo "booleanParam is set to ${params.deployInfra}"
                    }
                }
            }
        }
    }
}
```

### Functions 
Functions can be used for invoking reusable snippets

```
pipeline{
    agent any
    stages{
        stage("Demo"){
            steps{
                consoleMessage("Example")
            }
        }
    }
}

def consoleMessage(String message){
    echo "message: ${message}"
}
```

https://www.jenkins.io/doc/pipeline/steps/pipeline-build-step/