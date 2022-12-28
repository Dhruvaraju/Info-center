# Command reference for Terraform

> All the commands need to be run in the folder where the configuration is created.

#terraform-version
```sh
#To identify version of terraform
terraform version
```

#terraform-init
```sh
# To initate a resource type and download required files
terraform init
```

#terraform-plan
```sh
# To check what kind of resource and corresponding files generated without creating them
terraform plan
```

#terraform-apply
```sh
# To create the resources mentioned in the configuration
terraform apply
```

#terraform-destroy
```sh
# To remove the resources mentioned in the configuration
terraform destroy
```

#auto-approve
```sh
# To run terraform apply without aasking for permission
terraform apply -auto-approve
```

#terraform-output
```sh
# To get the output varaibales that are added in output stanza
terraform output
# To get a specific variable provide the varaible name as below
terraform output pet_name
```