# Understanding VPCs, Security Groups, and NACLs in AWS 🔐
As DevOps engineers, securing our applications in the cloud is critical. On Day 40, we explore Virtual Private Clouds (VPCs), subnets, security layers, and the differences between Security Groups and Network Access Control Lists (NACLs). Understanding these concepts is key to building a robust and secure cloud infrastructure. Additionally, we’ll walk through a practical example of creating a VPC and launching an EC2 instance to solidify these concepts.

----------

## [](https://100daysdevops.hashnode.dev/day-41-of-100-days-understanding-vpcs-security-groups-and-nacls-in-aws#heading-what-is-a-vpc "Permalink")🚀  **What is a VPC?**

A  **Virtual Private Cloud (VPC)**  is an isolated network in AWS that lets you manage your cloud resources securely. It acts as your private network in the AWS environment. When creating a VPC, you define an IP address range, which determines its size. For example, if the IP range is  `10.1.0.0/16`, the VPC can host up to  **65,536 IP addresses**.

Within a VPC, you can create  **subnets**:

-   **Public Subnets**: Accessible via the internet.
    
-   **Private Subnets**: Internal-facing and not exposed to the internet.
    

----------

## [](https://100daysdevops.hashnode.dev/day-41-of-100-days-understanding-vpcs-security-groups-and-nacls-in-aws#heading-how-traffic-flows-in-a-vpc "Permalink")🌉  **How Traffic Flows in a VPC**

Here’s a high-level overview:

1.  **Internet Gateway**: Connects your public subnet to the internet.
    
2.  **Load Balancer**: Serves as an intermediary, routing requests from users to private subnets.
    
3.  **Security Groups and NACLs**: Add additional layers of security.
    

----------

## [](https://100daysdevops.hashnode.dev/day-41-of-100-days-understanding-vpcs-security-groups-and-nacls-in-aws#heading-security-groups-vs-nacls "Permalink")🔑  **Security Groups vs. NACLs**

AWS provides  **shared responsibility security**, where AWS ensures infrastructure security, and users secure their applications. Two critical components in this shared responsibility are  **Security Groups**  and  **NACLs**.

### [](https://100daysdevops.hashnode.dev/day-41-of-100-days-understanding-vpcs-security-groups-and-nacls-in-aws#heading-1-security-groups "Permalink")**1. Security Groups**

-   **Instance-Level Security**: Security Groups operate at the EC2 instance level.
    
-   **Inbound and Outbound Rules**:
    
    -   **Inbound Traffic**: Manages requests coming into your EC2 instance.
        
    -   **Outbound Traffic**: Manages requests from your EC2 instance to the internet or other resources.
        
-   By default, all inbound traffic is denied, and all outbound traffic is allowed.
    
-   Example Use Case:
    
    -   Allow port  `8080`  for a web application.
        
    -   Block all unused ports to prevent malicious access.
        

### [](https://100daysdevops.hashnode.dev/day-41-of-100-days-understanding-vpcs-security-groups-and-nacls-in-aws#heading-2-nacls-network-access-control-lists "Permalink")**2. NACLs (Network Access Control Lists)**

-   **Subnet-Level Security**: NACLs provide security at the subnet level.
    
-   **Stateless Rules**: NACLs allow you to explicitly allow or deny traffic.
    
-   Can be applied to multiple subnets and affect all resources within them.
    

----------

## [](https://100daysdevops.hashnode.dev/day-41-of-100-days-understanding-vpcs-security-groups-and-nacls-in-aws#heading-practical-creating-a-vpc-and-launching-an-ec2-instance "Permalink")🛠️  **Practical: Creating a VPC and Launching an EC2 Instance**

Let’s implement what we’ve learned by creating a VPC, launching an EC2 instance, and configuring Security Groups and NACLs.

----------

### [](https://100daysdevops.hashnode.dev/day-41-of-100-days-understanding-vpcs-security-groups-and-nacls-in-aws#heading-step-1-create-a-vpc "Permalink")**Step 1: Create a VPC**

1.  Navigate to the  **VPC**  section in the AWS Management Console.
    
2.  Choose  **"VPC and More"**  to allow AWS to create default resources for the VPC automatically.
    
    -   **Resources AWS creates by default**:
        
        -   Public and private subnets in two availability zones (e.g.,  `us-east-1a`  and  `us-east-1b`).
            
        -   Internet Gateway (IGW).
            
        -   Route Tables.
            
        -   VPC Endpoints for S3 (optional).
            
