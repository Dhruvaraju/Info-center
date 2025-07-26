# Managed services

- **IAAS:** Infrastructure as a service, cloud providers will provide hardware, storage and virtualization software. Installing OS, installing app runtime, installing application, managing applications will be done by the end users.
- PAAS: Platform as service, in this including infrastructure, OS and app run time is provided, users are responsible for the app installation and app maintenance.
- SAAS: Software as service, in this users will just use the software they do not have any access to infrastructure or application management. Example Microsoft teams.

There are many other managed services like
- FAAS function as a service
- CAAS container as a service

## What is Serverless.

- End users will just add their app code to a platform, they do not  have to worry about managing server.
- No need to worry about infrastructure.
- No need to worry about OS updates.

## Shared responsibility

- Security is a shared responsibility on GCP
- GCP provides features for security like KMS and IAM

Customers are responsible for :
- SAAS: content, access policies, Usage
- PAAS: SAAS, deployment, web application security
- IAAS: PAAS, operations, network security, gest OS
