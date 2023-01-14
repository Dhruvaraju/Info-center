# Remote state

- Generally terraform creates a state file in the folder where configuration is present.
- Maintaining state locally is a not recommended
- Maintaining state in a version control system is also not recommended
	- Every time when performing operations on terraform we need to add pull latest version of state
	- If someone failed to push an updated state, further operations by others will create a data loss or resource manipulation
- We cannot store state on a SCM because it will contain sensitive information like IP's and initial credentials.

## State Locking

## Remote Backend

## Terraform State Commands


