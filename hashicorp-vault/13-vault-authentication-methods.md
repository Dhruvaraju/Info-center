# Vault Authentication Methods
#auth_methods

- Any auth method is used to get a vault token to perform other operations.
- Tokens are general method of authentication with vault.
- Most operations in vault require an existing token.
- Token auth method is responsible for creating and storing tokens.
- Token auth method cannot be disabled.

Auth method workflow:

User -> Authentication with credentials to vault -> vault -> vault validates against provider -> vault generates token with policy and attach time to live -> vault will sent the generated token back -> user can use the token to request secrets for user.

- Enable auth method before starting using vault
- One or many auth methods can be used at same time.
- Token auth method is enabled by default it cannot be enabled or disabled .
- New vault deployments will use token for authentication.
- Only method for authentication for a new vault deployment is root token

Auth Methods
- Each auth method is enabled at a path
- If name is not provided the default path is used.
- Example if aws auth method is configured without a name then its path will be by default aws

```sh
vault auth enable approle
Enabled approle at path approle/
```

