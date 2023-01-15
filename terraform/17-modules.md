# Modules in Terraform

Modules in terraform are reusable code used to run multiple identical resources, with different parameters, using the same configuration files.

Example:
- Create a terraform-projects folder
- Create folder terraform-projects/modules
- Create a folder terraform-projects/modules/payroll-ap
- Under pay roll app folder create files
	- app_server.tf
	- dynamodb_table.tf
	- s3_bucket.tf
	- variables.tf

// app_server.tf
```hcl
resource "aws_instance" "app_server" {
	ami = var.ami
	instance_type = "t2.medium"
	tags = {
		Name = ""${var.app_region}-app-server"
	}
	depends_on = [ aws_dynamodb_table.payroll_db,
					aws_s3_bucket.payroll_data
	]
}
```

// s3_bucket.tf
```hcl
resource "aws_s3_bucket" "payroll_data" {
	bucket = "${var.app_region}-${var.bucket}"
}
```

//dynamodb_table.tf
```hcl
resource "aws_dynamodb_table" "payroll_db"{
	name = "user_data"
	billing_mode = "PAY_PER_REQUEST"
	hash_key = "EmployeeID"

	attribute {
		name = "EmployeeID"
		type = "N"
	}
}
```

//variables.tf
```hcl
varibale "app_region" {
	type = string
}

variable {
	default = "flexit-payroll-alpha-22001c"
}

variable {
	type = string
}
```

Now we can use the above files as module and build another resource
- Create a folder terraform-projects/us-payroll-app
- Create a main.tf and provider.tf

//main.tf
```hcl
module "us_payroll" {
	source = "../modules/payroll-app"
	app_region = "us-east-1"
	ami = "ami-akhdgfwefygwuargw87q48y2387"
}
```

now when we run the terraform plan and apply will use the app_region and ami to create the  resources.

> Modules can be compared to packages or libraries in other programming languages.

- This will help in 
	- Simpler configuration files
	- Lower risk
	- Re-usability
	- Standardizing resources.

## Using modules from registry
- Terraform registry provides lots of modules
- https://registry.terraform.io/browse/modules
- There are 2 types of modules:
	- Official HashiCorp validated
	- Community provided

Example: For google verified network module
This is available at: https://registry.terraform.io/modules/terraform-google-modules/network/google/latest?tab=inputs

```hcl
module "network" {
  source  = "terraform-google-modules/network/google"
  version = "6.0.1"
  # insert the 3 required variables here
  network_name =
  project_id =
  subnets = []
}
```

To get the modules locally use `terraform get`
