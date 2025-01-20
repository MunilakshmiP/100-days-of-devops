# Ansible
Today marks  **Day 85**  of my 100 Days of DevOps journey, and I’m diving deep into one of the most powerful configuration management and automation tools in the DevOps world:  **Ansible**. Let’s explore why Ansible has become the go-to tool for many system administrators and DevOps engineers and how it simplifies everyday tasks.

----------

## [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-why-configuration-management-matters "Permalink")**Why Configuration Management Matters**

Over the past decade, the role of system administrators has evolved dramatically. Ten years ago, managing physical servers was the norm, and provisioning them was a manual and time-consuming process. Tasks like configuring software, managing dependencies, and deploying applications often took hours or even days to complete.

Fast forward to today, where configuration management tools like  **Ansible**,  **Puppet**,  **Chef**, and  **SaltStack**  have revolutionized the way we manage infrastructure. These tools help automate repetitive tasks, ensuring consistency and reliability across multiple servers. Among them, Ansible stands out for its simplicity and ease of use.

----------

## [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-a-simple-example-manual-vs-automated-management "Permalink")**A Simple Example: Manual vs. Automated Management**

### [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-the-old-way-manual-configuration "Permalink")**The Old Way: Manual Configuration**

Imagine a system administrator tasked with installing and configuring a web server on 10 physical servers:

1.  SSH into each server individually.
    
2.  Update system packages.
    
3.  Install the necessary software (e.g., Nginx or Apache).
    
4.  Configure the server files manually.
    
5.  Restart the service to apply changes.
    

Now multiply that effort across 100+ servers. It’s exhausting, error-prone, and difficult to scale.

### [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-the-ansible-way "Permalink")**The Ansible Way**

With Ansible, all these tasks can be automated using a  **playbook**:


```
- name: Configure Web Servers
  hosts: web_servers
  tasks:
    - name: Update packages
      apt:
        update_cache: yes
    - name: Install Nginx
      apt:
        name: nginx
        state: present
    - name: Start Nginx
      service:
        name: nginx
        state: started

```

Run the playbook, and Ansible will handle the rest. No more manual SSH sessions, no room for inconsistencies, and tasks that used to take hours now take minutes.

----------

## [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-why-ansible-comparing-with-puppet-chef-and-saltstack "Permalink")**Why Ansible? Comparing with Puppet, Chef, and SaltStack**

While tools like  **Puppet**,  **Chef**, and  **SaltStack**  are great, Ansible offers several advantages:

-   **Agentless**: Unlike Puppet or Chef, Ansible doesn’t require installing agents on managed nodes. It communicates over SSH.
    
-   **Simple Syntax**: Ansible uses YAML for its playbooks, making it easy to read and write.
    
-   **Quick to Get Started**: Ansible’s setup is straightforward. You don’t need a separate master server or extensive configuration.
    
-   **Wide Use Cases**: Ansible supports configuration management, provisioning, application deployment, CI/CD, and network automation.
    

----------

## [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-what-ansible-excels-at "Permalink")**What Ansible Excels At**

1.  **Configuration Management**: Maintain consistent configurations across all nodes.
    
2.  **Provisioning**: Quickly set up servers, virtual machines, or containers.
    
3.  **Application Deployment**: Streamline CI/CD pipelines with automated deployments.
    
4.  **Network Automation**: Manage network devices like switches, routers, and firewalls.
    
5.  **Control and Manage Nodes**: Easily scale up or down, run ad-hoc commands, and monitor systems.
    

----------

## [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-choosing-between-ansible-shell-scripts-and-python-automation "Permalink")**Choosing Between Ansible, Shell Scripts, and Python Automation**

While Ansible, shell scripts, and Python scripts can all automate tasks, each has its ideal use case:

### [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-shell-scripts "Permalink")**Shell Scripts**

-   Best for: Simple, quick tasks or one-off automation.
    
-   Example: Automating backups or cleaning up logs.
    
-   Limitation: Difficult to maintain and scale for complex workflows.
    

### [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-python-automation "Permalink")**Python Automation**

-   Best for: Custom solutions requiring logic or integrations.
    
-   Example: Writing a script to interact with APIs.
    
-   Limitation: Requires more effort for repetitive tasks that tools like Ansible simplify.
    

### [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-ansible "Permalink")**Ansible**

-   Best for: Managing multiple servers or infrastructure at scale.
    
-   Example: Deploying an application to 100+ servers with consistent configurations.
    
-   Limitation: Not suitable for highly custom workflows that require advanced logic (better handled by Python).
    

**Key Takeaway**: Use shell scripts for simple tasks, Python for logic-heavy workflows, and Ansible for managing infrastructure at scale.

----------

## [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-ansible-vs-terraform-provisioning-comparison "Permalink")**Ansible vs. Terraform: Provisioning Comparison**

Both Ansible and Terraform are provisioning tools, but they serve slightly different purposes:

-   **Ansible**: Focuses on configuration management and provisioning tasks post-deployment. Ideal for ongoing server management.
    
-   **Terraform**: Specializes in infrastructure provisioning as code (IaC). It’s best for creating cloud resources like VMs, networks, and storage.
    

**Verdict**: For provisioning,  **Terraform**  is the better choice due to its state management and infrastructure orchestration capabilities. However, Ansible is excellent for configuring and maintaining those resources after they’re provisioned.

----------

## [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-how-to-install-ansible-on-an-ec2-instance "Permalink")**How to Install Ansible on an EC2 Instance**

Follow these steps to set up Ansible on an EC2 instance:

### [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-step-1-launch-an-ec2-instance "Permalink")**Step 1: Launch an EC2 Instance**

1.  Log in to the AWS Console.
    
2.  Create an EC2 instance with an  **Ubuntu**  or other Linux AMI.
    
3.  Choose a free-tier instance type (e.g.,  `t2.micro`).
    
4.  Configure security groups to allow SSH (port 22).
    
5.  Launch the instance and connect via SSH.
    

### [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-step-2-update-and-install-ansible "Permalink")**Step 2: Update and Install Ansible**

1.  Connect to your instance:
    
    
    
    ```
     ssh -i <your-key.pem> ubuntu@<instance-public-ip>
    
    ```
    
2.  Update the package list:
    
    
    
    ```
     sudo apt update
     sudo apt upgrade -y
    
    ```
    
3.  Install Ansible:
    
    
    
    ```
     sudo apt install ansible -y
    
    ```
    
4.  Verify installation:
    

    
    ```
     ansible --version
    
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737298694030/a916e2ca-8051-43bf-bc57-49a77027e5c3.png?auto=compress,format&format=webp)
    

----------

### [](https://100daysdevops.hashnode.dev/day-85-of-100-days-exploring-ansible#heading-conclusion "Permalink")**Conclusion**

Ansible simplifies the complex world of configuration management and automation, making it a vital tool for DevOps professionals. Whether you’re provisioning servers, automating deployments, or managing configurations, Ansible’s versatility and ease of use make it a game-changer.

With just 15 days left in this journey, I can confidently say that Ansible has become one of my favorite tools in the DevOps toolkit. Try it out and see how it can transform your workflows!
