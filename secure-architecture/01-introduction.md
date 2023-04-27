- [[#What should be considered in secure architecture?|What should be considered in secure architecture?]]
- [[#Basic Principles|Basic Principles]]
	- [[#Basic Principles#CIA Triad|CIA Triad]]
	- [[#Basic Principles#Basic Principles|Basic Principles]]
	- [[#Basic Principles#Security Techniques|Security Techniques]]
	- [[#Basic Principles#Authentication & Authorization|Authentication & Authorization]]


## What should be considered in secure architecture?

- User-level design
- Infrastructure Design
- Architecture Planning
- Logging
- Backup & Disaster Recovery
- Documentation

## Basic Principles

### CIA Triad
#cia_triad

- Confidentiality 
	- Keeping private data private, Encrypting and providing sufficient access controls
- Integrity
	- Data is free from unauthorized changes, Accessing information only with valid digital certificates and file hashes.
- Availability
	- Maintain reliable and timely access to all the systems. Systems to have redundancy and protection from security controls. 

### Basic Principles

- Trust but verify
	- Applies to all aspects of security. When a new or existing system is verified check if the controls and settings are set as they should be set.
- Zero Trust
	- Model where everything is trusted only when it is verified.
- Defense in depth
	- Multiple layers of security controls, Overlap of systems, Try to use different vendors.
- Security through obscurity
	- Make systems difficult to detect, example: hidden SSIDs on wireless, using non standard ports for public access
- Asset & Inventory management and Control
	- Have an inventory management system. onboard or remove systems when needed.

### Security Techniques

- Minimizing the attack surface
	- Reduce the number of services, open ports on devices/ systems. hence having less for attackers to potentially compromise
- Secure defaults
	- New devices and systems should be configured to secure manner prior to deployment
	- Create own server images adding secure configurations
	- Do not use default ports, passwords, services, etc
- Privacy by design
	- All private data should be secured at all times
- Fail secure
	- If/when a system fails, it should not increase any security concerns
	- Predictable and uncompromising behavior

### Authentication & Authorization

- Least Privilege
	- Grant access for what is need to perform job, nothing more
- Separation of duties
	- Begin to introduce roles in authorization
	- Access given based on job roles
- RBAC
	- Role Based Access Control
	- Create Roles and groups and assign permissions to groups not users
- AUTH creep
	- Overtime more and more accesses are granted, and department and job transfers will happen. Then remove old access and assign new roles.