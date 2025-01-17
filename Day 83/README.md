#  Securing Your Secrets with Vault and AppRole Authentication! 🔐
Welcome to Day 83 of our 100 Days of DevOps Journey! Over the past two days, we’ve learned how to securely integrate  **Vault**  with  **AWS EC2**  and set up  **AppRole Authentication**. This process allows us to manage and access secrets securely without compromising on security or scalability. Let’s dive into the key concepts and the steps you need to follow to make it all happen!

----------

### [](https://100daysdevops.hashnode.dev/day-83-of-100-days-securing-your-secrets-with-vault-and-approle-authentication#heading-why-vault "Permalink")Why Vault? 🔑

Vault is an incredibly powerful tool for managing secrets (e.g., API keys, passwords, tokens) securely. Think of it as a vault where you lock away sensitive information, and only trusted parties can access it.

In cloud environments like  **AWS**, you need to ensure that the applications and services accessing your sensitive data are  **authorized**  and  **authenticated**. With Vault, you can ensure that your secrets are protected and only accessible to trusted entities through methods like  **AppRole Authentication**.

----------

### [](https://100daysdevops.hashnode.dev/day-83-of-100-days-securing-your-secrets-with-vault-and-approle-authentication#heading-step-1-set-up-aws-ec2-with-ubuntu "Permalink")Step 1: Set Up AWS EC2 with Ubuntu 🌐

To start with, we created an AWS EC2 instance with Ubuntu. AWS EC2 gives us the power to run virtual servers on the cloud with just a few clicks. Once we’ve created an EC2 instance, we install Vault on it to store and manage our secrets.

Here are the basic steps for creating an EC2 instance (I'll dive deeper into each step in future blogs):

1.  Go to the AWS Management Console and navigate to the EC2 service.
    
2.  Launch a new EC2 instance with Ubuntu Server AMI.
    
3.  Select the appropriate instance type, configure the instance settings, and click "Launch" to create it.
    

Once the instance is ready, we can move on to installing Vault on it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737044251270/6d545593-7a96-4d65-8d2e-c22e8ab4a343.png?auto=compress,format&format=webp)

----------

### [](https://100daysdevops.hashnode.dev/day-83-of-100-days-securing-your-secrets-with-vault-and-approle-authentication#heading-step-2-install-vault-on-your-ec2-instance "Permalink")Step 2: Install Vault on Your EC2 Instance 🖥️

Now that we have our EC2 instance, it's time to install Vault. Here's the simplified process:

1.  **Install**  `gpg`: This helps us secure the download of Vault by verifying its authenticity:
    
 
    ```
     sudo apt update && sudo apt install gpg
    
    ```
    
2.  **Download the signing key**: This ensures Vault's official repository is trusted:
  
    
    ```
     wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
    
    ```
    
3.  **Add HashiCorp repo**: This allows us to install Vault directly from the official repository:
    
    
    ```
     echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
     sudo apt update
    
    ```
    
4.  **Install Vault**: With the repo added, we can install Vault:

    ```
     sudo apt install vault
    
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737044318984/10eeb13b-dc32-4363-8d89-13b8f9568f6a.png?auto=compress,format&format=webp)
    

----------

### [](https://100daysdevops.hashnode.dev/day-83-of-100-days-securing-your-secrets-with-vault-and-approle-authentication#heading-step-3-start-vault "Permalink")Step 3: Start Vault 🏁

Once Vault is installed, it’s time to start the Vault server. Use the command below to start Vault in "development mode" for testing purposes:

```
vault server -dev -dev-listen-address="0.0.0.0:8200"

```

This starts the Vault server and makes it accessible to other applications that need to authenticate and access secrets.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737044351102/550b7024-dce1-4f0f-a7bc-b3f676dbcfc0.png?auto=compress,format&format=webp)

### [](https://100daysdevops.hashnode.dev/day-83-of-100-days-securing-your-secrets-with-vault-and-approle-authentication#heading-step-4-enable-approle-authentication-in-vault "Permalink")Step 4: Enable AppRole Authentication in Vault 🔐

AppRole Authentication ensures that only trusted applications or machines can access your secrets. Here's how you can enable and configure it in Vault:

1.  **Enable AppRole Authentication**: This command enables AppRole authentication in Vault:
 
    ```
     vault auth enable approle
    
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737044397491/908ce682-644c-4c11-a7a8-5921fe1e9bb3.png?auto=compress,format&format=webp)
    
2.  **Create a Policy**: Policies define the permissions of a particular role. For example, we create a  **terraform**  policy that allows access to secrets:
  
    ```
     vault policy write terraform - <<EOF
     path "*" {
       capabilities = ["list", "read"]
     }
     path "secret/data/*" {
       capabilities = ["create", "read", "update", "delete", "list"]
     }
     EOF
    
    ```
    
3.  **Create an AppRole**: Now, we create an AppRole with specific policies. The AppRole will have access to secrets for Terraform, with limited usage times and permissions:

    
    ```
     vault write auth/approle/role/terraform \
         secret_id_ttl=10m \
         token_num_uses=10 \
         token_ttl=20m \
         token_max_ttl=30m \
         secret_id_num_uses=40 \
         token_policies=terraform
    
    ```
    
4.  **Generate Role ID and Secret ID**: After creating the AppRole, you need two credentials: the  **Role ID**  and the  **Secret ID**. These allow Terraform to authenticate with Vault:
    
    -   **Get Role ID**:
       
        ```
          vault read auth/approle/role/terraform/role-id
        
        ```
        
    -   **Generate Secret ID**:
   
        
        ```
          vault write -f auth/approle/role/terraform/secret-id
        
        ```
        

----------

### [](https://100daysdevops.hashnode.dev/day-83-of-100-days-securing-your-secrets-with-vault-and-approle-authentication#heading-aws-concept-integration-how-does-this-all-fit-together "Permalink")AWS Concept Integration: How Does This All Fit Together? 🤔

Just like AWS provides services to securely manage access to cloud resources (e.g., IAM roles for EC2), Vault provides a way to securely manage access to sensitive secrets. When you use  **AppRole**  in Vault, it’s similar to how you assign  **IAM roles**  in AWS.

-   In  **AWS**, IAM roles are used to give EC2 instances permissions to access other AWS services securely.
    
-   In  **Vault**, AppRole is used to securely grant applications or machines the ability to access secrets, such as API keys or tokens.
    

By integrating Vault with AWS EC2, you ensure that only trusted instances and applications can access sensitive data, just like how IAM roles secure access to AWS resources.

----------

### [](https://100daysdevops.hashnode.dev/day-83-of-100-days-securing-your-secrets-with-vault-and-approle-authentication#heading-conclusion "Permalink")Conclusion

In this blog, we’ve learned how to securely set up  **Vault**  on an AWS EC2 instance, enable  **AppRole Authentication**, and generate credentials that allow apps to access secrets securely. This is a critical skill for DevOps engineers who need to manage secrets and sensitive information in a safe and organized way.

Stay tuned for Day 84, where we’ll dive deeper into configuring Terraform to interact with Vault securely and automate our workflows. Let’s keep pushing forward on this exciting DevOps journey!
