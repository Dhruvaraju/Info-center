## Vault Components

Below mentioned are the core components of vault.

### Storage Backends
#storage-backend
Place where vault stores it's data in encrypted form, In an enterprise environment generally it will be raft or consul. Other cases it will be some data base.
- Configures Location for storage of vault data
- Storage configuration is defined in the main vault configuration file with desired parameters.
- All data is encrypted in transit with TLS and at-0rest using AES256.
- Depending up on the storage backend chosen we can get high availability, or tools for management and data protection.
- There will be only one storage back-end per vault cluster.

### Secret Engines
#secret-engine
Basically the heart of what vault does, vault is being used to make use of secret engines. These store, encrypt or generate data. 
- These are responsible for managing the secrets for your organization.
- Secret engines can store, generate or encrypt data
- Secret engines connect to other services to generate dynamic credentials on-demand.
- Many secret engines can be enables and used as per the requirement
	- Even multiple secret engines of same type can be enabled with different paths
- Secret engines are enabled and isolated at a "path"
	- All interactions are done directly with the path

### Authentication methods
#auth-method
In order to use secret engines we need to authenticate first with vault, There are multiple ways to authenticate with vault. Once authenticated a token will be generated to access secret engines.
- These components perform authentication and manage identities.
- Responsible for assigning identity and policies to users.
- Multiple authorization methods can be enabled based on requirement
	- authorization methods can differentiate human vs machine
- Once authenticated a token will be issued which can be used to perform future operations.
	- main aim of all authorization methods is t get a token.
	- Each token will have an associated policy or policies and a time to live (TTL)
- Default authentication method for a new vault deployment is **tokens**

### Audit Devices
#audit-device
As vault is a security software we need audit devices to make sure everything is 100% audited and logged properly.
- These keep a detailed log of all requests and responses to a Vault.
- Audit log is formatted using a JSON
- Sensitive information is hashed before logging
- It is preferred to have more than one audit enabled devices
	- Vault requires at least one audit device to write the log before completing the Vault request - If an audit device is enabled.
	- Vault prioritizes safety over availability, meaning if it is not able to write a log due to some issues like insufficient storage for logs it will not respond to request.

## Vault Architecture and Pathing Structure

![vault-architecture](images/vault-architecture.png)

The center part which is encapsulated in the Barrier are the components inside vault. To access vault a HTTP/s api is available, to store data from vault an external storage backend will be used like consul or PostgreSQL or MySQL.

To access Vault the api should get authenticated or it should have a token.

## vault paths
- Everything in vault is path based
- Path prefix helps vault to understand which component a request need to be routed.
- Secret engines, auth methods, and audit devices are mounted at a specified path
	- These are often referred as a mount.
- paths available are dependent on the features enabled in the vault like auth methods and secret engines.
- System backend is a default backend  in vault which is mounted at the `/sys` endpoint.

- vault components can be enabled at any path as per your desire using the `-path` flag
	- Each path has a `default path`, which can also be used.
- Some paths are system reserved and they cannot be used or removed.

| Path Mount Point | Description |
| --- | --- |
| auth/ | Endpoint for auth method configuration |
| cubbyhole/ | Endpoint used to Cubbyhole secrets engine |
| identity/ | Endpoint for configuring Vault identity (entities and groups) |
| secret/ | Endpoint used by key/Value v2 secrets engine if running in dev mode |
| sys / | System endpoint for configuring Vault |

## How do vault protect data?
#encryption-key #master-key
- Vault saves all the data in storage backend
- Data stored in backend is encrypted by an `encryption key`
- This `Encryption key` is stored on vault node.
- Before storing encryption key on vault node, `Encryption key` is encrypted using a `master key`

### Master Key

Used to decrypt the `EncryptionKey`

- Created during vault initialization or during a rekey operation
- Never written to storage when using traditional unseal mechanism
- Written to core/master (storage backend) when using Auto Unseal

### Encryption Key

Used to encrypt/decrypt data written to storage backend

- Encrypted by master key
- Stored alongside the data in a keyring on the storage backend
- Can be easily rotated (Which is a manual operation)

## Seal and Unseal

