# Vault Interfaces

- Three interfaces are available to interact with vault
	- UI
	- CLI
	- HTTP API
- Not all the vault features are available via UI and CLI.
- All the Vault features are available with HTTP api.
- Calls from CLI and UI invoke the http api.
- CLI is a wrapper over http api
- UI must be enabled over configuration file, before using it.
- Authentication is required for using any of the interfaces.

## Vault Users and which interface they use

- Humans
	- User Interface
	- Command Line
- Orchestration services
	- Command Line
	- HTTP API
- Applications
	- HTTP API