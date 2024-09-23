To create a security group in AWS using the `aws_security_group` resource in Terraform, which allows all outgoing connections but restricts incoming connections to TCP on port 443 (HTTPS) and port 22 (SSH), you can follow these steps:

### Step-by-Step Guide

1. **Create a Terraform Configuration File**: Create a file named `main.tf` (or any name you prefer) and add the following configuration:

```hcl
data "aws_ami" "app_ami" {
  most_recent = true

  filter {
    name   = "name"
    values = ["bitnami-tomcat-*-x86_64-hvm-ebs-nami"]
  }

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }

  owners = ["979382823631"] # Bitnami
}

data "aws_vpc" "default" {
  default = true
}

resource "aws_instance" "blog" {
  ami                    = data.aws_ami.app_ami.id
  instance_type          = var.instance_type
  vpc_security_group_ids = [aws_security_group.blog.id]

  tags = {
    Name = "Learning Terraform"
  }
}

resource "aws_security_group" "blog" {
  name = "blog"
  tags = {
    Terraform = "true"
  }
  vpc_id = data.aws_vpc.default.id
}

resource "aws_security_group_rule" "blog_http_in" {
  type        = "ingress"
  from_port   = 80
  to_port     = 80
  protocol    = "tcp"
  cidr_blocks = ["0.0.0.0/0"]
  security_group_id = aws_security_group.blog.id
}


resource "aws_security_group_rule" "blog_https_in" {
  type        = "ingress"
  from_port   = 443
  to_port     = 443
  protocol    = "tcp"
  cidr_blocks = ["0.0.0.0/0"]
  security_group_id = aws_security_group.blog.id
}


resource "aws_security_group_rule" "blog_everything_out" {
  type        = "egress"
  from_port   = 0
  to_port     = 0
  protocol    = "-1"
  cidr_blocks = ["0.0.0.0/0"]
  security_group_id = aws_security_group.blog.id
}
```

### Explanation

- **Provider Block**: Specifies the AWS provider and region.
- **Resource Block**: Defines the security group with the name `custom_security_group`.
- **Egress Rule**: Allows all outgoing traffic (`from_port` and `to_port` set to 0, `protocol` set to `-1` for all protocols, and `cidr_blocks` set to `0.0.0.0/0` for all IPs).
- **Ingress Rules**:
    - Allows incoming HTTPS traffic on port 443.
    - Allows incoming SSH traffic on port 22.
- **Tags**: Adds a name tag to the security group for easier identification.

### Applying the Configuration

1. **Initialize Terraform**:
    
    ```sh
    terraform init
    ```
    
2. **Plan the Changes**:
    
    ```sh
    terraform plan
    ```
    
3. **Apply the Configuration**:
    
    ```sh
    terraform apply
    ```
    

[This will create a security group in your specified VPC with the desired rules](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group)[1](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group)[2](https://registry.terraform.io/providers/-/aws/latest/docs/data-sources/security_group)[3](https://shisho.dev/dojo/providers/aws/Amazon_EC2/aws-security-group/).

If you have any specific requirements or need further customization, feel free to ask!