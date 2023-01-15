# Provisioners
#provisioner
provisioners provide a way to carryout tasks such as running commands or scripts on a remote resource or locally on a machine where terraform is installed.

Example: For running a NGINX server on an aws ec2 instance we can use the following resource
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
```

## `remote-exec` provisioner
#remote-exec
The same can be modified to use a provisiner as below:

```hcl
resource "aws_instance" "webserver" {
  ami           = "ami-lhmgsilg784wbasfg"
  instance_type = "t2.micro"
  tags = {
    Name        = "webserver"
    Description = "An NGINX server for webhosting"
  }
  provisioner "remote-exec" {
	  inline = ["sudo apt update",
				 "sudo apt install nginx -y",
				 "sudo systemctl enable nginx",
				 "sudo systemctl start nginx"
				]
  }
  connection {
	  type = "ssh"
	  host = self.public_ip
	  user = "ubuntu"
	  private_key = file("root/.ssh/web")
  }
  key_name               = aws_key_pair.web.id
  vpc_security_group_ids = [aws_security_group.ssh-access.id]
}
```

- In the above example `remote-exec` provisioner is used.
- It is not guaranteed that the provisioner will run just by adding it.
- There should be network connectivity between machine on which terraform is run and the EC2 resource that is being created.
- An Authentication mechanism should be provided like SSH
- Access to connect to resource also need to be provided.

## `local-exec` provisioner
#local-exec
- User to run scripts on a local machine where configuration is present.
- Used when data need to be gathered in a local machine.

```hcl
resource "aws_instance" "webserver" {
  ami           = "ami-lhmgsilg784wbasfg"
  instance_type = "t2.micro"
  tags = {
    Name        = "webserver"
    Description = "An NGINX server for webhosting"
  }
  provisioner "local-exec" {
	  command = "echo ${aws_instance.webserver.public_ip} >> /tmp/ips.txt"
  }
```

- By default provisioners are run after the resources are provisioned, this is also know as create_time provisioner.
- A provisioner can also be run at a destroy time called as destroy_time  #destroy_time_provisioner
- destroy time provisioner can be defined as below
```hcl
provisioner "local-exec" {
	when = destroy
	command = "echo ${aws_instance.webserver.public_ip} >> /tmp/ips.txt"
  }
```

> If the script or provisioner fails terraform script will also fail. This is the default behavior

- We can define what need to be done when a provisioner script fails by mentioning the on_failure attribute.
- on failure attribute takes fail or continue as value.
- If the provisioner script fails terraform marks the resource as tainted

```hcl
provisioner "local-exec" {
	when = destroy
	on_failure = fail
	command = "echo ${aws_instance.webserver.public_ip} >> /tmp/ips.txt"
  }
```

- Terraform only recommends the use of provisioners as a last resort.
- Provisioners actions cannot be maintained by terraform.
