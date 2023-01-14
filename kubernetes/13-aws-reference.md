# AWS reference commands

- To interact with aws we can use aws cli
- after installing aws cli version can be found using `aws --version`
- to interact with any service `aws <service> <subcommand>`

> Local stack is a mocking tool used to mock aws cloud environment

- Once configured it will give a url if the url provided is `http:aws:4566`, we can access it with aws cli as `aws --endpoint http://aws:4566 <service> <subcommand>`

Default region and credentials can be added in .aws folder so that those do not have to be provided again and again
config
```
[default]
region = us-east-1
```

credentials
```
[default]
aws_access_key_id = foo
aws_secret_access_key = bar
```

Creating an aws iam user
```sh
aws --endpoint http://aws:4566 iam create-user --user-name alpha
#alpha user wil be created with default permissions
```

Attaching an user policy to user
```sh
aws --endpoint http://aws:4566 iam attach-user-policy --user-name mary --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
```

Creating a iam-group using aws cli
```sh
aws --endpoint http://aws:4566 iam create-group --group-name project-developers
```

Adding user to user group
```sh
aws --endpoint http://aws:4566 iam add-user-to-group --group-name project-sapphire-developers --user-name jill
```

