# Audit Devices

- Audit devices keeps a detailed log of all authenticated requests and responses to vault
- Audit log is formatted using JSON
- Sensitive information in the request and response is hashed with a salt using HMAC-SHA256 to ensure secrets and tokens aren't in plain text.
- Log files hould be protected as a user with permission can still check the value of those secrets via the /sts/audit-hash api and compare to the log file
- Command used to enable a log file
```
vault audit enable file file_path=/var/log/vault_audit_log.log 
```

## Types of Audit Devices

- File
	- Writes to a file - appends logs to the file
	- Does not assist with log rotation
	- use fluentd or similar tool to send to collector.
- Syslog
	- Writes audit logs to a syslog
	- Sends to a local agent only
- Socket
	- Writes to a tcp, udp, or Unix socket
	- unreliable due to the underlying protocol, never enable UDP
	- should be used where strong guarantees are required.

- Best practice is to have more than one audit device enabled
- If there are any audit devices enables, vault requires that it can write to the vault log before completing the client request.
- Vault prioritizes safety over availability.
- If vault cannot write to a persistent log, it will stop responding to client requests, which means vault is down.

> [!Info]
> Vault requires at least one audit device to write the log before completing the vault request - if enabled.
