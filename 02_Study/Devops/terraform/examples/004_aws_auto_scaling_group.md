# What is an *auto scaling group* - *[[004_aws_auto_scaling_group|Click here]]*

==To integrate an Auto Scaling group with an Application Load Balancer (ALB) using Terraform, you need to follow these steps:==

1. **Create a Launch Template**: Define the configuration for your EC2 instances.
2. **Create an Auto Scaling Group**: Use the launch template to create an Auto Scaling group.
3. **Create an Application Load Balancer**: Define the load balancer and its target group.
4. **Attach the Auto Scaling Group to the Load Balancer**: Register the Auto Scaling group with the target group of the load balancer.

### Step-by-Step Guide

#### 1. Create a Launch Template

Define the configuration for your EC2 instances, including the AMI, instance type, and security groups.

```hcl
resource "aws_launch_template" "example" {
  name          = "example-template"
  image_id      = "ami-12345678"
  instance_type = "t2.micro"

  network_interfaces {
    associate_public_ip_address = true
    security_groups             = [aws_security_group.instance_sg.id]
  }
}
```

#### 2. Create an Auto Scaling Group

Use the launch template to create an Auto Scaling group.

```hcl
resource "aws_autoscaling_group" "example" {
  desired_capacity     = 2
  max_size             = 5
  min_size             = 1
  vpc_zone_identifier  = [aws_subnet.subnet_a.id, aws_subnet.subnet_b.id]
  launch_template {
    id      = aws_launch_template.example.id
    version = "$Latest"
  }

  target_group_arns = [aws_lb_target_group.app_tg.arn]
}
```

#### 3. Create an Application Load Balancer

Define the load balancer and its target group.

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

#### 4. Attach the Auto Scaling Group to the Load Balancer

Register the Auto Scaling group with the target group of the load balancer.

```hcl
resource "aws_autoscaling_attachment" "asg_attachment" {
  autoscaling_group_name = aws_autoscaling_group.example.name
  alb_target_group_arn   = aws_lb_target_group.app_tg.arn
}
```

### Diagram of the Architecture

Here’s a simplified diagram of how the architecture looks:

!AWS Load Balancer Diagram

### Summary

This setup creates an Auto Scaling group that automatically adjusts the number of EC2 instances based on demand and integrates it with an Application Load Balancer to distribute incoming traffic across the instances. [The load balancer ensures high availability and fault tolerance by routing traffic only to healthy instances](https://developer.hashicorp.com/terraform/tutorials/aws/aws-asg)[1](https://developer.hashicorp.com/terraform/tutorials/aws/aws-asg)[2](https://devopscube.com/terraform-autoscaling-group/)[3](https://spacelift.io/blog/terraform-alb).