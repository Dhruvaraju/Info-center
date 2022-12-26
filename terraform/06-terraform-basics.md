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