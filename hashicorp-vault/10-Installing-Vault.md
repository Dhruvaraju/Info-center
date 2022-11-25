# Installing Vault

Vault is platform agnostic, it can be run on many different underlying platforms. like

	- Kubernetes
	- Cloud based machines (AWS Instances or Azure Virtual Machines)
	- VMware virtual machines
	- Physical servers
	- A lap top

Vault is available on may operating systems like, Windows, MacOS, Linux, FreeBSD, NetBSD, OpenBSD, Solaris.

## Steps followed while installing Vault

1) Install Vault
2) Create Configuration File
3) Initialize Vault
4) Unseal Vault

## How to install Vault

- We can get vault from
	- vaultproject.io
	- releases.hashicorp.com/vault
- Vault can be downloaded from package manager like apt, yum, even or homebrew
- Commands can be found for installing vault at https://www.vaultproject.io/downloads
- To install or configure vault on kubernetes use `helm install vault hashicorp/vault`

## Installing with Packer

> Add all other options to install vault

Predefined scripts can be found at https://github.com/btkrausen/hashicorp

For installing vault https://github.com/btkrausen/hashicorp/tree/master/vault/packer

Github repo btkrausen/hashicorp
- Contains information regarding many HashiCorp products.
- For Vault related installation procedures and other examples refer to vault folder.

## Installing Manually

Vault can be downloaded from https://developer.hashicorp.com/vault/downloads?product_intent=vault
Alternatively we can go to https://releases.hashicorp.com
For Vault versions we can use https://releases.hashicorp.com/vault/

- Choose the most recent version and copy the url for it

```sh
curl --silent -Lo /tmp/vault.zip https://releases.hashicorp.com/vault/1.12.1/vault_1.12.1_windows_amd64.zip
```

- Or Download the binary for your OS
- Extract it, place it in a desired location.
- Update the system path in windows
- In Linux place it in `/usr/local/bin`

Check version by using `vault --version`