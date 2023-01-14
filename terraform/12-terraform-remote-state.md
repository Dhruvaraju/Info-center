# Remote state

- Generally terraform creates a state file in the folder where configuration is present.
- Maintaining state locally is a not recommended
- Maintaining state in a version control system is also not recommended
	- Every time when performing operations on terraform we need to add pull latest version of state
	- If someone failed to push an updated state, further operations by others will create a data loss or resource manipulation
- We cannot store state on a SCM because it will contain sensitive information like IP's and initial credentials.

## State Locking
#terraform-state-locking #state-locking
 When an apply is running on a terraform configuration, terraform will not allow running another apply on the same configuration. To preserve the current state. This is called as state locking.

## Remote Backend
#remote-back-end
- As storing state is local configuration or SCM is not advised. State need to be stored in a remote location.
- An object storage is preferred for storing state, This is called as storage backend.
- Once a storage backend is added, whenever an apply is triggered. it will always fetches the latest state from storage backend.
- It would be better if storage backend provides state-locking.
- Git doesn't provide state locking.
- Examples of storage-backend AWS S3, HashiCorp Consul, Google Cloud Storage, Terraform Cloud

Advantages;
 - Automatically Load and upload state file
 - Many Back-end support state-locking
 - Security

### Remote Backend with S3

- an existing S3 bucket is required for terraform state storage
- Dynamo DB instance is required for state locking
- Bucket Name, Key or path on bucket, region of aws and dynamo DB table for state-locking 
- add a terraform block with backend section, an example provided below
	- Immediately after creation terraform apply will not work, backend need to be initiated so use `terraform init`

```hcl
resource "local_file" "pet" {
	filename = "d://temp.txt"
	content = "example for testing"
}

terraform {
	backend "s3" {
		bucket = "alpha-bucket-01"
		key = "daimension/alpha"
		region = "us-west-1"
		dynamodb_table = "state-locking"
	}
}
```

> We can add the terraform section to a different file named as `terraform.tf`
> Then a terraform apply and remove the state file from local folder.

## Terraform State Commands

Terraform state should never be modified manually, we have few commands to manipulate terraform state.

- Terraform state command syntax
```sh
terraform state <sub_command> [options] [args]
```
- Few of terraform state commands
	- list
	- mv
	- pull
	- rm
	- show


### `terraform state show`
 To see the state of a terraform resource use `terraform state show <resource_name>` #state_show
```sh
terraform state show local_file.ev[0]

# will retun
# local_file.ev[0]:
resource "local_file" "ev" {
    content              = "example content"
    directory_permission = "0777"
    file_permission      = "0777"
    filename             = "d:\\temp\\alpha.txt"
    id                   = "0ff30941ca5acd879fd809e8c937d9f9e6dd1615"
}
```
- `terraform state list` will print details of every resource, it will not give any additional information

### `terraform state mv`
Generally used to move recourses across different configuration folders or rename a resource. If we want to rename a resource from cars to suvs

```sh
terraform state mv local_file.cars local_file.suvs
```

Remember to update the configuration file manually. Once renamed, if you run terraform apply there should not be any update to the resources.

### `terraform state pull`
When  we store terraform state in remote backend, we have to use `terraform state pull` to download and display state information. We can pass the json information to parsers for furthur processing if required.

### `terraform state rm`

Use this command to remove a resource from state, when it is no longer required to be maintained by terraform.
example: `terraform state rm local_file.cars`

- Remember to remove the resource manually from the configuration file.
- Running a terraform rm will not delete the resource in real world, it will just remove if from state.