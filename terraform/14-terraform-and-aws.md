# Using terraform with AWS

## Creating an iam user
```hcl
provider "aws" {
	region = "us-west-2"
		access_key = "as;jdkhoweut9842h3oh23tr2hrh"
		secret_key = "k;jhgwe8t249ywehfn2y3n275"
}
resource "aws_iam_user" "admin-user" {
	name = "alpha"
	tags = {
		description = "Technical team lead requires full access"
	}
}
```

Instead of placing the credentials in configuration file we can place it in aws cli config path `.aws/config/credntials`
```config
[default]
aws_access_key_id =
aws_secret_access_key =
```

It can also be performed by setting environment variables: `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY_ID`

## iam policies with terraform

- [ ] create user
- [ ] create policy
- [ ] Attach policy to user

```hcl
resource "aws_iam_user" "admin-user"{
	name = "alpha"
	tags = {
		Description = "Tech lead"
	}
}

resource "aws_iam_policy" "admin-user" {
	name = "AdminUsers"
	policy = <<EOF
	{
		"Version": "20112-10-17",
		"Statement": [
			{
			  "Effect": "Allow",
			  "Action": "*",
			  "Resource": "**"
			}
		]
	}
	EOF
}

resource "aws_iam_user_policy_attachemnt" "lucy-admin-access" {
	user = aws_iam_user.admin-user.name
	policy_arn = aws_iam_policy.adminUser.arn
}
```

- To add file content `<<EOF  EOF` is used.
- Alternatively we can move it to a file and access the file using the file name
// admin-polict-file
```json
{
	"Version": "20112-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Action": "*",
			"Resource": "**"
		}
	]
}
```

// config file

```hcl
resource "aws_iam_user" "admin-user"{
	name = "alpha"
	tags = {
		Description = "Tech lead"
	}
}

resource "aws_iam_policy" "admin-user" {
	name = "AdminUsers"
	policy = file(admin-policy.json)
}

resource "aws_iam_user_policy_attachemnt" "lucy-admin-access" {
	user = aws_iam_user.admin-user.name
	policy_arn = aws_iam_policy.adminUser.arn
}
```

### EC2 instance with terraform

`main.tf`

```hcl
resource "aws_instance" "webserver" {
  ami           = "ami-lhmgsilg784wbasfg"
  instance_type = "t2.micro"
  tags = {
    Name        = "webserver"
    Description = "An NGINX server for webhosting"
  }
  user_data              = <<EOF
                #!/bin/bash
                sudo apt update
                sudo apt install nginx -y
                systemctl enable nginx
                systemctl start nginx
                EOF

  key_name               = aws_key_pair.web.id
  vpc_security_group_ids = [aws_security_group.ssh-access.id]
}

resource "aws_key_pair" "web" {
  public_key = file("/root/.ssh/web.pub")
}

resource "aws_security_group" "ssh-access" {
  name        = "ssh-access"
  description = "Allow ssh access from internet"
  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

output "public-ip" {
  value = aws_instance.webserver.public_ip
}
```