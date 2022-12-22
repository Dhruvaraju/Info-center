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

![sample.png](sample.png)

Above example is for resource type local