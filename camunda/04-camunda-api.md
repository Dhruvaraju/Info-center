## Camunda Rest
> [!Note]
> While passing a json to Camunda as a process variable, pass it as escaped JSON string .

**Example:**
```json
{
    "variables": {
        "broker": {
            "value": "{\"name\":\"Broker Name\"}",
            "type": "json"
        }
    }
}
```

[Additional Information](https://stackoverflow.com/questions/50771870/pass-json-in-process-variables-in-camunda-process)

