## Data-sources

Information read from a resource which is created by some other way, other than using the terraform script in the current configuration folder.

Example a file is created with help of terraform and another file manually we can ready the information of the other file using data source in the below example example.txt is created by terraform and manual.txt is created manually.

```hcl
resource "local_file" "myfile"{
  filename        = "D:\\temp\\example.txt"
  content         = data.local_file.myfile.content
}

data "local_file" "manual" {
 filename = "D:\\temp\\manual.txt"
}
```

Details that can be used as data source can be found at HashiCorp documentation for each resource type.

- Resource
	- keyword `resource`
	- Used to create, update destroy infrastructure
	- aka managed resource
- Datasource
	- keyword `data`
	- Only to read infrastructure
	- aka data resource

## Meta Arguments

- When we have to create  multiple instances of same resources, we use meta arguments.
- Meta arguments can be used in any resource blocks
- Example for meta arguments: `depends_on`, `lifecycle`

### Count

Count can be used to create multiple instance of same resource example:
```hcl
resource "local_file" "ev" {
  filename = var.filename[count.index]
  content  = "example content"
  
  count    = 3
}

variable "filename" {
  default = ["d:\\temp\\alpha.txt", "d:\\temp\\beta.txt", "d:\\temp\\omega.txt"]
}
```

- On running terraform apply it will create 3 files.
- If we remove the first fi
