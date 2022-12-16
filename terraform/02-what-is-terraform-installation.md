### What is Terraform?
#terraform

- An infrastructure automation tool, which is open source and vendor agnostic. Meaning it works with many vendors, it doesn't matter which vendor we are using.
- The source file is a single binary compiled from Go Lang.
- It uses declarative syntax.
- Configuration files are written in Hasicorp configuration language (extension `.tf`) or JSON.
- It follows push based deployment style.

### Core components of Terraform
- Executable which is the source code itself.
- Configuration files (HCL or Json)
- Provider plugins (Cloud provider plugins)
- State Data (Terraform maintains state files which will say the current situation of an environment that a component is provisioned to.)


## IAC
Types of iac models