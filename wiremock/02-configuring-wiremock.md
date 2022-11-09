# Configuring Wire mock for request response
#configure_wiremock

Once wire mock is started, it will create two folders `mappings` and `__files`. In the `mappings` folder add the request response mapping. The corresponding response json files can be added in the `__files` folder. The format of those files should be `.json`.

## Sample Mapping file

```json
{
	"request": {
		"method": "POST",
		"urlPath": "/api/example"
	},
	"response": {
		"status": 200,
		"headers": {
			"Content-Type": "application/json"
		}
	}
}
```

- Request and response object need to be defined.
- Under `request`
	- method `POST/PUT/GET/UPDATE/DELETE` will be specified.
	- `urlPath` the path of the api will be specified
- Under `response`
	- `status` which http status code is required that will be mentioned.
	- `headers` we can mention the header parameter
	- `body` we can mention the json body, content which need to be returned as string.

We can add match the parameters passed in request url, query parameters, headers and request body.
We can send a string or return a json body as response referring to a file. `bodyFileName: <<path inside the files>>`. example: `bodyFileName: externalsystem/response.json` where `response.json` is the response as a json file and `externalsystem` is the folder in which the `response.json` is residing.

Additional Stubbing information found at:
https://wiremock.org/docs/stubbing/