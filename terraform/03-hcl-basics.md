# HashiCorp Configuration Language
#hcl

HCL syntax contains the following 

```hcl
<block> <paramaters> {
	key1 = value1
	key2 = value2
}
```

- HCL syntax contains blocks and arguments.
- Block is defined with in a curly brace
- Inside the block arguments will be present as key value pairs.

A typical block contains defines an infrastructure platform and set of resources that can be created in it. Consider a simple task that we need to create a file in a machine where terraform is installed.

```hcl
resource "local_file" "pet" {
    filename = "D:\\temp\\example.txt"
    content = "Initial file from terraform"
}
```

Above example is explained as below:

- `resource` indicates the name of block
- `local_type` indicates resource type
	- `local` is provider
	- `file` is resource
- `pet` is file name
- `filename` and `content` are arguments for resource type
	- `filename` is the name of the file that is going to be created in local.
	- `content` specifies the content that will be created inside it.

Examples:

- For creating a s3 bucket
// aws-s3.tf
```
resource "aws_s3_bucket" "data" {
	bucket = "webserver-bucket-org-2207"
	acl = "private"
}
```

- For creating an ec2 instance
//aws-ec2 instance
```hcl
resource "aws_instance" "webserver" {
	ami = "ami-oaGFasdmnbjHFGkaed90896GD&Rwgkhdtwedm"
	instance_type = "t2.micro"
}
```

## Terraform Work flow
#terraform-work-flow

A typical terraform workflow consists of 4 steps as mentioned below.

- [ ] Write Configuration file, place it in a folder
- [ ] Run `terraform init`
- [ ] Review execution plan using `terraform plan` command
- [ ] Apply the changes using `terrafomr apply`