# Terraform Workspace

Reusing same configuration files for creating multiple infrastructure environments within the same configuration directory is possible using workspaces.

To create a new workspace
```sh
terraform workspace new <workspace_name>
```

- Once workspace is created terraform will switch to the workspace as well.

To see the list of workspaces use
```sh
terraform workspace list
```

The current workspace will have a `*` pre-pended to it.

//main.tf
```hcl
resource "aws_instance" "projectA" {
	ami = lookup(var.ami, terraform.workspace)
	instance_type = ami.instance_type
	tags = {
		Name = terraform.workspace
	}
}
```

//varibales.tf
```hcl
variable region {
	default = "ca-cental-1"
}

variable instance_type {
	default = "t2-micro"
}

variable ami {
	type = map
	default = {
		"projectA" = "ami-project-a"
		"projectB" = "ami-project-b"
	}
}
```

the variable `terraform.workspace' will provide the current workspace name

To switch between workspaces use `terraform workspace select <workspace_name>`
