### Infrastructure as code
#infrastructure_as_code #Iac

> [!Info]
> Provisioning infrastructure through software to achieve consistent and predictable deployments is called as infrastructure as code.

### Few concepts of Iac
- **Define it in code**, meaning convert the infrastructure configuration in json, yaml or hasicorp language.
- **Store the files in SCM**, as the files are considered as software store them in version control.
- **Declarative or Imperative**
- Idempotent and consistent configuration.
- push or pull a configuration.

### Imperative vs Declarative 
Imperative way | Declarative way
---- | ----
Where we will define each component we need. The steps to assemble these to create a final component. | We say type of final component required and supply the sub components required

**Example:**
**Imperative way to make a taco**
- get shell
- get beans
- get cheese
- get salsa

**Steps to assemble:**
- put beans in shell
- put cheese on beans
- put lettuce on cheese
- put salsa on lettuce

**Declarative way of making a taco:**

```
food taco "bean-taco" {
	ingredients = ["beans", "cheese", "lettuce", "salsa"]
}
```

It is asking to prepare taco of type food and it is specifically bean-taco, with the provided ingredients. The steps and implementation will be taken care of.

**Idempotent :** 

Consider an example where a person asks for a taco and we make them one, but the same person asks for an another taco. In ideal world we will give them a new one, but since the person has a taco already we do not provide another.

So if and when a component is requested from Terraform, if it senses that the requirement is already met in an environment it will not provision it. ==Hence Terraform in idempotent==.

### Push or Pull
Considering a taco example, When a person asks for a taco we just **push** the taco towards them. If they are kind enough they will say thank you.

In **pull** scenario they will just ask for a taco and take it from us and we will just say sure take it.

Terraform sends configuration by push. When a environment needs an infrastructure it asks for it and Terraform pushes it.

### Advantages of Infrastructure as code
- Automated Deployments.
- Repeatable process.
- Consistent environments.
- Reusable Components.
- Documented architecture.

> [!note]
> Terraform is declarative, Idempotent and push type.
