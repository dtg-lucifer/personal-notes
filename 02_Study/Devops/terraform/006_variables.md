A **`.tfvars` file** in Terraform is used to define variable values separately from the main configuration files. This helps in managing and organizing variable assignments, especially when dealing with multiple environments or complex configurations. Here’s a breakdown of how to use them:

### What is a `.tfvars` File?

- [**Purpose**: `.tfvars` files store variable definitions, allowing you to externalize and manage them efficiently](https://spacelift.io/blog/terraform-tfvars)[1](https://spacelift.io/blog/terraform-tfvars).
- **Format**: These files use the same syntax as Terraform configuration files (HCL) but are specifically for variable assignments. [They can also be in JSON format with the extension `.tfvars.json`](https://spacelift.io/blog/terraform-tfvars)[1](https://spacelift.io/blog/terraform-tfvars).

### How to Use `.tfvars` Files

1. **Creating a `.tfvars` File**:
    
    - Create a file with the extension `.tfvars` (e.g., `terraform.tfvars`).
    - Define your variables in this file. For example:
        
        ```hcl
        instance_type = "t2.micro"
        instance_count = 3
        ```
        
2. **Referencing Variables in Configuration**:
    
    - In your main Terraform configuration files, declare the variables:
        
        ```hcl
        variable "instance_type" {
          type = string
          description = "Type of EC2 instance"
        }
        
        variable "instance_count" {
          type = number
          description = "Number of instances"
        }
        ```
        
3. **Applying the `.tfvars` File**:
    
    - Terraform automatically loads `terraform.tfvars` or any file matching `*.auto.tfvars` in the current directory.
    - You can also specify a `.tfvars` file explicitly using the `-var-file` flag:
        
        ```sh
        terraform apply -var-file="custom.tfvars"
        ```
        

### Benefits of Using `.tfvars` Files

- [**Separation of Concerns**: Keeps variable definitions separate from their values, making the configuration cleaner and more manageable](https://spacelift.io/blog/terraform-tfvars)[2](https://www.devopsschool.com/blog/terraform-variable-using-terraform-tfvars-example/).
- [**Environment Management**: Easily switch between different environments (e.g., development, staging, production) by using different `.tfvars` files](https://spacelift.io/blog/terraform-tfvars)[2](https://www.devopsschool.com/blog/terraform-variable-using-terraform-tfvars-example/).
- [**Security**: Sensitive information can be stored in `.tfvars` files and excluded from version control using `.gitignore`](https://spacelift.io/blog/terraform-tfvars)[2](https://www.devopsschool.com/blog/terraform-variable-using-terraform-tfvars-example/).

Would you like an example of a complete Terraform setup using `.tfvars` files?

[](https://spacelift.io/blog/terraform-tfvars)[1](https://spacelift.io/blog/terraform-tfvars): [](https://spacelift.io/blog/terraform-tfvars)[2](https://www.devopsschool.com/blog/terraform-variable-using-terraform-tfvars-example/):