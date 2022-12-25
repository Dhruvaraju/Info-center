# Update a Resource
- Update the  configuration 
- Run `terraform plan` to see what will happen
- Run `terraform apply` for applying new configuration, creating updated resource.

### Example updating file permission
Update configuration as below
```hcl
resource "local_file" "pet"{
	filename = "D:\\temp\\example.txt"
    content = "Initial file from terraform"
    file_permission = "0700"
}
```

**`terraform plan` output**

```sh
local_file.pet: Refreshing state... [id=afb2ad235663ca4d4901802d057d9cbe10911337]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
-/+ destroy and then create replacement

Terraform will perform the following actions:

  # local_file.pet must be replaced
-/+ resource "local_file" "pet" {
      ~ file_permission      = "0777" -> "0700" # forces replacement
      ~ id                   = "afb2ad235663ca4d4901802d057d9cbe10911337" -> (known after apply)
        # (3 unchanged attributes hidden)
    }

Plan: 1 to add, 0 to change, 1 to destroy.

──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```

- The file will be removed then recreated again with the given permissions.

**`terraform apply` output**

```sh
local_file.pet: Refreshing state... [id=afb2ad235663ca4d4901802d057d9cbe10911337]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
-/+ destroy and then create replacement

Terraform will perform the following actions:

  # local_file.pet must be replaced
-/+ resource "local_file" "pet" {
      ~ file_permission      = "0777" -> "0700" # forces replacement
      ~ id                   = "afb2ad235663ca4d4901802d057d9cbe10911337" -> (known after apply)
        # (3 unchanged attributes hidden)
    }

Plan: 1 to add, 0 to change, 1 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

local_file.pet: Destroying... [id=afb2ad235663ca4d4901802d057d9cbe10911337]
local_file.pet: Destruction complete after 0s
local_file.pet: Creating...
local_file.pet: Creation complete after 0s [id=afb2ad235663ca4d4901802d057d9cbe10911337]

Apply complete! Resources: 1 added, 0 changed, 1 destroyed.
```

## Destroy resource

- use `terraform destroy` to remove a resource

**`terraform destroy` output**

```sh
local_file.pet: Refreshing state... [id=afb2ad235663ca4d4901802d057d9cbe10911337]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # local_file.pet will be destroyed
  - resource "local_file" "pet" {
      - content              = "Initial file from terraform" -> null
      - directory_permission = "0777" -> null
      - file_permission      = "0700" -> null
      - filename             = "D:\\temp\\example.txt" -> null
      - id                   = "afb2ad235663ca4d4901802d057d9cbe10911337" -> null
    }

Plan: 0 to add, 0 to change, 1 to destroy.

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

local_file.pet: Destroying... [id=afb2ad235663ca4d4901802d057d9cbe10911337]
local_file.pet: Destruction complete after 0s

Destroy complete! Resources: 1 destroyed.
```