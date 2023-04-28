# Vault Authentication Methods
#auth_methods

- Any auth method is used to get a vault token to perform other operations.
- Tokens are general method of authentication with vault.
- Most operations in vault require an existing token.
- Token auth method is responsible for creating and storing tokens.
- Token auth method cannot be disabled.

Auth method workflow:

User -> Authentication with credentials to vault -> vault -> vault validates against provider -> vault generates token with policy and attach time to live -> vault will sent the generated token back -> user can use the token to request secrets for user.

