# taint and un-taint
#terraform_taint #terraform_untaint #taint #untaint
- When a resource creation is not properly done or some provisioner failed while creating resource, terraform marks that resource as tainted.
- A tainted resource will be recreated when the terraform apply is run.
- sometime when manual changes are made to the resource that terraform created we might have to recreate it, instead of doing so we can mark a terraform resource as tainted by using `terraform taint <resource_name>`
- To untaint a resource use `terraform untaint <resource_name>`

## Debugging in Terraform
#terraform_logs
- On running `terraform apply` we get lots of logs. If we need additional logging we can configure terraform to do so.
- Set the terraform log level with environment variable as `export TF_LOG=TRACE`
- Terraform provides the following log levels
	- INFO
	- WARNING
	- ERROR
	- DEBUG
	- TRACE
- To redirect logs to a persistent file use the environment variable `TF_LOG_PATH` eg: `export TF_LOG_PATH=/tmp/terraform.log`

## Terraform import
#terraform_import
In real world we might not use terraform for creating all the resources from scratch. There might be few resources which are already created earlier. We can collect the information of those resources with help of data source. To get these resources under the control of terraform we use terraform import.

syntax for terraform import
```sh
terraform import <resource_type>.<resource_name> <unique_identifier_attribute>
```

example:
```sh
terraform import aws_instance.webserver i-cjkhg348raw734r2h3qg4w
```

The above command might not work straight away, we need to manually add a resource block with empty content and then run it.

```
resource "aws_instance" "webserver"{

}

# Now run the command
terraform import aws_instance.webserver i-cjkhg348raw734r2h3qg4w
```

Once after the import is successful add the appropriate variables in the resource block, the next terraform apply will not update anything because the resource is already created.
