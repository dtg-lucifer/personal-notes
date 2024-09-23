Creating a well-organized Terraform folder structure is crucial for maintaining and scaling your infrastructure as code, especially in a production environment. Here’s an advanced folder structure that is commonly used in production-grade setups:

### Advanced Terraform Folder Structure

```plaintext
├── environments
│   ├── dev
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── terraform.tfvars
│   ├── staging
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── terraform.tfvars
│   └── prod
│       ├── main.tf
│       ├── variables.tf
│       ├── outputs.tf
│       └── terraform.tfvars
├── modules
│   ├── vpc
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── README.md
│   ├── ec2
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── README.md
│   ├── rds
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── README.md
│   └── ...
├── global
│   ├── providers.tf
│   ├── backend.tf
│   ├── versions.tf
│   └── variables.tf
├── scripts
│   ├── init.sh
│   ├── deploy.sh
│   └── destroy.sh
└── README.md
```

### Explanation of the Structure

1. **Environments**:
    
    - **dev, staging, prod**: Separate directories for each environment. Each environment has its own `main.tf`, `variables.tf`, `outputs.tf`, and `terraform.tfvars` files. This separation allows for environment-specific configurations and variables.
2. **Modules**:
    
    - **vpc, ec2, rds**: Reusable modules for different components of your infrastructure. Each module has its own `main.tf`, `variables.tf`, `outputs.tf`, and `README.md` files. Modules encapsulate and abstract the configuration for specific resources, making them reusable and easier to manage.
3. **Global**:
    
    - **providers.tf**: Defines the providers (e.g., AWS, Azure) used across all environments.
    - **backend.tf**: Configures the backend for storing the Terraform state (e.g., S3, Azure Blob Storage).
    - **versions.tf**: Specifies the required Terraform version and provider versions.
    - **variables.tf**: Global variables that are shared across multiple environments.
4. **Scripts**:
    
    - **init.sh, deploy.sh, destroy.sh**: Shell scripts for initializing, deploying, and destroying the infrastructure. These scripts help automate common tasks and ensure consistency.
5. **README.md**:
    
    - Documentation for the project, explaining the structure, usage, and any other relevant information.

### Benefits of This Structure

- **Modularity**: By breaking down the configuration into modules, you can reuse and manage components more effectively.
- **Scalability**: This structure supports scaling by allowing you to add more environments and modules as needed.
- **Maintainability**: Clear separation of concerns makes it easier to understand, update, and maintain the codebase.
- **Collaboration**: Different teams can work on different modules or environments without interfering with each other.

### Example Usage

Here’s a brief example of how you might use this structure to deploy a VPC and EC2 instances in the `dev` environment:

**environments/dev/main.tf**:

```hcl
module "vpc" {
  source = "../../modules/vpc"
  cidr_block = var.vpc_cidr_block
}

module "ec2" {
  source = "../../modules/ec2"
  vpc_id = module.vpc.vpc_id
  subnet_id = module.vpc.public_subnet_id
}
```

**modules/vpc/main.tf**:

```hcl
resource "aws_vpc" "main" {
  cidr_block = var.cidr_block
  tags = {
    Name = "main-vpc"
  }
}

resource "aws_subnet" "public" {
  vpc_id     = aws_vpc.main.id
  cidr_block = "10.0.1.0/24"
  tags = {
    Name = "public-subnet"
  }
}

output "vpc_id" {
  value = aws_vpc.main.id
}

output "public_subnet_id" {
  value = aws_subnet.public.id
}
```

**modules/ec2/main.tf**:

```hcl
resource "aws_instance" "web" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
  subnet_id     = var.subnet_id
  tags = {
    Name = "web-instance"
  }
}
```

[This structure and approach ensure that your Terraform codebase is organized, scalable, and maintainable, making it suitable for production-grade deployments](https://www.env0.com/blog/terraform-files-and-folder-structure-organizing-infrastructure-as-code)[1](https://www.env0.com/blog/terraform-files-and-folder-structure-organizing-infrastructure-as-code)[2](https://cloud.google.com/docs/terraform/best-practices/general-style-structure).

If you have any specific requirements or need further customization, feel free to ask!