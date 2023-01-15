# Terraform functions

- `file()`Used to load content from a file
- `length()` : to find the length of a map, set or list
- `toset()` to convert a list to set
- We can play with the function using the state of current configuration from terminal using the `terraform console` command.
- We can now run the file() and other functions with proper syntax to check if they are working as expected.

There are many more functions available, documentation for the same is present at: https://developer.hashicorp.com/terraform/language/functions

## Conditional expressions

We can make use of conditional expressions while using terraform configuration
Syntax `condition ? true_value : false_value`

```hcl
resource "random_password" "generatedpwd"{
	length = var.pwd-length < 8 ? 8 : var.pwd-length
}

variable "pwd-length"{

}
```