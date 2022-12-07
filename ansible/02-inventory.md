# Configuring an inventory

Ansible can work with one or more number of machine in an environment, in order to work with multiple servers ansible should maintain connectivity to those servers. This is done with help of
 - ssh for Linux
 - PowerShell remoting with windows.

- Working with ssh and winrm (windows remoting aka PowerShell remoting) makes ansible agentless.
- Agentless meaning we do not have to install anything additional on target machines specific to ansible to work with ansible.
- Other orchestration tools need some sort of agent to be installed in target machine.

## Inventory file
- Details about the target systems are stored in a file called inventory file.
- If inventory file is not specified a default inventory file is created by ansible.
- Default ansible inventory file location is `/etc/ansible/hosts`

- Inventory file uses an ini format by default
- Group name is mentioned in `[]` we can have multiple groups in a inventory file.

```
server1.company.com
server.company.com

[mail]
mail.server1.com
mail.server2.com

[db]
db.server.com
db.server2.com
```

## Inventory parameters

- if we want to refer to a target machine with an alias we can add it at the beginning of entry in inventory and mention the server address as `ansible_host`
- `ansible_host` is an inventory parameter which will specify target server
- Target server connection type can be specified using `ansible_connection`
- Port number can be specified using `ansible_port`
- user name for connecting to target machine can be provided with `ansible_user`
- ssh pass word can be provided using `ansible_shh_pass`

### Possible values and default values for inventory parameters

- `ansible_connection`
	- `ssh`/`winrm`/`localhost`
	- for Linux default is ssh
- `ansible_port`
	- 22 / 5986
	- default 22 for Linux
- `ansible_user`
	- root / administrator
	- root is default for Linux
- `ansible_ssh_pass`
	- no default plain text password is not recommended

**Example**

```text
web ansible_host=server1.company.com ansible_connection=ssh ansible_user=root
db ansible_host=server2.company.com ansible_connection=ssh ansible_user=admin
mail ansible_host=server3.company.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=P@$$
web2 ansible_host=server4.company.com ansible_connection=winrm

# Use this when you need to work with local machine
localhost ansible_host=localhost
```
