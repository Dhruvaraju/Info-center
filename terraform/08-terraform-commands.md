# Terraform Commands

Few useful commands which can be used 
- `terraform validate` #terraform_validate
	- Even with out running plan or init, `terraform validate` can be used to see if the syntax is proper or not. If the validation is successful it will show a `Success` message. Else it will show the location where error occurred.
- terraform fmt #terraform_fmt
	- Used to format terraform configuration files for better readability
- terraform show #terraform_show
	- Will  list all the attributes under each resource 
	- `-json` switch can be used to display the same in json format
- terraform providers #terraform_provider
	- Will list all the providers that are being used in the configuration files
	- mirrors can be used to copy the providers to a different folder.
	- `terraform providers mirror <destination_folder>`
- terraform output #terraform_output
	- Used to display all the output variables in a configuration
	- specific variable related information can be found by passing variable name to `terraform output`
- terraform refresh #terraform_refresh
	- Used to update the current state of the resource with the state file maintained by terraform
	- Mainly used when the resource is updated out of the purview of terraform
	- refresh can be turned off by passing `-refresh=false` switch
- terraform graph #terraform_graph
	- can be used to get the relationship graph of each resources in the configurations used.
	- This will provide in a dot format.
	- the graph format can be visualized with `graphviz` which can be installed as `apt install graphviz -y`
	- `terraform graph | dot -Tsvg > graph.svg`
