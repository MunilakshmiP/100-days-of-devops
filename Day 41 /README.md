# Securing AWS Applications with VPC: A Step-by-Step Guide
In this blog, we'll dive into the concept of setting up a **Virtual Private Cloud (VPC)** in AWS to securely deploy your applications. This is a must-have skill for anyone preparing for AWS-related interviews, and it’s also one of the best practices recommended by AWS for production-grade applications.

### **Project Overview**

In this project, you will learn how to:

1.  Create a **VPC** (Virtual Private Cloud) on AWS.
    
2.  Secure applications within the VPC.
    
3.  Utilize components like **subnets**, **load balancers**, **NAT gateways**, and **auto scaling groups** to ensure your infrastructure is both secure and highly available.
    

Here's a high-level overview of the architecture we'll implement:

-   **VPC**: We'll create a VPC with public and private subnets.
    
-   **Public Subnet**: The public subnet will host resources like **load balancers** and **NAT gateways**.
    
-   **Private Subnet**: Your application will reside here, ensuring it’s not directly accessible from the internet.
    
-   **High Availability**: We'll deploy the architecture in **two availability zones** to ensure high availability and fault tolerance.
    

### **Why Two Availability Zones?**

You may wonder why we need two availability zones instead of one. The answer is simple: **redundancy**. If one AWS availability zone goes down due to any issue, the other availability zone can still handle the traffic, ensuring your application stays available. This is an important consideration for production environments.

### **Components of the Architecture**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732958366675/6e55d99c-d6f3-4586-8ec1-305890d1d10c.png)

#### **1. VPC with Public and Private Subnets**

A **VPC** provides a virtual network within AWS. For this project, we will set up:

-   **Public Subnets**: These subnets will host resources that need to be accessible from the internet, like **load balancers** and **NAT gateways**.
    
-   **Private Subnets**: These are for your application servers that do not need to be exposed to the public internet.
    

#### **2. Load Balancer and NAT Gateway**

-   **Load Balancer**: It helps distribute incoming traffic across multiple instances, improving the availability and reliability of your applications. The load balancer can also perform path-based or host-based routing to direct traffic to the correct instances.
    
-   **NAT Gateway**: Applications in private subnets often need to access the internet (e.g., to fetch updates or call external APIs). A **NAT gateway** allows these private instances to access the internet securely, by masking their private IP addresses with a public one.
    

#### **3. Auto Scaling Group**

An **auto scaling group** ensures your application can scale based on demand. For instance, if the number of incoming requests spikes, the auto scaling group can automatically add more EC2 instances to handle the load, ensuring no downtime.

#### **4. Bastion Host**

To enhance security, applications in private subnets do not have public IPs. **Bastion hosts** are used to provide a secure entry point into these private instances. You can connect to the private instances through the bastion host, which acts as a jump server, ensuring your application remains secure.

----------

### **Steps to Implement the Architecture**

Now that we have an understanding of the architecture, let's look at how to implement it step-by-step.

#### **Step 1: Create VPC with Public and Private Subnets**

1.  **Navigate to VPC Dashboard**: In your AWS Management Console, search for **VPC** and click on **Create VPC**.
    
2.  Choose **VPC and more** for a more automated setup.
    
3.  Select **IPv4 configuration** and **two availability zones** for your VPC.
    
4.  Add **public and private subnets** in both availability zones.
    
5.  AWS will automatically create route tables and associate them with the subnets. Ensure that:
    
    -   The **public subnets** have a route to the **internet gateway**.
        
    -   The **private subnets** have routes set up to access the **NAT gateway** for internet access.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732959145063/adfcc8ac-b530-489a-8be9-5a4be59249a9.png)![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732960364025/78a63945-85eb-44a5-8c95-2052da2d75b9.png)

#### **Step 2: Set Up NAT Gateway and Load Balancer**

1.  **Create NAT Gateway**: Go to **NAT Gateways** in your VPC and create a NAT gateway in one of the public subnets. This will be used by instances in the private subnet to access the internet.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732959028269/ac7613ee-4624-44f5-808e-15fafc52c645.png)
2.  **Set Up Load Balancer**: Create an **Application Load Balancer** (ALB) or **Network Load Balancer** (NLB) in the public subnet to distribute traffic across your EC2 instances in the private subnet.
    

#### **Step 3: Implement Auto Scaling Group**

1.  In the EC2 console, create an **auto scaling group** that will launch EC2 instances within your private subnets.
    