- Vault always starts in a sealed state that means, it knows where to access the data, and how, but can't decrypt it.
- Almost no operations are possible when vault is in a sealed state. Only the below operations are possible
	- Only status check (Meaning is it in sealed on unsealed state)
	- Unsealing a vault 
- Unsealing the vault means the node can reconstruct the master key in order to decrypt the encryption key, and ultimately read the data.
- After unsealing the encryption key is stored in the memory.

**Sealing vault:** Means Vault throws away the encryption key and requires another unseal to do any further operation

> Vault starts in a sealed state, you can also seal it via UI, CLI or API.

## What is the need of sealing a vault?

- Key shards are inadvertently exposed (As of now think key shards  means your some credentials)
- Detection of a compromise or network intrusion.
- Spyware/malware on the Vault nodes

### Unsealing Options:

- Key Sharding (Using Sharmir algorithm) 
- Cloud Auto Unseal (can use AWS KMS)
- Transit Auto Unseal (With help of another Vault cluster or nodes)

## Un Sealing with Key Shards
#shards #unseal
- Vault data >> protected by Encryption key >> Encryption key is encrypted by  Master key
- Master key is broken into 5 pieces with **Shamir's secret sharing Algorithm** these are called as key **shards or unseal keys.**
- To unseal a Vault we need a threshold of keys generally it will be 3 out of 5
- Once we provide any 3 keys vault will generate master key from it and use it to generate encryption key, which in turn is used to encrypt or decrypt vault data.

To get status of vault use `vault status` it will give information such as 
- Seal type eg: Shamir
- Sealed true or false
- Total share which is number of shards
- Threshold : number of keys required to unseal vault
- Unseal progress: Number of shards provide so far to unseal Vault

After providing the keys:
Once Vault is unsealed it will provide additional details such as:
- Vault version
- Storage type: Storage backend type
- Cluster Name: Name of Vault cluster
- Cluster ID: Which is the autogenerated ID of the cluster
- HA Enabled: true or false (High Availability mode enabled or not)

- Unsealing with key shards is the default option - No additional configuration required
- No Single person should have access to all key shards.
- Ideally each key shard should be stored by a different employee.
- While initializing Vault, you can request the individual shards to be encrypted with different PGP keys.
- Key shards should not be stored online and should be highly protected ideally stored encrypted.

### Basic commands used:

- To get vault status `vault status`
- To read the configuration file use `cat /etc/vault.d/vault.hcl` Initially there will not be any configuration related to sealing.
- To initialize vault cluster use `vault operator init` #vault_init
	- Once the command is executed we will get the 5 unseal keys and Initial root token to access vault
- To provide unseal keys use `vault opreater unseal` Vault will ask for shards, provide any one of the shards.
- After threshold is met, we should be able to get an unsealed status and we can start interacting with vault.
- To log in to vault use `vault login <<token>>` #vault_login
- To get list of secrets engine: `vault secrets list` #vault_secrets_list

## Unsealing with Auto Unseal
#auto_unseal #cloud_kms

- Vault Data -> encrypted by Encryption Key -> Encrypted key will be encrypted by Master Key -> Master key will be encrypted by a Key generated with Key generated with Cloud Key management Service (KMS)
- Master key will ne stored on Storage backend with vault data.
- Encryption key will be stored on Vault node.

- Auto unseal uses a cloud or on-premises HSM to decrypt the master key #one-prem_hsm
- Vault configuration file identifies the particular key to use for decryption
- Cloud Auto Unseal automatically unseals Vault upon service or node restarts.
- This option is available in both open source and enterprise editions
- This was a Enterprise option only until Vault 1.0 version

Requires an config file update:
The following section (seal stanza) need to be added without the comments

```
seal "awskms" { # identefies the type of seal mechanism for cluster
 region = "REGION" # Identefies the region where KMS key resides
 ksm_key_id = "KMSKEY" # Identefies the actual KMS key in AWS
}
```

- Got to any cloud key management system, create a key and copy those details to vault config
-  Once the config is updated, seal type will be changed to Recovery seal type.
- Initialize the vault with  `vault operator init`
- We will get 5 Recovery keys and a root token to perform operation on Vault.
- These 5 keys can be used when the vault is manually sealed.

## Unsealing with Transit Auto Unseal