3.  **Provide a Name**  for the VPC (e.g.,  `Demo VPC`).
    
4.  Configure the  **CIDR Block**:
    
    -   `/16`  gives you 65,536 IP addresses.
        
    -   `/24`  gives you 256 IP addresses.
        
    -   Choose based on your requirements.
        
5.  Configure the  **Number of Availability Zones and Subnets**:
    
    -   You can use the default settings (2 AZs with both public and private subnets).
6.  Click  **Create VPC**.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732950351336/e855e6a7-bb6e-4829-a136-9937b9150834.png?auto=compress,format&format=webp)

----------

### [](https://100daysdevops.hashnode.dev/day-41-of-100-days-understanding-vpcs-security-groups-and-nacls-in-aws#heading-step-2-launch-an-ec2-instance "Permalink")**Step 2: Launch an EC2 Instance**

1.  Navigate to the  **EC2**  section in AWS Management Console.
    
2.  Click  **"Launch Instance"**.
    
3.  Configure the instance:
    
    -   Instance Name:  `Demo Instance`.
        
    -   AMI: Choose  **Ubuntu**.
        
    -   Instance Type:  **t2.micro**.
        
    -   Key Pair: Select an existing one or create a new one.
        
4.  **Network Configuration**:
    
    -   Select your  **Custom VPC**  (`Demo VPC`).
        
    -   Change the subnet to  **Public Subnet**.
        
    -   Assign a  **Public IP Address**.
        
5.  Click  **Launch Instance**.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732950490468/16e3d738-9494-4574-81ce-ad13c112dd29.png?auto=compress,format&format=webp)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732950543587/1e3c3897-e232-4e19-a6a3-f5439e46e556.png?auto=compress,format&format=webp)

----------

### [](https://100daysdevops.hashnode.dev/day-41-of-100-days-understanding-vpcs-security-groups-and-nacls-in-aws#heading-step-3-access-the-ec2-instance "Permalink")**Step 3: Access the EC2 Instance**

1.  Open a terminal and SSH into the EC2 instance:
    
    Copy
    
    Copy
    
    ```
     ssh -i "your-key.pem" ubuntu@<public-ip-address>
    
    ```
    
2.  Update packages:
    
    Copy
    
    Copy
    
    ```
     sudo apt update
    
    ```
    
3.  Run a simple Python HTTP server:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732950815595/62014785-d6e0-4d21-8e1a-6352242ccdf6.png?auto=compress,format&format=webp)
    

----------

### [](https://100daysdevops.hashnode.dev/day-41-of-100-days-understanding-vpcs-security-groups-and-nacls-in-aws#heading-step-4-test-application-accessibility "Permalink")**Step 4: Test Application Accessibility**

1.  Open your browser and navigate to:
    
    
    ```
     http://<public-ip-address>:8000
    
    ```
    
2.  The application might fail to load because:
    
    -   The  **default security group**  only allows SSH traffic (Port 22).
3.  Modify the security group to allow traffic on Port 8000:
    
    -   Add an  **Inbound Rule**  for Port 8000 with  **Source: 0.0.0.0/0**.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732951373665/1367b333-a958-47d1-936e-22a58ce07ea1.png?auto=compress,format&format=webp)
        

### [](https://100daysdevops.hashnode.dev/day-41-of-100-days-understanding-vpcs-security-groups-and-nacls-in-aws#heading-step-5-test-application-behavior-post-configuration "Permalink")Step 5:  **Test Application Behavior Post Configuration**

1.  After updating security groups and testing NaCl rules, access the application again via:
   
    
    ```
     http://<public-ip-address>:8000
    
    ```
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732951449257/56839c27-3503-4dca-baa0-b4e4003edcce.png?auto=compress,format&format=webp)

## [](https://100daysdevops.hashnode.dev/day-41-of-100-days-understanding-vpcs-security-groups-and-nacls-in-aws#heading-wrapping-it-up "Permalink")**Wrapping It Up**🌟

Today, we unlocked the doors to secure cloud networking with AWS VPCs, Security Groups, and NACLs. These powerful tools ensure that your applications are not just functional but also fortified against threats. By mastering these concepts and applying best practices, you're laying a strong foundation for building scalable and secure cloud infrastructures.

Keep exploring, experimenting, and expanding your knowledge—each step brings you closer to DevOps mastery! See you on Day 41 for another exciting learning journey! 🚀
