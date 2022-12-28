# Terraform Basics

## Terraform Providers

Once after creating a configuration, to initialize the configuration we run `terraform init`, this will  do the following:
- Identify the provider
- Download the provider, create a `.terraform` folder and place the required provider related files 
- The providers can be from any cloud providers like azure, aws, gcp or as used earlier it can be from local provider as well.

> [!Info]
> Terraform uses plugin based architecture to work with many plugins

- Providers are distributed by HasiCorp and publicly available at url `registry.terraform.io`
- There are 3 tiers of providers
	- **Official**
		- These are maintained and provided by HasiCorp
		- Example: Aws, Azure, GCP
	- **Verified**
		- These are owned and maintained by third party providers which go through a partner access program by HasiCorp
		- Example: BigIP, Heroku, Digital ocean
	- **Community**
		- Community providers are published and maintained by Individuals of community.

### Terraform init from a provider perspective

- On running `terraform init` terraform will download the plugin and place it in `.terraform folder` which will be created new in the same folder where configuration is present.
- Terraform always gets the most latest version from registry
- The version of provider can be configured in configuration file.

```sh
Initializing provider plugins...
- Finding latest version of hashicorp/local...
- Installing hashicorp/local v2.2.3...
- Installed hashicorp/local v2.2.3 (signed by HashiCorp)
```

### Provider Naming Convention
 - `organization-namespace/provider` eg: `hashicorp/local`
- The registry url can also be appended before the organization namespace.
- For an official provider the registry url will be `registry.hashicorp.io`
- So the provider name can be `registry.hashicorp.io/hasicorp/local`
- As it is an official provider no need to mention the registry name.

## Configuration Directory

- In the local-file example a single configuration file is created for `local_file` resource.
- We can have more than one configuration file with in a configuration directory.
- Generally when we have more than one resource block, instead of creating separate `.tf` files, all those are placed in a single file and named as `main.tf`
- Other than resources we can also have few types 

| File Name | purpose |
| ---- | ---- |
| main.tf | main configuration file containing resource definition |
| variables.tf | Contains variable declarations |
| output.tf | Contains outputs from resources |
| Provider.tf | Contains provider Definition |

## Multiple Providers

We can use multiple providers in same `.tf` file.
Example: 
```hcl
resource "local_file" "pet" {
    filename = "D:\\temp\\example.txt"
    content = "Initial file from terraform"
    file_permission = "0700"
}

resource "random_pet" "test_pet" {
    prefix = "Mrs"
    seperator = "."
    length = 2
}
```

On running `terraform init`, terraform will download both of the providers mentioned in the above example. (local and random)
Information on Random provider available at: https://registry.terraform.io/providers/hashicorp/random/latest/docs

```sh
Initializing provider plugins...
- Finding latest version of hashicorp/random...
- Finding latest version of hashicorp/local...
- Installing hashicorp/random v3.4.3...
- Installed hashicorp/random v3.4.3 (signed by HashiCorp)
- Installing hashicorp/local v2.2.3...
- Installed hashicorp/local v2.2.3 (signed by HashiCorp)
```

Now we can run plan and apply to create those resources. We can add any number of resources in a terraform configuration file.

## Input Variables

- In example configuration files the argument values are hardcoded.
- These values can be placed in a separate file named as `variables.tf`, can be referenced from there.
- A new variable can be crenelated as below

```hcl
variable "filename" {
    default = "D:\\temp\\example.txt"
}
```

- It can be referenced as `var.filename`
An example `main.tf` and its corresponding `variables.tf` file is shown below

```hcl
resource "local_file" "pet" {
    filename = var.filename
    content = var.content
    file_permission = var.file_permission
}

resource "random_pet" "test_pet" {
    prefix = var.prefix
    separator = var.seperator
    length = 2
}
```

```hcl
variable "filename" {
    default = "D:\\temp\\example.txt"
}

variable "content" {
    default = "Initial file from terraform"
}
 
variable "file_permission" {
    default = "0700"
}  

variable "prefix" {
    default = "Mrs"
}  

variable "seperator" {
    default = "."
}
```

## Variable Block

- A simple variable block contains a default value other than that we can add type and description
```hcl
variable "filename" {
	default = "/root/example.txt"
	type = string
	description = "Used to specify the path of file"
}
```

### Arguments

Terraform CLI defines the following optional arguments for variable declarations:

- default - A default value which then makes the variable optional.
- type - This argument specifies what value types are accepted for the variable.
- description - This specifies the input variable's documentation.
 - validation - A block to define validation rules, usually in addition to type constraints.
 - sensitive - Limits Terraform UI output when the variable is used in configuration.
 - nullable - Specify if the variable can be null within the module.

### Custom Validation Rules

> This feature was introduced in Terraform CLI v0.13.0.

You can specify custom validation rules for a particular variable by adding a `validation` block within the corresponding `variable` block. The example below checks whether the AMI ID has the correct syntax.

```hcl
variable "image_id" {
  type        = string
  description = "The id of the machine image (AMI) to use for the server."

  validation {
    condition     = length(var.image_id) > 4 && substr(var.image_id, 0, 4) == "ami-"
    error_message = "The image_id value must be a valid AMI id, starting with \"ami-\"."
  }
}
```
 
> [! Info]
> type, description are optional fields

### Type of variables allowed
- `string`
	-  `/root/pets.txt` can be fetched by `var.variablename`
