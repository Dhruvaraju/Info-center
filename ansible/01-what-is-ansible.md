### What is ansible?
#ansible
- It is an open source configuration management, software provisioning and application deployment tool set.
- Ansible is a multitude of tools, modules and software defined infrastructure, collectively are the ansible tool set.

### Core components of ansible
#### Modules:
- Cloud computing
- Networking
- Server Configuration and Management
- Virtualization
- Containers and much more.

> [!Note]
> There will be a module for every need, if it is not present we can create a module of our own using the ansible framework.

Modules can be found at: https://docs.ansible.com/ansible/latest/collections/index_module.html

#### Ansible Executable
- It is a Swiss army knife with lots of functionalities.
- It can be invoked by typing `ansible` on a machine where it is installed.
- Great for initially setting up a project and testing ansible configuration.
- Easy to use with ansible modules.
- Easy to use with your ansible target infrastructure.

#### Ansible Play book
- Can be invoked by typing `ansible-playbook` at a prompt where ansible is installed.
- Use ansible's human readable configuration deployment and orchestration language to create yml.
- Playbook is a book of plays which means applying a specific configuration to a defined infrastructure.

#### Ansible Inventories
- An inventory of targets.
- It contains Hosts, Network Switches, Containers, Storage arrays and many more physical and virtual devices.
- Inventories provide useful information regarding the targets.