# Running Vault Server

## Running Vault in Dev server mode

> Never use vault in dev server mode in production

To start vault in dev server mode use 
```sh
vault server -dev
```

- Using dev server we can start vault without providing any configuration.
- Vault will be automatically initialized and unsealed.
- Automatically enables the UI at localhost
- Provides an unseal key.
- Automatically logs you in as root user.
- The data you store in is non persistent and runs in memory.
- Insecure as it does not use TLS
- By default sets the listener to `127.0.0.1:8200` 
- Mounts a Key value secrets engine to the path /secret
- Provides a Root Token

### Use cases for dev server 
- Proof of concepts
- New development integrations
- Testing new features of vault
- Experimenting of features.

After starting vault with `vault server -dev`, We need to set a variable `VAULT_ADDR` as shown below to start using vault.

PowerShell:
    $env:VAULT_ADDR="http://127.0.0.1:8200"
cmd.exe:
    set VAULT_ADDR=http://127.0.0.1:8200

We can run `vault status` it will provide result similar to
```sh
Key             Value
---             -----
Seal Type       shamir
Initialized     true
Sealed          false
Total Shares    1
Threshold       1
Version         1.12.1
Build Date      2022-10-27T12:32:05Z
Storage Type    inmem
Cluster Name    vault-cluster-66b4b371
Cluster ID      80c91023-91be-0545-8507-e2b8886eddc7
HA Enabled      false
```

We can see the secret engine list as `vault secrets list`
```sh
C:\Users\dhruv>vault secrets list
Path          Type         Accessor              Description
----          ----         --------              -----------
cubbyhole/    cubbyhole    cubbyhole_3114f973    per-token private secret storage
identity/     identity     identity_fdf58e60     identity store
secret/       kv           kv_1665ee71           key/value secret storage
sys/          system       system_089791ec       system endpoints used for control, policy and debugging
```

By default it will enable the key/value secrets engine

We can add a key/value by using a path as below.
```sh
vault kv put secret/example/dexter dexter=miami
```
To get the key back we can use the command
```sh
vault kv get secret/example/dexter
```

> As the dev mode will provide only storage backend as in-memory on restart the data will be lost

## Running Vault in Production Mode

- Deploy one or more persistence nodes via configuration file.
- Use a storage backend that meets the requirements
- Multiple Vault nodes will be configured as a cluster.
- Deploy close to you applications, meaning use the same cloud provider for storage and hosting as well.
- Automate provisioning of vault if possible.

To start Vault use command
```sh
vault server -config=<file>
```

- In a production environment we will have a service manager executing and managing the vault service (systemctl, Windows Service Manager)
- For Linux we also need a systemd file to manage the service for Vault (and Consul if we are using consul)
- Not recommended to use a single node
	- No redundancy
	- No Scalability

### Running Vault in production

- [ ] Download vault from HashiCorp vault
- [ ] Unpackage vault to a directory
- [ ] Set path to Executable
- [ ] Add configuration file and Customize
- [ ] Create Systemd service File
- [ ] Download Consul from HashiCorp
- [ ] Configure and Join Consul Cluster
- [ ] Launch Vault Service

Place vault service file in `/etc/systemd/system`
Vault configuration file or `vault.hcl` can be added at `/etc/vault.d/`
To start vault `sudo systemctl start vault`

## Example Vault.service file

```
[Unit]
Description="HashiCorp Vault - A tool for managing secrets"
Documentation=https://www.vaultproject.io/docs/
Requires=network-online.target
After=network-online.target
ConditionFileNotEmpty=/etc/vault.d/vault.hcl
StartLimitIntervalSec=60
StartLimitBurst=3

[Service]
User=vault
Group=vault
ProtectSystem=full
ProtectHome=read-only
PrivateTmp=yes
PrivateDevices=yes
SecureBits=keep-caps
AmbientCapabilities=CAP_IPC_LOCK
Capabilities=CAP_IPC_LOCK+ep
CapabilityBoundingSet=CAP_SYSLOG CAP_IPC_LOCK
NoNewPrivileges=yes
ExecStart=/usr/local/bin/vault server -config=/etc/vault.d/vault.hcl
ExecReload=/bin/kill --signal HUP $MAINPID
KillMode=process
KillSignal=SIGINT
Restart=on-failure
RestartSec=5
TimeoutStopSec=30
StartLimitInterval=60
StartLimitIntervalSec=60
StartLimitBurst=3
LimitNOFILE=65536
LimitMEMLOCK=infinity

[Install]
WantedBy=multi-user.target
```