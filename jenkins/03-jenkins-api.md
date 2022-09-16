# Jenkins API
#jenkins_api
## Create API token
To access API Jenkins uses basic authentication, it is better to create separate user and use access token for API access. User can obtain API token from personal configuration page of Jenkins which is accessible on `$JENKINS_URL/me/configure`

A random token will have alpha numeric content.

## Config.xml location
- In a container config.xml location will be present at each job level under `/var/jenkins_home/jobs/<pipeline_name>/config.xml`.
- In a windows machine `~/users/<user_name>/.jenkins/jobs/<pipeline_name>/config.xml`.

## Create Pipeline using API

Jenkins support creation API for which you need to pass xml file for the job structure which you want to create. You can follow below steps to obtain xml file and create the pipeline:

-   Create pipeline manually in Jenkins UI and test it.
-   Export your pipeline using export import plugin or Jenkins jar to xml file.
-   Now use this xml file as a reference and create pipeline through API.
-   Use below curl to create pipeline

```
# JENKINS_USER_API_TOKEN is obtained from $JENKINS_URL/me/configure
BASIC_AUTH=${JENKINS_USER}:$JENKINS_USER_API_TOKEN

# Obtained from URL without any protocol
JENKINS_ADDRESS="<jenkins_host>:<port>"

# Curl will create pipeline with name my_pipeline with config from file config.xml
curl -X POST http://${BASIC_AUTH}@${JENKINS_ADDRESS}/createItem?name=my_pipeline \
    --header "Content-Type:text/xml" \
    --data-binary @config.xml

```

API to Create Jenkins Pipeline

Curl request will return status **200** if pipeline is successfully created otherwise it will return **400** if pipeline is already created or failed to create due to some error

## Update pipeline using API

Updating pipeline is nothing but updating config.xml for that job.

```
# Update job config.xml   
curl -X POST http://${BASIC_AUTH}@${JENKINS_ADDRESS}/job/my_pipeline/config.xml \
                  --header "Content-Type:text/xml" \
                  --data-binary @new_config.xml
```

API to update Jenkins Job

Above curl request will return **200** if pipeline is updated successfully otherwise it will have status code greater than **400** in case of error.

Note the URL in update request it has **config.xml** in path.

## Delete Pipeline using API

Deletion of pipeline/job is also a POST request with _doDelete_ action specified in the request.

```
# Delete pipeline using doDelete pipeline
curl -X POST http://${BASIC_AUTH}@${JENKINS_ADDRESS}/job/my_pipeline/doDelete
```

API to delete Jenkins Job

Above curl request will return **200** if job is deleted successfully in case of failure it should return status code greater than **400**.

## Trigger Pipeline using API

This is the most common case of using API to automate job trigger with parameters. Use below curl to trigger pipeline/job via curl request.

```
# Pass parameters with --data option
curl http://${BASIC_AUTH}@${JENKINS_ADDRESS}/job/my_pipeline/buildWithParameters \
  --data param1=123 --data param2="git-repo"
```

> [!Info] Jenkins Remote access api
> https://www.jenkins.io/doc/book/using/remote-access-api/


### Example Config.xml
```xml
<?xml version='1.1' encoding='UTF-8'?>
<project>
  <actions/>
  <description></description>
  <keepDependencies>false</keepDependencies>
  <properties/>
  <scm class="hudson.scm.NullSCM"/>
  <canRoam>true</canRoam>
  <disabled>false</disabled>
  <blockBuildWhenDownstreamBuilding>false</blockBuildWhenDownstreamBuilding>
  <blockBuildWhenUpstreamBuilding>false</blockBuildWhenUpstreamBuilding>
  <triggers/>
  <concurrentBuild>false</concurrentBuild>
  <builders>
    <hudson.tasks.Shell>
      <command>echo &quot;First Build&quot;</command>
      <configuredLocalRules/>
    </hudson.tasks.Shell>
  </builders>
  <publishers/>
  <buildWrappers/>
  </project>
```

## Postman call to create a job
- Make a post call `http://localhost:8080/createItem?name=exampleJob`
- Use basic authorization provide Jenkins username and the api key generated in configure section.
- Add header `Content-Type` as `text/xml`
- In the body section choose binary and attach the above config.xml
- Once you execute the post call, exampleJob should be reflecting in Jenkins.
- For updating the job use method `update` `/job/<pipeline_name>/config.xml`
- For deleting the job use method `delete` `/job/<Pipeline_name>/config.xml`

## Api to get the list of builds
```
<jenkins-server-address>/job/<pipeline_name>/api/json

#Example
http://localhost:8090/job/exampleJob/api/json
```

**Example Response:**
```
{

    "_class": "hudson.model.FreeStyleProject",

    "actions": [

        {},

        {},

        {

            "_class": "org.jenkinsci.plugins.displayurlapi.actions.JobDisplayAction"

        },

        {

            "_class": "com.cloudbees.plugins.credentials.ViewCredentialsAction"

        }

    ],

    "description": "",

    "displayName": "exampleJob",

    "displayNameOrNull": null,

    "fullDisplayName": "exampleJob",

    "fullName": "exampleJob",

    "name": "exampleJob",

    "url": "http://localhost:8090/job/exampleJob/",

    "buildable": true,

    "builds": [

        {

            "_class": "hudson.model.FreeStyleBuild",

            "number": 2,

            "url": "http://localhost:8090/job/exampleJob/2/"

        },

        {

            "_class": "hudson.model.FreeStyleBuild",

            "number": 1,

            "url": "http://localhost:8090/job/exampleJob/1/"

        }

    ],

    "color": "blue",

    "firstBuild": {

        "_class": "hudson.model.FreeStyleBuild",

        "number": 1,

        "url": "http://localhost:8090/job/exampleJob/1/"

    },

    "healthReport": [

        {

            "description": "Build stability: No recent builds failed.",

            "iconClassName": "icon-health-80plus",

            "iconUrl": "health-80plus.png",

            "score": 100

        }

    ],

    "inQueue": false,

    "keepDependencies": false,

    "lastBuild": {

        "_class": "hudson.model.FreeStyleBuild",

        "number": 2,

        "url": "http://localhost:8090/job/exampleJob/2/"

    },

    "lastCompletedBuild": {

        "_class": "hudson.model.FreeStyleBuild",

        "number": 2,

        "url": "http://localhost:8090/job/exampleJob/2/"

    },

    "lastFailedBuild": null,

    "lastStableBuild": {

        "_class": "hudson.model.FreeStyleBuild",

        "number": 2,

        "url": "http://localhost:8090/job/exampleJob/2/"

    },

    "lastSuccessfulBuild": {

        "_class": "hudson.model.FreeStyleBuild",

        "number": 2,

        "url": "http://localhost:8090/job/exampleJob/2/"

    },

    "lastUnstableBuild": null,

    "lastUnsuccessfulBuild": null,

    "nextBuildNumber": 3,

    "property": [],

    "queueItem": null,

    "concurrentBuild": false,

    "disabled": false,

    "downstreamProjects": [],

    "labelExpression": null,

    "scm": {

        "_class": "hudson.scm.NullSCM"

    },

    "upstreamProjects": []

}
```
