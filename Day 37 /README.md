# Launching an EC2 Instance on AWS : A Practical Guide
Welcome to  **Day 37**  of my 100 Days of DevOps Journey! Today, we dive into the world of AWS, specifically learning how to create an  **EC2 instance**  while understanding the foundational concepts of regions, availability zones, and more .

----------

### [](https://100daysdevops.hashnode.dev/day-38-of-100-days-launching-an-ec2-instance-on-aws-a-practical-guide#heading-understanding-ec2-instances-and-key-concepts "Permalink")**Understanding EC2 Instances and Key Concepts**

#### [](https://100daysdevops.hashnode.dev/day-38-of-100-days-launching-an-ec2-instance-on-aws-a-practical-guide#heading-1-what-is-an-ec2-instance "Permalink")**1. What is an EC2 Instance?**

Amazon EC2 (Elastic Compute Cloud) provides scalable virtual servers in the cloud, enabling you to deploy applications effortlessly.

#### [](https://100daysdevops.hashnode.dev/day-38-of-100-days-launching-an-ec2-instance-on-aws-a-practical-guide#heading-2-why-regions-and-availability-zones-matter "Permalink")**2. Why Regions and Availability Zones Matter**

-   **Regions**: Physical locations worldwide (e.g., Mumbai, Frankfurt) where AWS has its data centers.
    
    -   **Latency Reduction**: Hosting your servers closer to users minimizes latency.
        
    -   **Compliance**: Certain industries or customers mandate data residency within specific regions (e.g., European banks requiring data within Europe).
        
-   **Availability Zones**: Each region contains multiple data centers (AZs), ensuring  **high availability**  and  **disaster recovery**.
    

----------

### [](https://100daysdevops.hashnode.dev/day-38-of-100-days-launching-an-ec2-instance-on-aws-a-practical-guide#heading-step-by-step-guide-creating-your-first-ec2-instance "Permalink")**Step-by-Step Guide: Creating Your First EC2 Instance**

Here’s a hands-on guide to creating an EC2 instance on AWS. Follow along with the screenshots for clarity!

----------

#### [](https://100daysdevops.hashnode.dev/day-38-of-100-days-launching-an-ec2-instance-on-aws-a-practical-guide#heading-step-1-login-to-aws-console "Permalink")**Step 1: Login to AWS Console**

-   Navigate to the  [AWS Management Console](https://aws.amazon.com/console/).
    
-   Use your login credentials to access the dashboard.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732891274010/4a26452f-369e-4ce1-9573-28be32ec719d.png?auto=compress,format&format=webp)
    

----------

#### [](https://100daysdevops.hashnode.dev/day-38-of-100-days-launching-an-ec2-instance-on-aws-a-practical-guide#heading-step-2-navigate-to-the-ec2-service "Permalink")**Step 2: Navigate to the EC2 Service**

-   In the search bar, type "EC2" and click on the  **EC2 Service**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732891346013/d9083146-b456-47d1-b47f-50807b35d90a.png?auto=compress,format&format=webp)

----------

#### [](https://100daysdevops.hashnode.dev/day-38-of-100-days-launching-an-ec2-instance-on-aws-a-practical-guide#heading-step-3-click-on-launch-instance "Permalink")**Step 3: Click on "Launch Instance"**

-   On the EC2 dashboard, click  **Launch Instance**  to start the instance creation process.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732891382331/4a76e437-77e5-4c1a-a9d2-ece943fe86e6.png?auto=compress,format&format=webp)

----------

#### [](https://100daysdevops.hashnode.dev/day-38-of-100-days-launching-an-ec2-instance-on-aws-a-practical-guide#heading-step-4-configure-your-instance "Permalink")**Step 4: Configure Your Instance**

1.  **Name Your Instance**
    
    -   Enter a meaningful name (e.g., poc_vm).
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732891435795/117e9e9e-1f48-4683-9e13-8a403c5c13cc.png?auto=compress,format&format=webp)
        

2.  **Select an Operating System**
    
    -   Choose an OS for your instance. For example:
        
        -   Ubuntu
            
        -   Amazon Linux
            
        -   Red Hat
            
    -   Ensure it’s marked  **Free Tier Eligible**.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732891483306/126e16cb-acd2-4b90-9b6b-9df6a6b5c1c3.png?auto=compress,format&format=webp)
        

3.  **Instance Type**
    
    -   Select  `t2.micro`  for free-tier eligibility (1 vCPU, 1 GB RAM).
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732891516499/b5d7ae05-0ac5-4c0b-86b1-639880598cec.png?auto=compress,format&format=webp)
        

4.  **Key Pair Configuration**
    
    -   Create or select a  **key pair**  to securely access your instance.
        
    -   Save the private key file (.pem) in a secure location.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732891545802/ffcc4466-52b9-4109-894c-0a86125ce3b0.png?auto=compress,format&format=webp)
        

----------

#### [](https://100daysdevops.hashnode.dev/day-38-of-100-days-launching-an-ec2-instance-on-aws-a-practical-guide#heading-step-5-configure-network-settings "Permalink")**Step 5: Configure Network Settings**

-   Use default settings or customize them for your use case (e.g., allow SSH access).
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732891580296/7ddee3a6-888e-46d7-99fd-8ea5cdd96cd7.png?auto=compress,format&format=webp)
    

----------

#### [](https://100daysdevops.hashnode.dev/day-38-of-100-days-launching-an-ec2-instance-on-aws-a-practical-guide#heading-step-6-launch-your-instance "Permalink")**Step 6: Launch Your Instance**

-   Review your configuration and click  **Launch Instance**.
    
-   You will be redirected to a status page where you can see the instance being initialized.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1732891614503/cabb5e8b-5321-47c9-a415-9792085dab25.png?auto=compress,format&format=webp)
    

----------

### [](https://100daysdevops.hashnode.dev/day-38-of-100-days-launching-an-ec2-instance-on-aws-a-practical-guide#heading-important-notes "Permalink")**Important Notes**

1.  **Free Tier Limits**:
    
    -   AWS offers 750 hours/month for free-tier EC2 instances.
        
    -   Exceeding this limit or using non-eligible resources will incur charges.
        
2.  **Security Best Practices**:
    
    -   Never share your private key.
        
    -   Use SSH to access your instance securely.
        
3.  **Resource Cleanup**:
    
    -   Always  **stop**  or  **terminate**  unused instances to avoid unnecessary charges.

----------

### [](https://100daysdevops.hashnode.dev/day-38-of-100-days-launching-an-ec2-instance-on-aws-a-practical-guide#heading-whats-next "Permalink")**What’s Next?**

In the upcoming blogs, I’ll explore:

-   Connecting to the EC2 instance using SSH.
    
-   Deploying applications on EC2.
    
-   High Availability and Scaling concepts.
    

----------

### [](https://100daysdevops.hashnode.dev/day-38-of-100-days-launching-an-ec2-instance-on-aws-a-practical-guide#heading-conclusion "Permalink")**Conclusion**

And there you have it! 🚀 Today, we successfully launched our very own EC2 instance, taking one more confident step in mastering cloud computing. Each click and configuration taught us something new, and now, the power of AWS feels just a bit more within our grasp. Here’s to many more milestones on this journey—let’s keep building, learning, and growing! 🌟
