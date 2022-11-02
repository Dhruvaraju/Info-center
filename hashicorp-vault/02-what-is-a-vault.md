## Understanding Vault

## What is a secret?

Anything that is deemed as as sensitive by an organization is considered as secret.
Usernames, passwords, certificates, API keys, Encryption Keys.

## What is Vault?
#vault 

- Vault manages secrets and sensitive data
- Provides a single source of secrets for both humans and machines. Vault has a UI and cli for humans to interact with. it also have an API for machines to interact with. Vault shines more in an automated environment, like pipelines.
- Vault provides a complete lifecycle management for secrets. It is capable of renewing certificates or authentication keys. Setting limits on how much time a key can be used by an api. Provides access controls when secrets are stored across multiple teams.
	- Eliminates secret sprawl
	- Securely store any secret
	- Provides governance for access to secrets.
		- Dev team a can have access to a secret and all other teams can be restricted from accessing it.

## Interacting with Vault

We can interact with vault in 3 ways
1) CLI generally used by machine and humans
2) UI used for human interaction
3) API used by machines for interaction

## Authenticating with Vault
#auth #vault-authentication
- With vault we can authenticate using different ways such as 
	- Username & password
	- Role ID & Secret ID
	- TLS Certificate
	- Integrated Cloud Credentials

Once we authenticate, vault will generate a token which will be valid for a certain time (time to live or TTL). It give you certain privileges' to Read, write, delete and list on certain paths in vault.

After getting a token if we request some data like username & password from a certain path in vault. vault will verify the following:
- Token is valid
- Token is not expired
- Token has permission for the path requested.

If all the above conditions are met then it will send the requested data back.

## Benefits of HashiCorp Vault
#vault-pros
- Strone long-lived static secrets
- Dynamically generate secrets upon a request
- Fully Featured Api
- Identity-based access across different clouds and systems
- Provides encryption as a service
- Act as a root or intermediate certificate authority

## Use cases for vault
#vault-usecases
- Centralize storage of secrets
- Migrate to Dynamically generated secrets
- Secure data with centralized workflow for encryption operations
- Automate the generation of X.509 certificates
- Migrate to identity based access

### Static credential vs Dynamic credentials

#### Static Credentials:

- Valid for 24 / 7 / 365
- Long-Lived
- Manual Password rotation
- Frequently shared across teams
- Reused Across systems
- Susceptible being added to a code repo
- Often highly privileged.
- Manually created by Human.

#### Dynamic Credential

- Short Lived
- Follows principle of least privilege
- Automatically Reevoked (Based on lease)
- Each system can retrieve unique credentials
- Programmatically retrieved
- No human interaction

### Encryption Options

Secret Engines
- Transit
- KMIP
- Key management
- Transform

### Use Case - Automate X.509 Certificates

#### Before vault

Generate CSR >> Enter Ticket for cert creation >> Submit CSR to signing CA >> Retrieve the certificate and Key >> Certificate is returned ticket closed >> Engineer uploads certificate and private key >> Renewal follows the same process.

#### Using vault

App request for a certificate --> Vault acts as a PKI --> Issues certificate and key