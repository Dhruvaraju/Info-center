### What is Terraform?
#terraform

- An infrastructure automation tool, which is open source and vendor agnostic. Meaning it works with many vendors, it doesn't matter which vendor we are using.
- The source file is a single binary compiled from Go Lang.
- It uses declarative syntax.
- Configuration files are written in HashiCorp configuration language (extension `.tf`) or JSON.
- It follows push based deployment style.

### Core components of Terraform
- Executable which is the source code itself.
- Configuration files (HCL or Json)
- Provider plugins (Cloud provider plugins)
- State Data (Terraform maintains state files which will say the current situation of an environment that a component is provisioned to.)


## Installing terraform

- Download terraform binary from terraform website according to your platform
- Unzip and place it in a folder.
- Add the location to path

Installation procedure can be found at: https://developer.hashicorp.com/terraform/downloads
- For Linux move the binary to `/usr/local/bin`
- For windows add the location of binary in user or system variables.

#terraform-version
```sh
#To identify version of terraform
terraform version
```

- We can start deploying resources after this.

Terraform uses a declarative language called `HCL`
These can be created using any text editor, `hcl` files have an extension of `.tf`

## What is terraform resource

- A resource is an object that terraform manages
- It can be a file on a local host
- Or a virtual machine, IAM user, roles, s3 buckets or anything that a cloud provider provides.
- There are many resources which can be provisioned using terraform.