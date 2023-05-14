 ## Running a vault dev server:

```
vault server -dev
```

- Vault will continue to run in foreground, so use another terminal to connect to it.
- Vault will provide unseal key, root token and a local address where vault is running 

- run `set VAULT_ADDR=http://127.0.0.1:8200` to set the vault address and save your root and unseal key somewhere.
- Set the vault root token also as a variable `set VAULT_DEV_ROOT_TOKEN_ID=<root_token>`
- or set the root token to `VAULT_TOKEN`

### Interacting with vault
adding a secret
```sh
vault kv put -mount=secret hello foo=world
```

getting a secret
```sh
vault kv get -mount=secret hello
```

deleting a secret:
```sh
vault kv delete -mount=secret hello
```

Enabling a new secrets engine on path kv
```
vault secrets enable -path=kv kv
```

to get list of all secret engines:

```
vault secrets list
```

To disable a secrets engine
```sh
vault secrets disable kv/
```