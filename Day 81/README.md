# Terraform Provisioners — A Tale of Automation and Magic! 🌟
Hello, Terraform Wizards! 🪄  
Today, let me tell you a story about  **Provisioners**, the unsung heroes of Terraform. They work behind the scenes to sprinkle some magic dust—executing scripts or commands to make your infrastructure shine.

Let’s dive into the world of  **provisioners**, understand their role, and try out some fun projects together! 🛠️

----------

## [](https://100daysdevops.hashnode.dev/day-81-of-100-days-terraform-provisioners-a-tale-of-automation-and-magic#heading-once-upon-a-time-what-are-provisioners "Permalink")**Once Upon a Time: What Are Provisioners? 📜**

Imagine you're building a castle (your infrastructure). The walls, towers, and gates are all in place, but you still need a team of helpers to decorate the interiors and add the final touches.

**Provisioners**  are those helpers in Terraform. They execute scripts or commands during resource creation or deletion, ensuring everything is perfect.

### [](https://100daysdevops.hashnode.dev/day-81-of-100-days-terraform-provisioners-a-tale-of-automation-and-magic#heading-what-do-provisioners-do "Permalink")**What Do Provisioners Do?**

-   Install software on a server.
    
-   Upload configuration files.
    
-   Run scripts to configure the server.
    

### [](https://100daysdevops.hashnode.dev/day-81-of-100-days-terraform-provisioners-a-tale-of-automation-and-magic#heading-types-of-provisioners "Permalink")**Types of Provisioners**

Provisioners come in two flavors:

1.  **Creation-Time Provisioners**: Run during resource creation.
    
2.  **Destroy-Time Provisioners**: Run during resource destruction.
    

----------

## [](https://100daysdevops.hashnode.dev/day-81-of-100-days-terraform-provisioners-a-tale-of-automation-and-magic#heading-meet-the-magical-provisioners "Permalink")**Meet the Magical Provisioners ✨**

1.  **File Provisioner**  
    Like a mailman, it copies files or directories from your local machine to the remote server.
    
2.  **Local-Exec Provisioner**  
    Think of it as shouting commands from your desk—it runs scripts on your local machine.
    
3.  **Remote-Exec Provisioner**  
    The wizard of the group! It runs commands directly on the remote server.
    

----------

## [](https://100daysdevops.hashnode.dev/day-81-of-100-days-terraform-provisioners-a-tale-of-automation-and-magic#heading-a-story-of-tainted-resources "Permalink")**A Story of Tainted Resources 🛑**

Sometimes, a provisioner might fail. In such cases, Terraform marks the resource as  **tainted**—meaning, it will destroy and recreate it during the next  `terraform apply`.

Why? Because Terraform wants to make sure your infrastructure is perfect! 🌟

----------

## [](https://100daysdevops.hashnode.dev/day-81-of-100-days-terraform-provisioners-a-tale-of-automation-and-magic#heading-lets-learn-by-doing-practical-demos "Permalink")**Let’s Learn By Doing: Practical Demos 🛠️**

### [](https://100daysdevops.hashnode.dev/day-81-of-100-days-terraform-provisioners-a-tale-of-automation-and-magic#heading-demo-1-using-the-file-provisioner "Permalink")**Demo 1: Using the File Provisioner**

Copy a file to an EC2 instance.

**Steps**:

1.  **Write Your Terraform Configuration**:
    

    ```
     provider "aws" {
       region = "ap-south-1"
     }
    
     resource "aws_instance" "example" {
       ami           = "ami-053b12d3152c0cc71" # Replace with a valid AMI
       instance_type = "t2.micro"
       key_name      = "your-key-name"
    
       provisioner "file" {
         source      = "hello.txt" # A file on your local machine
         destination = "/home/ec2-user/hello.txt"
       }
     }
    
    ```
    
2.  **Create the File to Be Copied**:  
    Create a file named  `hello.txt`  with this content:

    ```
     Hello from Terraform!
    
    ```
    
3.  **Run Terraform Commands**:
  
    ```
     terraform init
     terraform plan
     terraform apply
    
    ```
    
4.  **Check the Instance**: SSH into the instance and verify the file at  `/home/ec2-user/hello.txt`.
    

----------

### [](https://100daysdevops.hashnode.dev/day-81-of-100-days-terraform-provisioners-a-tale-of-automation-and-magic#heading-demo-2-using-the-local-exec-provisioner "Permalink")**Demo 2: Using the Local-Exec Provisioner**

Run a local shell command.

**Steps**:

1.  **Update Your Terraform Configuration**:
        
    ```
     resource "null_resource" "local_exec_example" {
       provisioner "local-exec" {
         command = "echo 'Terraform Local-Exec is running!'"
       }
     }
    
    ```
    
2.  **Run Terraform Commands**:
   
    ```
     terraform init
     terraform plan
     terraform apply
    
    ```
    
3.  **Output**: You’ll see the message in your terminal during the apply phase.
    

----------

### [](https://100daysdevops.hashnode.dev/day-81-of-100-days-terraform-provisioners-a-tale-of-automation-and-magic#heading-demo-3-using-the-remote-exec-provisioner "Permalink")**Demo 3: Using the Remote-Exec Provisioner**

Run a command on a remote EC2 instance.

**Steps**:

1.  **Write the Configuration**:
  
    ```
     resource "aws_instance" "example_with_remote_exec" {
       ami           = "ami-053b12d3152c0cc71"
       instance_type = "t2.micro"
       key_name      = "your-key-name"
    
       connection {
         type        = "ssh"
         user        = "ec2-user"
         private_key = file("path/to/your/private-key.pem")
         host        = self.public_ip
       }
    
       provisioner "remote-exec" {
         inline = [
           "sudo yum update -y",
           "echo 'Terraform Remote-Exec is awesome!' > /home/ec2-user/message.txt"
         ]
       }
     }
    
    ```
    
2.  **Run Terraform Commands**:

    ```
     terraform init
     terraform plan
     terraform apply
    
    ```
    
3.  **Verify**: SSH into the instance and check  `/home/ec2-user/message.txt`.
    

----------

## [](https://100daysdevops.hashnode.dev/day-81-of-100-days-terraform-provisioners-a-tale-of-automation-and-magic#heading-wrapping-it-up-the-magic-of-provisioners "Permalink")**Wrapping It Up: The Magic of Provisioners 🪄**

Provisioners are your go-to helpers in Terraform for executing tasks like copying files and running scripts. They add that extra touch of automation to your infrastructure, making it functional and ready to use.

Let’s celebrate the power of Terraform provisioners and keep learning together. Tomorrow awaits new adventures in the DevOps realm! 🎉
