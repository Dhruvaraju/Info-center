# Version Constraints for provides
- Terraform uses plugin based arch to get providers locally
- Without providing an version to download terraform will download the latest version of a provider.
- To get a specific version of provider we have to add a new block in the config file called `terraform` under which we have to add `required_providers` section mentioning the provider the source from where we can get it and  version required example provided below

```hcl
terraform {
  required_providers {
    local = {
      source = "hashicorp/local"
      version = "2.2.3"
    }
  }
}

provider "local" {
  # Configuration options
}

resorce "local_file" "cars"{
	filename = "cars.txt"
	content = "example car"
}
```

- We can also perform operation on versions
	- if we don not want a specific version we can use `version = "!= 2.0.0"`
	- if version higher than `2.0.0` `version= "> 2.0.0"`
	- if version less than `2.0.0` `version= "< 2.0.0"`
	- if version range then  `version= "< 2.0.0, > 1.2.0, != 1.2.4"` this will get version between 1.2.0 and 2.0.0 but not 1.2.4
	- we can also user `~` which will load the nearest pessimistic version example `~>1.2` will get anything above 1.2 up till 1.9 