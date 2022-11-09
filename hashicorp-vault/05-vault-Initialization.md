# Vault Initialization

- Initializing the vault will prepare the backend storage to receive data
- Only need to initialize a vault cluster one time via a single node 
- Vault Initialization is when the vault create master key and key shares.
- During Vault initialization we have options to define thresholds, key shares, recovery keys and encryption.
- Vault initialization is also where the initial root token is generated and returned to the user.
- Vault can be initialized via CLI, API or UI

Command used to initialize vault is

```
vault operator init <options>
```