- `number`
	- `1` can be fetched by `var.variablename`
- `bool`
	- `true` can be fetched by `var.variablename`
- `list (<TYPE>)``
	- List can be specified with type as `type = list(string)` then it will only allow string
```hcl
#variables.tf
variable "prefix" {
	default = ["Mr", "Ms", "sir"]
	type = list
}

#main.tf
resource "random_pet" "test_pet" {
    prefix = var.prefix[0]
    separator = var.seperator
    length = 2
}
```

- `set(<TYPE>)`
	- Set also same as list except the values will not have duplicates
	- Set can be specified with type as `type = set(string)` then it will only allow string
- `map(<TYPE>)`
	- map can be specified with type as `type = map(string)` then it will only allow string
```hcl
#variables.tf
variable "prefix" {
	default = {
		 "coma_seperator" = ","
		 "period_seperator" = "."
 }
	type = map
}

#main.tf
resource "random_pet" "test_pet" {
    prefix = var.prefix["period_seperator"]
    separator = var.seperator
    length = 2
}
```
- `object({<ATTR NAME> = <TYPE>, ... })`
	- object type is used when a group of parameters need to be specefied example
```hcl
#variables.tf
variable "bella" {
	type = object ({
		name = string
		color = string
		age = number
		food = list(string)
		favorite_pet = bool
	})
	default = {
		name = "bella"
		color = "brown"
		age = 4
		food = ["fish", "chicken", "turkey"]
		favorite_pet = true
	}
}
```
- `tuple([<TYPE>, ...])`
	- tuple is similar to list but a specified number of fields and their types will be mentioned
```hcl
#variables.tf
variable "kitty" {
	type = tuple([string, number , bool])
	default = ["cat", 5, true]
}
```

> [!Note]
> If we provide incorrect type terraform plan and apply will fail specifying the error that type is not correct.

## Using Variables while running terraform

- Interactive form
	- When the default value is not provided in `variables.tf`
	- Terraform will ask for those values in an interactive form on running plan or apply.
- Command Line Flags
	- variables can also be passed as command line arguments as below
	```sh
	terraform apply -var "filename=/root/pets.txt" -var "content=example text" -var "prefix=Mr"
	```
- We can set the variables as environment variables as show below
	- The above used variables can be
	```sh
	export TF_VAR_filename="/root/pets.txt"
	export TF_VAR_content="example content"
	export TF_VAR_prefix="Mr"
	```
- Variables can be place in a file in the same folder as configuration folder with name `terraform.tfvars` or `terraform.tfvars.json`
	- Example file content is mentioned below
	```
	filename="root/pets.txt"
	content="example text"
	prefix="Mr"
	```
	> [!Note]
	> To automatically load variable file names can be named with any name with extension `*.auto.tfvars` or `*.auto.tfvars.json*` 

## Variable Definition Precedence

The above mechanisms for setting variables can be used together in any combination. If the same variable is assigned multiple values, Terraform uses the _last_ value it finds, overriding any previous values. Note that the same variable cannot be assigned multiple values within a single source.

Terraform loads variables in the following order, with later sources taking precedence over earlier ones:

-   Environment variables
-   The `terraform.tfvars` file, if present.
-   The `terraform.tfvars.json` file, if present.
-   Any `*.auto.tfvars` or `*.auto.tfvars.json` files, processed in lexical order of their filenames.
-   Any `-var` and `-var-file` options on the command line, in the order they are provided. (This includes variables set by a Terraform Cloud workspace.)

## Resource Attributes

```hcl
resource "local_file" "pet" {
    filename = var.filename
    content = "The pet that is generated is tobe replaced"
    file_permission = var.file_permission
}

resource "random_pet" "test_pet" {
    prefix = var.prefix
    separator = var.seperator
    length = 2
}
```

- If we want to use the id generated by random pet resource to be used in the `local_file` resource
- The name of the pet generated will be with name id so we can use interpolation syntax as below. `${random_pet.test_pet.id}`

```hcl
resource "local_file" "pet" {
    filename = var.filename
    content = "The pet that is generated is ${random_pet.test_pet.id}"
    file_permission = var.file_permission
}

resource "random_pet" "test_pet" {
    prefix = var.prefix
    separator = var.seperator
    length = 2
}
```

- Terraform will use **implicit dependency** while creating and deleting these resources.
- We do not have to mention the order in which the resources need to be deleted or created.
- Terraform is intelligent enough to create `test_pet` first and then pet.

### Explicit Dependency

If we want to run generate few resources before moving on to another we can use `depends_on` tag.

```hcl
resource "local_file" "pet" {
    filename = var.filename
    content = "The pet that is generated is auto generated"
    file_permission = var.file_permission
    depends_on = [
	    random_pet.test_pet
    ]
}

resource "random_pet" "test_pet" {
    prefix = var.prefix
    separator = var.seperator
    length = 2
}
```


## Output Variables

- A variable which will be generated as part of resource creation can be added to output variable.
- Example the id generated as per the `test_pet` can be added to output block.
- An output stanza can be added as below

```hcl
output pet_name {
    value = random_pet.test_pet.id
    description = "The pet name that will be created as part of test_pet generation"
}
```

To get the values of output parameters
#terraform-output
```sh
# To get the output varaibales that are added in output stanza
terraform output
# To get a specific variable provide the varaible name as below
terraform output pet_name
```
