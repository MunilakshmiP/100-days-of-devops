# Terraform Practical Demo – Spin Up Your First EC2 Instance in AWS! 🚀

Welcome to Day 75 of my **100 Days of DevOps** journey! 🎉 Today, we’re diving into a **hands-on, practical** demo of **Terraform**. If you've ever wanted to quickly spin up an AWS EC2 instance without manually clicking through the AWS Console, this is your chance!

We’re going to keep it simple and easy, so don’t worry if you’re new to Terraform. By the end of this blog, you’ll know how to use Terraform to create your very own **EC2 instance** in AWS.

----------

### **Step 1: Check Terraform Version**

Before we start, let's first check if Terraform is installed on your system. Open your terminal or bash and type the following command:

```bash
terraform -v

```

This command will show you the installed Terraform version. If you see something like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736439724333/39651654-2869-433f-9128-9b1dba3a77df.png)

Congratulations! Terraform is already installed. If not, you’ll need to install it first. Once you're good to go, we can move to the next step!

----------

### **Step 2: Set Up Your AWS Secret Keys**

To use Terraform with AWS, you need to pair it with your AWS credentials. This ensures Terraform has permission to interact with your AWS account.

In your bash terminal, use the following commands to set up your AWS credentials:

```bash
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"
export AWS_DEFAULT_REGION="ap-south-1"  # Mumbai region

```

Make sure to replace `your-access-key` and `your-secret-key` with your actual AWS credentials. You can get these from your **AWS IAM** (Identity and Access Management) console. These keys are like a password that Terraform uses to talk to AWS.

----------

### **Step 3: Create the Terraform Configuration File**

Now, let’s create a Terraform configuration file. We’ll use **Nano** to create the [`main.tf`](http://main.tf) file, which will tell Terraform what to do.

Open the terminal and type:

```bash
nano main.tf

```

Inside [`main.tf`](http://main.tf), paste the following code:

```plaintext
provider "aws" {
  region = "ap-south-1"  # AWS Region set to Asia Pacific (Mumbai)
}

resource "aws_instance" "demo_ec2" {
  ami           = "ami-053b12d3152c0cc71"  # Your AMI ID for the EC2 instance
  instance_type = "t2.micro"               # t2.micro is eligible for the Free Tier
  key_name      = "aws_logins"             # EC2 key pair for SSH access (make sure this key pair exists in the region)

  tags = {
    Name = "Demo EC2 Instance"  # Tagging the instance with a name
  }
}

```

----------

### **Breaking Down the Code** – Let's Explain It Like a Kid! 🎨

Let’s break down this code and explain it like we’re explaining to a 5-year-old! 🧸

1.  `provider "aws"`:  
    This part tells Terraform, "Hey! I want to use AWS for creating resources." The `region` is where your resources will live – in this case, Mumbai (`ap-south-1`).
    
2.  `resource "aws_instance" "demo_ec2"`:  
    This defines the resource we’re creating – in this case, an EC2 instance named `demo_ec2`.
    
3.  `ami = "ami-053b12d3152c0cc71"`:  
    This is the ID of the **Amazon Machine Image** (AMI). An AMI is like a blueprint for your instance. It tells AWS what kind of machine you’re creating. This AMI ID is for a basic, free-tier-friendly Linux machine.
    
4.  `instance_type = "t2.micro"`:  
    This is the type of EC2 instance. A **t2.micro** is free-tier eligible, which means it’s free for personal use up to certain limits!
    
5.  `key_name = "aws_logins"`:  
    This is the SSH key pair that you’ll use to securely access your EC2 instance. You should already have this key pair created in the AWS console.
    
6.  `tags = { Name = "Demo EC2 Instance" }`:  
    Tags help us name and organize our resources. We’re naming our EC2 instance “Demo EC2 Instance.”
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736439649321/e60aae6e-8f5b-421d-ad5c-9db71a45db6a.png)

----------

### **Step 4: Initialize Terraform**

Before running any commands, we need to initialize Terraform. This sets up the backend and downloads any necessary plugins.

Run:

```bash
terraform init

```

This command will:

-   Initialize your working directory.
    
-   Download AWS provider plugins.
    
-   Prepare everything for the magic to happen.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736439609711/c37bbded-ea66-405d-a233-d7f761bdac9d.png)

----------

### **Step 5: Preview the Changes**

Now that everything is initialized, let’s see what Terraform is planning to do. Run:

```bash
terraform plan

```

This command shows you a **preview** of what Terraform is going to create, modify, or delete. Think of it as a sneak peek before the actual action begins!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736439574690/21db34f3-b374-4094-aaa4-a1715100143e.png)

----------

### **Step 6: Apply the Terraform Configuration**

Ready for action? Let’s apply the changes. Run:

```bash
terraform apply

```

Terraform will ask for confirmation to proceed. Type `yes` to confirm.

This command will:

-   Create the EC2 instance based on the configuration we wrote in [`main.tf`](http://main.tf).
    
-   Spin up the EC2 instance, ready for you to SSH into and start using!
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736439494070/7e6e9a6b-6ad8-4c86-a292-62f7876088da.png)![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736439513544/464ce10d-774d-4ae2-a52a-bb563f096727.png)

----------

### **Step 7: Check Your AWS EC2 Instance**

After the Terraform apply finishes, head over to the AWS Console to see your **EC2 instance** running. You should see something like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736439449616/62f417cf-e37d-4ef6-8c2e-eda4766360ec.png)

----------

### **Additional Terraform Commands**

Here are a few other useful Terraform commands you can use in your day-to-day workflow:

-   `terraform deploy`: Not an official command, but often used to describe the act of applying your configuration and deploying resources in AWS.
    
-   `terraform destroy`: When you’re done, run this command to delete the resources you’ve created and clean up your AWS account.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736439858681/f2175fdd-4d5c-4a35-af8a-6e024e2dd47a.png)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736439919891/90c615b0-ee00-404c-8288-b4c09fc40930.png)

----------

### **Conclusion: Terraform Magic at Your Fingertips!**

Today, we’ve gone through the entire process of using Terraform to create an EC2 instance in AWS, from checking your version to running your very own infrastructure as code. 🚀

With Terraform, the sky’s the limit! You can scale up your infrastructure in no time, automate the deployment of entire cloud environments, and work faster and smarter.

Make sure to check your AWS console for the EC2 instance you’ve just created and have fun exploring what Terraform can do next!



