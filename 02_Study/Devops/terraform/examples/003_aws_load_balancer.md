### Real-Life Example: Setting Up a Load Balancer on AWS

Let’s set up an Application Load Balancer (ALB) to distribute traffic across multiple EC2 instances.

#### Step-by-Step Guide

1. **Create a VPC and Subnets**: Define a VPC and subnets where your instances will reside.
    
    ```hcl
    resource "aws_vpc" "main" {
      cidr_block = "10.0.0.0/16"
    }
    
    resource "aws_subnet" "subnet_a" {
      vpc_id     = aws_vpc.main.id
      cidr_block = "10.0.1.0/24"
      availability_zone = "us-west-2a"
    }
    
    resource "aws_subnet" "subnet_b" {
      vpc_id     = aws_vpc.main.id
      cidr_block = "10.0.2.0/24"
      availability_zone = "us-west-2b"
    }
    ```
    
2. **Create Security Groups**: Define security groups for the load balancer and EC2 instances.
    
    ```hcl
    resource "aws_security_group" "lb_sg" {
      vpc_id = aws_vpc.main.id
    
      ingress {
        from_port   = 80
        to_port     = 80
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
    
    resource "aws_security_group" "instance_sg" {
      vpc_id = aws_vpc.main.id
    
      ingress {
        from_port   = 80
        to_port     = 80
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
    
3. **Launch EC2 Instances**: Launch EC2 instances in the defined subnets.
    
    ```hcl
    resource "aws_instance" "web" {
      count         = 2
      ami           = "ami-12345678"
      instance_type = "t2.micro"
      subnet_id     = element([aws_subnet.subnet_a.id, aws_subnet.subnet_b.id], count.index)
      security_groups = [aws_security_group.instance_sg.name]
    
      tags = {
        Name = "WebServer"
      }
    }
    ```
    
4. **Create an Application Load Balancer**: Define the load balancer and its target group.
    
    ```hcl
    resource "aws_lb" "app_lb" {
      name               = "app-lb"
      internal           = false
      load_balancer_type = "application"
      security_groups    = [aws_security_group.lb_sg.id]
      subnets            = [aws_subnet.subnet_a.id, aws_subnet.subnet_b.id]
    }
    
    resource "aws_lb_target_group" "app_tg" {
      name     = "app-tg"
      port     = 80
      protocol = "HTTP"
      vpc_id   = aws_vpc.main.id
    }
    
    resource "aws_lb_listener" "app_listener" {
      load_balancer_arn = aws_lb.app_lb.arn
      port              = 80
      protocol          = "HTTP"
    
      default_action {
        type             = "forward"
        target_group_arn = aws_lb_target_group.app_tg.arn
      }
    }
    ```
    
5. **Register Instances with the Target Group**: Register the EC2 instances with the target group.
    
    ```hcl
    resource "aws_lb_target_group_attachment" "app_tg_attachment" {
      count            = 2
      target_group_arn = aws_lb_target_group.app_tg.arn
      target_id        = element(aws_instance.web.*.id, count.index)
      port             = 80
    }
    ```
    

### Summary

This setup creates an Application Load Balancer that distributes incoming HTTP traffic across two EC2 instances in different subnets. [The load balancer ensures high availability and fault tolerance by routing traffic only to healthy instances](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/how-elastic-load-balancing-works.html)[1](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/how-elastic-load-balancing-works.html)[2](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)[3](https://creately.com/diagram/example/ip8amw3c1/architecture-of-the-elastic-load-balancing-service-example).