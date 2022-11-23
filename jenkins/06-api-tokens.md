# Generating Api tokens

For generating an api token we need to follow the following steps:

Create a CSRF token also know as CRUMB

```sh
curl -s --cookie-jar **/tmp/cookies** -u username:password http://localhost:8080/crumbIssuer/api/json
```

This returns a response like 

```json
{  
   "_class":"hudson.security.csrf.DefaultCrumbIssuer",  
   "crumb":"24c0fd6d0763fe8ad72709f0bae08d",  
   "crumbRequestField":"Jenkins-Crumb"  
}
```

We can use the value from `crumb` to get api token as below.

```sh
curl -X POST --cookie **/tmp/cookies** http://localhost:8080/me/descriptorByName/jenkins.security.ApiTokenProperty/generateNewToken?newTokenName=<**token name**>  
-H "Jenkins-Crumb:<**value of crumb from last response**>" -u username:password
```

Which will respond with a response similar to:

```json
{  
  "status":"ok",  
  "data":{  
    "tokenName":"token name",  
    "tokenUuid":"51f0ea87-862c-4e31-a9cd",  
    "tokenValue":"112cb65b59c70cd"  
    }  
}
```

For revoking the token use the following api

```sh
curl -X POST --USER username:password --data 'tokenUuid=<token_id>'  http://localhost:8080/me/descriptorByName/jenkins.security.ApiTokenProperty/revoke
```
