# Lifecycle Rules

## Mutability and Immutability of infrastructure

- In immutable infrastructure, when attribute modifications are required for resources. existing resource is deleted and a new resource will be created in its place.
- For Mutable architecture attribute modifications will update the existing resource.
- Terraform mainly tries to choose immutability

## `create_before_destroy`

Consider local_file provider, when file permission is updated, terraform will delete the existing resource and then create a new resource in its place. sometime we might have to create the resource before deleting the existing resource.

```hcl
resource "local_file" "example_ref" {
  filename        = "D:\\temp\\lifecycle.txt"
  content         = "Example file creation for test"
  file_permission = "0777"
  lifecycle {
    create_before_destroy = true
  }
}
```

From now on any modifications will create the resource first and then delete the old one.
```sh
local_file.example_ref: Creating...
local_file.example_ref: Creation complete after 0s [id=55f1c7d312887349604ff8d2e19074f20f33c891]
local_file.example_ref (deposed object f191817d): Destroying... [id=55f1c7d312887349604ff8d2e19074f20f33c891]
local_file.example_ref: Destruction complete after 0s
```

## `prevent_destroy`

Sometimes we might not destroy a resource for making changes like a database provisioned.
We can use prevent_destroy lifecycle hook.

```hcl
resource "local_file" "example_ref" {
  filename        = "D:\\temp\\lifecycle.txt"
  content         = "Example file creation for test"
  file_permission = "0777"
  lifecycle {
    prevent_destroy = true
  }
}
```

This will not allow for deleting and recreating a resource for modifications.
But the resource still can be deleted with `terraform destroy`

## `ignore_changes`

This will ignore changes made to a specific or all attributes of a resource.

example:
```hcl
resource "aws_instance" "webserver" {
	ami = "ami_0kmasgfqwegtrt23t42yq4t238"
	instance_type = "t2.micro"
	tags = {
		name = "server-alpha"
	}
	lifecycle {
		ignore_changes = [
			tags
		]
	}
}
```

Now any changes made to ignore will be ignored and subsequent apply will not update the values for tags. 

we can also make every field as ignore by using
```hcl
resource "aws_instance" "webserver" {
	ami = "ami_0kmasgfqwegtrt23t42yq4t238"
	instance_type = "t2.micro"
	tags = {
		name = "server-alpha"
	}
	lifecycle {
		ignore_changes = all
	}
}
```
