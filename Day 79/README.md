# Terraform Modules
Today, we’ll dive into  **Terraform Modules**  and understand why they are a game-changer for infrastructure as code. I’ve also prepared a practical demo to illustrate how modules simplify and enhance infrastructure management. You can find the code for this blog in my  [GitHub repository](https://github.com/MunilakshmiP/Terraform_projects.git).([https://github.com/MunilakshmiP/Terraform_projects.git]

----------

## [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-what-are-terraform-modules "Permalink")What Are Terraform Modules?

Think of Terraform modules as  **reusable building blocks**  for your infrastructure. Instead of repeating yourself (like a broken record), you can create these blocks once and reuse them wherever needed. It’s like having a LEGO set for cloud infrastructure – modular, reusable, and easy to assemble.

----------

## [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-why-do-we-need-modules "Permalink")Why Do We Need Modules?

Let’s break it down step by step,  **explained like you’re five**:

### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-1-modularity "Permalink")1.  **Modularity**

Modules let you split your infrastructure into smaller, easy-to-manage chunks. Instead of handling one giant, messy configuration, you’ll have neat, self-contained pieces like:

-   One module for an EC2 instance
    
-   Another module for a database
    
-   Yet another for a network
    

This makes everything clearer and easier to understand.

### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-2-reusability "Permalink")2.  **Reusability**

Imagine building a treehouse. Every time you need stairs, would you build them from scratch? No! You’d reuse your favorite staircase design. Modules work the same way: create something once, then reuse it across different projects.

### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-3-simplified-collaboration "Permalink")3.  **Simplified Collaboration**

In a team, you’d want everyone to work on different parts of the project without stepping on each other’s toes. Modules allow team members to work on separate pieces of the infrastructure and later combine them, making teamwork smooth.

### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-4-versioning-and-maintenance "Permalink")4.  **Versioning and Maintenance**

Modules have their own versions. When you make updates, you can bump up the version and let others choose when to use the new version. It’s like updating an app on your phone – only when you’re ready!

### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-5-abstraction "Permalink")5.  **Abstraction**

Modules hide the complicated stuff so you can focus on the important bits. For instance, a module for an EC2 instance can handle security groups, subnets, and all the nitty-gritty. You just specify the basics like instance type and image ID.

### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-6-testing-and-validation "Permalink")6.  **Testing and Validation**

Because modules are smaller, you can test them individually to ensure they’re error-free before using them in larger projects.

### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-7-documentation "Permalink")7.  **Documentation**

Modules make it clear how to use them by defining variables and outputs. It’s like giving you a recipe book along with the ingredients.

### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-8-scalability "Permalink")8.  **Scalability**

As your infrastructure grows, modules keep your code clean and organized. You can add more modules for new components without creating chaos.

### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-9-security-and-compliance "Permalink")9.  **Security and Compliance**

You can bake in best practices for security and compliance directly into modules. For example, an EC2 instance module could come with pre-configured security groups, IAM roles, and other settings, ensuring consistency and safety.

----------

## [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-practical-demo-terraform-modules "Permalink")Practical Demo: Terraform Modules

I’ve created a Terraform project to demonstrate modules. The code is available in my  [GitHub repository](https://github.com/MunilakshmiP/Terraform_projects.git). Let’s explore the structure:

### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-project-structure "Permalink")Project Structure

```
Terraform_projects/
├── modules/
│   ├── ec2_instance/
│       ├── main.tf
│       ├── variables.tf
│       ├── outputs.tf
├── main.tf

```

### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-step-1-creating-the-module "Permalink")Step 1: Creating the Module

Inside the  `modules/ec2_instance/`  folder:

#### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-maintf "Permalink")`main.tf`


```
provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "example" {
    ami = var.ami_value
    instance_type = var.aws_instance_type
}

```

#### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-variablestf "Permalink")`variables.tf`


```
vvariable "aws_value" {
  description = "Value of AMI"

}

variable "aws_instance_type" {
  description = "Value of instance type"

}

```

#### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-outputstf "Permalink")`outputs.tf`

```
output "public-ip-address" {
  value = aws_instance.example.public_ip
}

```

### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-step-2-using-the-module "Permalink")Step 2: Using the Module

In the root  `main.tf`  file:


```
provider "aws" {
  region = "ap-south-1"
}


  module "ec2_instance" {
  source = "./modules/ec2_instance"
  ami_value = "ami-053b12d3152c0cc71" # replace this
  aws_instance_type = "t2.micro"
  key_name      = "aws_logins"

}

```

### [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-step-3-running-the-code "Permalink")Step 3: Running the Code

1.  **Initialize Terraform**:

    ```
     terraform init
    
    ```
    
2.  **Plan Your Infrastructure**:
    

    
    ```
     terraform plan
    
    ```
    
3.  **Apply the Configuration**:
  
    
    ```
     terraform apply
    
    ```
    
4.  **Verify the Outputs**: Terraform will display the EC2 instance ID created by the module.
    

----------

## [](https://100daysdevops.hashnode.dev/day-79-of-100-days-terraform-modules?source=more_articles_bottom_blogs#heading-key-takeaways "Permalink")Key Takeaways

-   **Modules make your life easier**: They simplify, reuse, and organize your infrastructure.
    
-   **Think modular**: Start breaking down your Terraform configurations into modules.
    
-   **Check out the repo**: All the files are in my  [GitHub repositor](https://github.com/MunilakshmiP/Terraform_projects.git)  [https://github.com/MunilakshmiP/Terraform_projects.git]
    
    Happy Terraforming! See you on Day 80! 🌟
