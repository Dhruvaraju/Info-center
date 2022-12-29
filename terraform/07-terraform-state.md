# What is state?

- Terraform is a blueprint of the resource that terraform is created.
- It will be created when `terraform apply` is run.
- State file will be named as `terraform.tfstate`
- It is a json file to keep track of all the resources that are created.
- Terraform uses state a source of truth.
- Every attribute information related to terraform will be present in `terraform.tfstate` file.
- It is better to store configuration files in a version control.
- But it would be better to store the `terraform.tfstate` file in a secure storage as it contains sensitive information.

## Why is state considered as source of truth

Consider a scenario where a configuration file contains 3 resources, the configuration is applied and resources are created. Next couple of resources are removed. If we consider the configuration file alone terraform will not be able to understand which resources need to be deleted. As state file is present, a comparison will be made and terraform will delete those files.

- Every time when we run a plan or apply terraform will check for an existing state file to compare with.