# storage backend Configuration

## Consul
#consul #consul_backend

- Consul provides a durable K/V store for vault, vault will store all its data in it.
- Having  separate consul cluster integrated will help in
	- Independently scaling backend as consul runs in its own cluster
	- Easy to automate
	- Built in automation between consul and vault
- Consul brings high availability, distributed systems, built in snapshots for data retentions

### Consul Deployments
#consul_deployment
- Consul itself is deployed as a multi-node cluster
- Generally odd number of nodes will be used.
- Data is replicated across all clusters
- A leader election promotes a single consul as a single consul node cluster

>[!Info] 
>Do not use the consul cluster that is being provisioned for vault backend, to perform any other consul functions (Such as service mesh).

A vault node will have a consul client which will communicate with consul cluster. Hence sequence of operations.

Vault node -> Consul Client -> Consul Cluster.
If a consul node goes down there will note be any impact as there is no direct relation between consul node and a vault node. Consul client default port in vault node will be `8500`

### Example config for consul
#consul_backend_config
```hcl
storage "consul" {
	address="127.0.0.1:8500"
	path="vault/"
	token="I732I5T734CIAWU65847T2L;723T5V-WK3572T35"
}
```

example consul server configuration:
#consul_server_config
```json
{
  "log_level": "INFO",
  "server": true,
  "key_file": "/etc/consul.d/cert.key",
  "cert_file": "/etc/consul.d/client.pem",
  "ca_file": "/etc/consul.d/chain.pem",
  "verify_incoming": true,
  "verify_outgoing": true,
  "verify_server_hostname": true,
  "ui": true,
  "encrypt": "xxxxxxxxxxxxxx",
  "leave_on_terminate": true,
  "data_dir": "/opt/consul/data",
  "datacenter": "us-east-1",
  "client_addr": "0.0.0.0",
  "bind_addr": "10.11.11.11",
  "advertise_addr": "10.11.11.11",
  "bootstrap_expect": 5,
  "retry_join": ["provider=aws tag_key=Environment-Name tag_value=consul-cluster region=us-east-1"],
  "enable_syslog": true,
  "acl": {
   "enabled": true,
   "default_policy": "deny",
   "down_policy": "extend-cache",
   "tokens": {
      "agent": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
   }
},
   "performance": {
    "raft_multiplier": 1
  }
}
```

## Vault with integrated storage

- Integrated storage is vault internal storage option
- It leverages `Raft Consensus Protocol`
- All vault nodes will have a copy of vaults data.
- Eliminates network hops to consul, supports high availability
- Built in snapshots available just like consul
- Vault integrated storage also known as Raft allows Vault nodes to provide its own replicated storage across the Vault nodes.
- define a local path at which the data need to be stored.
- All vault nodes interact over TCP on port `8201`

### Example Raft configuration
```hcl
storage "raft" {
	path ="/opt/vault/data"
	node_id ="node-a-us-1.example.com"
	retry_join {
		auto_join="provider=aws region=us-east-1 tag_key=vault tag_vault=us-east-1"
	}
}
```

In a vault cluster we will have one leader node and other followers nodes
We can manually join a node to vault cluster

```sh
vault operator raft join https://active_node.example.com:8200
```

To list Vault cluster members
```sh
vault operator raft list-peers
```
