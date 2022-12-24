# Using Local Provider

To create a text file using terraform we can use local provider.
Create a configuration file as below.

```
resource "local_file" "pet" {
    filename = "D:\\temp\\example.txt"
    content = "Initial file from terraform"
}
```

### `terraform init`
	- Terraform will identify which provider is being used.
	- Then download the files related to those provider and create `.terraform` folder.

```sh
Initializing the backend...

Initializing provider plugins...
- Finding latest version of hashicorp/local...
- Installing hashicorp/local v2.2.3...
- Installed hashicorp/local v2.2.3 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

###  `terraform plan` 
- to check which resources will be created, modified as per the configuration given.
- Output from for the above config file will be something like this
```sh
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # local_file.pet will be created
  + resource "local_file" "pet" {
      + content              = "Initial file from terraform"
      + directory_permission = "0777"
      + file_permission      = "0777"
      + filename             = "D:\\temp\\example.txt"
      + id                   = (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```

- The plus symbol indicates an addition of a resource
- List of attributes modified will be displayed.

### `terraform apply`
- This will create the resource mentioned in the configuration 
- Before creating it will ask to proceed with the creation.

```sh
Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # local_file.pet will be created
  + resource "local_file" "pet" {
      + content              = "Initial file from terraform"
      + directory_permission = "0777"
      + file_permission      = "0777"
      + filename             = "D:\\temp\\example.txt"
      + id                   = (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

local_file.pet: Creating...
local_file.pet: Creation complete after 0s [id=afb2ad235663ca4d4901802d057d9cbe10911337]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

> apply also lists the resources and displays them in github syntax.

### Files that will be generated
- `.terraform` folder will be created
- `terraform.locl.hcl` file will be created
- `terraform.tfstate` file will also be created.