2.  Set a minimum and maximum number of instances, based on your traffic needs. The auto scaling group will automatically adjust the number of instances based on the incoming traffic.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732960836311/5ae76a2a-cd5c-4c4f-9ade-bf43e105ddc9.png)
    
    Create a launch template and add that in auto scaling group . here i have a created a (eg .. aws-prod-example) launch template .  
    in the launch template we have to mention like the name and the instance type , networking components like ssh on port 22 and to deploy our application on port 8000 - create like this and give launch template .
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732961128164/24b21f56-2bb3-439c-bfdf-ace941ae95ca.png)
    
    add our aws-prod-example vpc , and two private subnets and click on next
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732961284391/5ca6df2f-fe91-4488-976f-c8ed09e544a5.png)![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732961310232/09129088-b136-417b-a678-0d917531dd97.png)![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732961338437/feb53249-9970-4676-a66f-be139827f09e.png)

**Step 4 . Creating a Bastion Host in AWS**

A **Bastion Host** acts as a secure entry point for SSH access into private instances within a VPC.

#### **1: Launch the Bastion Host**

1.  Navigate to the **EC2 Dashboard** and launch a new **Ubuntu instance** (T2 Micro).
    
2.  Make sure the **Bastion Host** is in the same **VPC** as your private instances.
    
3.  Assign a **public IP** to the instance for remote access.
    
4.  Configure the **Security Group** to allow **SSH (port 22)** access from your IP.
    

Now, you can SSH into the Bastion Host using the key pair you created during the launch.

#### **2 : SSH Access to Private Instances**

To access private instances via the Bastion Host, you'll need to transfer your private key and connect securely:

1.  **Transfer the private key** from your local machine to the Bastion Host using **SCP**:
    
    ```bash
    scp -i /path/to/private-key.pem /path/to/aws-login.pem ubuntu@<bastion-public-ip>:/home/ubuntu/
    ```
    
2.  SSH into the Bastion Host:
    
    ```bash
    ssh -i /path/to/aws-login.pem ubuntu@<bastion-public-ip>
    ```
    
3.  From the Bastion Host, SSH into the private instance using its **private IP**:
    
    ```bash
    ssh -i /path/to/aws-login.pem ubuntu@<private-ip-address>
    ```
    

----------

### **Step 5 . Installing a Simple Python Application on Private Instances**

Once you have SSH access, you can install a simple Python application to run on your private instances.

#### **Step 1: Create an HTML File**

Create a basic HTML file (`index.html`) on the private instance:

```http
<html>
  <head><title>My First AWS Project</title></head>
  <body><h1>Welcome to my AWS App!</h1></body>
</html>
```

#### **Step 2: Run a Python HTTP Server**

To serve the HTML file, start a simple Python HTTP server:

```bash
python3 -m http.server 8000
```

This will host the application on the private instance's **private IP** at port 8000.

----------

### **Step 6 . Setting Up an Application Load Balancer**

Now, let’s set up an **Application Load Balancer (ALB)** to distribute traffic between two instances—one running the Python app and another idle instance.

#### **Step 1: Create the Load Balancer**

1.  Navigate to **Load Balancers** in the **EC2 Console** and click **Create Load Balancer**.
    
2.  Choose **Application Load Balancer (ALB)**.
    
3.  Select your **VPC** and public subnets, ensuring the load balancer is **internet-facing**.
    
4.  Configure security settings for your ALB and listeners (HTTP/HTTPS).
    

#### **Step 2: Create a Target Group and Register Instances**

1.  Create a **Target Group** with **HTTP** as the protocol.
    
2.  Register the private instances—one with the Python app and another idle instance—under this target group.
    

#### **Step 3: Attach Load Balancer to the Target Group**

1.  Attach the newly created target group to the load balancer.
    
2.  Set up the listener to route traffic on port **80**.
    

The load balancer will now distribute incoming traffic between the two instances based on availability.

----------

### **Step 7 . Testing and Verifying the Setup**

To test the configuration, you can use the **load balancer’s DNS name** to check if the setup is working as expected.

Run the following command to see if traffic is being directed to the correct instance:

```bash
curl http://<load-balancer-dns>
```

You should see the **Python app’s HTML page** if the traffic is routed correctly to the instance running the app.

----------

### **Conclusion**

Setting up a **Bastion Host**, **SSH access**, and an **Application Load Balancer** in AWS is an important skill for anyone working with cloud infrastructure. This architecture ensures secure access to private instances, while also providing a scalable solution to distribute traffic across multiple instances, improving availability and performance.
