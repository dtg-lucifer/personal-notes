### Example: Setting Up Auto Scaling and ELB

1. **Create a Launch Template**: Define the configuration for your EC2 instances, including the AMI, instance type, and security groups.
    
    ```hcl
    resource "aws_launch_template" "example" {
      name          = "example-template"
      image_id      = "ami-12345678"
      instance_type = "t2.micro"
    
      network_interfaces {
        associate_public_ip_address = true
        security_groups             = [aws_security_group.example.id]
      }
    }
    ```
    
2. **Create an Auto Scaling Group**: Use the launch template to create an Auto Scaling group.
    
    ```hcl
    resource "aws_autoscaling_group" "example" {
      desired_capacity     = 2
      max_size             = 5
      min_size             = 1
      vpc_zone_identifier  = [aws_subnet.example.id]
      launch_template {
        id      = aws_launch_template.example.id
        version = "$Latest"
      }
    }
    ```
    
3. **Create an Elastic Load Balancer**: Distribute traffic across the instances in the Auto Scaling group.
    
    ```hcl
    resource "aws_lb" "example" {
      name               = "example-lb"
      internal           = false
      load_balancer_type = "application"
      security_groups    = [aws_security_group.example.id]
      subnets            = [aws_subnet.example.id]
    }
    
    resource "aws_lb_target_group" "example" {
      name     = "example-tg"
      port     = 80
      protocol = "HTTP"
      vpc_id   = aws_vpc.example.id
    }
    
    resource "aws_lb_listener" "example" {
      load_balancer_arn = aws_lb.example.arn
      port              = 80
      protocol          = "HTTP"
    
      default_action {
        type             = "forward"
        target_group_arn = aws_lb_target_group.example.arn
      }
    }
    ```
    

### Creating and Linking Multiple EC2 Instances for Dev and Prod Environments

To create and link multiple EC2 instances for development and production environments, you can use separate subnets and security groups within the same VPC:

1. **Define Subnets for Dev and Prod**:
    
    ```hcl
    resource "aws_subnet" "dev" {
      vpc_id            = aws_vpc.example.id
      cidr_block        = "10.0.1.0/24"
      availability_zone = "us-west-2a"
    }
    
    resource "aws_subnet" "prod" {
      vpc_id            = aws_vpc.example.id
      cidr_block        = "10.0.2.0/24"
      availability_zone = "us-west-2b"
    }
    ```
    
2. **Create Security Groups for Dev and Prod**:
    
    ```hcl
    resource "aws_security_group" "dev_sg" {
      name        = "dev_sg"
      description = "Security group for development environment"
      vpc_id      = aws_vpc.example.id
    
      ingress {
        from_port   = 22
        to_port     = 22
        protocol    = "tcp"
        cidr_blocks = ["0.0.0.0/0"]
      }
    
      egress {
        from_port   = 0
        to_port     = 0
        protocol    = "-1"
        cidr_blocks = ["0.0.0.0/0"]
      }
    }
    
    resource "aws_security_group" "prod_sg" {
      name        = "prod_sg"
      description = "Security group for production environment"
      vpc_id      = aws_vpc.example.id
    
      ingress {
        from_port   = 443
        to_port     = 443
        protocol    = "tcp"
        cidr_blocks = ["0.0.0.0/0"]
      }
    
      egress {
        from_port   = 0
        to_port     = 0
        protocol    = "-1"
        cidr_blocks = ["0.0.0.0/0"]
      }
    }
    ```
    
3. **Launch EC2 Instances in Dev and Prod Subnets**:
    
    ```hcl
    resource "aws_instance" "dev_instance" {
      ami           = "ami-12345678"
      instance_type = "t2.micro"
      subnet_id     = aws_subnet.dev.id
      security_groups = [aws_security_group.dev_sg.name]
    
      tags = {
        Name = "DevInstance"
      }
    }
    
    resource "aws_instance" "prod_instance" {
      ami           = "ami-12345678"
      instance_type = "t2.micro"
      subnet_id     = aws_subnet.prod.id
      security_groups = [aws_security_group.prod_sg.name]
    
      tags = {
        Name = "ProdInstance"
      }
    }
    ```
    

[By using VPCs, subnets, security groups, and Auto Scaling, you can effectively manage and scale your EC2 instances for both development and production environments](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)[1](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)[2](https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html)[3](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-vpc.html)[4](https://docs.aws.amazon.com/autoscaling/ec2/userguide/tutorial-ec2-auto-scaling-load-balancer.html).