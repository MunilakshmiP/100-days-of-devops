## Vault and Terraform Integration Continued!
welcome back to Day 84 of our DevOps journey! Yesterday, we learned how to integrate Vault with Terraform and create some key-value pairs. Today, we're going to continue the magic! 🪄 We'll dive deeper into Vault, create a Key-Value (KV) secret, and understand how to fetch that secret dynamically inside our AWS infrastructure using Terraform. Let’s make it as simple as a story!

----------

### [](https://100daysdevops.hashnode.dev/day-84-of-100-days-vault-and-terraform-integration-continued#heading-recap-what-we-did-yesterday "Permalink")**Recap: What We Did Yesterday**

Yesterday, we had a great time setting up the integration between Vault and Terraform. We created the necessary  **AppRole**,  **policies**, and  **secrets**  inside Vault. How amazing was that, right? By the end of it, we had Vault securely storing secrets, and Terraform ready to pull those secrets into our infrastructure.

Today, we will continue from where we left off, building upon the knowledge we gained. We'll add more magic to our Terraform code by pulling secret data directly from Vault and using it in AWS!

----------

### [](https://100daysdevops.hashnode.dev/day-84-of-100-days-vault-and-terraform-integration-continued#heading-step-1-creating-a-key-value-pair-in-vault-a-simple-concept "Permalink")**Step 1: Creating a Key-Value Pair in Vault (A Simple Concept)**

Imagine Vault as a big treasure chest, and inside this chest, you can store important secrets (like passwords or API keys). We can access these secrets whenever we need them.

So, let’s first create a  **Key-Value pair**  in Vault. In this example, we will store a key called  `username`  and assign it a value  `muni`. Think of it like writing a little note inside the chest saying "Hey, the username is 'muni'!"

#### [](https://100daysdevops.hashnode.dev/day-84-of-100-days-vault-and-terraform-integration-continued#heading-how-to-create-the-kv-pair-in-vault "Permalink")**How to Create the KV Pair in Vault**

-   First, we’ll go to Vault’s UI or use the command line to add a secret.
    
-   **Path**:  `/secret/data/test-secret`  (You can name it anything you like!)
    
-   **Key-Value Pair**: We’ll store a key called  `username`  with the value  `muni`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737047748797/b20a175e-4c50-4ac7-9dd3-bef088c754d6.png?auto=compress,format&format=webp)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737047799424/e2ac4623-ec8b-4356-807e-9ad706f50e64.png?auto=compress,format&format=webp)
    

Let's say we are using the command line to add a secret, like this:



```
vault kv put secret/test-secret username=muni

```

This command will add a secret called  `test-secret`  at the  `/secret`  path and inside it, there’s a key  `username`  with the value  `muni`. 📜

----------

### [](https://100daysdevops.hashnode.dev/day-84-of-100-days-vault-and-terraform-integration-continued#heading-step-2-terraform-code-to-fetch-secrets "Permalink")**Step 2: Terraform Code to Fetch Secrets**

Now that we’ve stored our secret in Vault, it’s time to fetch it with Terraform and use it in our AWS instance. Let’s go step-by-step, just like how a superhero prepares for battle, one tool at a time! 🦸‍♀️🦸‍♂️

#### [](https://100daysdevops.hashnode.dev/day-84-of-100-days-vault-and-terraform-integration-continued#heading-the-main-terraform-configuration-maintfhttpmaintf "Permalink")**The Main Terraform Configuration (**[](http://main.tf/)**[main.tf](http://main.tf/)****)**

In this code, we will set up two providers:  **AWS**  and  **Vault**. Think of them as two workers in our team—AWS builds our infrastructure, and Vault keeps our secrets safe.

Here's the complete Terraform script:


```
provider "aws" {
  region = "us-east-1"
}

provider "vault" {
  address = "<>:8200"
  skip_child_token = true

  auth_login {
    path = "auth/approle/login"
    parameters = {
      role_id = "<>"
      secret_id = "<>"
    }
  }
}

data "vault_kv_secret_v2" "example" {
  mount = "secret"  # This should match where the KV secret is stored in Vault
  name  = "test-secret"  # This matches the secret name we created
}

resource "aws_instance" "my_instance" {
  ami           = "ami-053b0d53c279acc90"  # Change the AMI ID as needed
  instance_type = "t2.micro"

  tags = {
    Name   = "test"
    Secret = data.vault_kv_secret_v2.example.data["username"]  # Fetching the secret 'username' from Vault
  }
}

```

### [](https://100daysdevops.hashnode.dev/day-84-of-100-days-vault-and-terraform-integration-continued#heading-step-by-step-explanation-of-the-terraform-code "Permalink")**Step-by-Step Explanation of the Terraform Code:**

1.  **AWS Provider**: This is where we define which AWS region our resources will be created in. In this example, we're using the  `us-east-1`  region.
    
2.  **Vault Provider**: Here, we define how we connect to Vault. This is where the magic happens! We authenticate with Vault using  **AppRole**. We have to give Vault a  **role_id**  and  **secret_id**  to allow us to fetch secrets securely. This step ensures that only trusted users can access Vault.
    
3.  **Vault KV Secret Data**: This part tells Terraform to look for the secret we created earlier (`test-secret`) in Vault. We’re specifically interested in the value of the key  `username`  inside that secret, which is  `muni`.
    
4.  **AWS EC2 Instance**: Now, we create an EC2 instance in AWS. We assign a name tag to it as "test" and dynamically set another tag called  `Secret`  with the value of the  `username`  key we fetched from Vault. Cool, right?
    

----------

### [](https://100daysdevops.hashnode.dev/day-84-of-100-days-vault-and-terraform-integration-continued#heading-step-3-run-terraform-and-apply-the-configuration "Permalink")**Step 3: Run Terraform and Apply the Configuration**

Let's get our hands dirty now. We’ll run the following Terraform commands to make everything come alive!

1.  **Initialize Terraform**: This command sets up Terraform by downloading the required providers.
    
   
    
    ```
     terraform init
    
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737047700997/d6955d69-3b1e-46b9-8057-0b40cded0c5c.png?auto=compress,format&format=webp)
    
2.  **Apply the Configuration**: This command creates all the resources we defined in the code, including the EC2 instance and fetching the secret from Vault.
    
   
    ```
     terraform apply
    
    ```
    
    After running this command, Terraform will create an EC2 instance in AWS, and the tag  `Secret`  will be set with the value  `muni`  (the secret we pulled from Vault).
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737047645188/8ebdb2b2-83b5-4235-b44c-068189dc31ad.png?auto=compress,format&format=webp)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737047668042/5170f390-d79e-4131-8341-30396aaf7e9a.png?auto=compress,format&format=webp)
    

----------

### [](https://100daysdevops.hashnode.dev/day-84-of-100-days-vault-and-terraform-integration-continued#heading-step-4-verify-the-output "Permalink")**Step 4: Verify the Output**

Once Terraform has run successfully, we can go to the  **AWS Console**  and check the newly created EC2 instance. Under the  **Tags**  section, we’ll find that the instance has a tag  `Secret`  with the value  `muni`, which is exactly what we stored in Vault!

We can verify the secret was fetched correctly, and the EC2 instance is using that secret dynamically in its configuration.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737047602237/1da38060-2590-4aef-a8b2-588c624c37ce.png?auto=compress,format&format=webp)

----------

### [](https://100daysdevops.hashnode.dev/day-84-of-100-days-vault-and-terraform-integration-continued#heading-why-are-we-doing-this-the-importance-of-secret-management "Permalink")**Why Are We Doing This? The Importance of Secret Management**

So why do we need to go through all this trouble? Well, imagine if you were to hardcode your secrets like passwords or API keys inside your Terraform files. This is risky because anyone who has access to your Terraform files can see your secrets! 😱

Vault helps us avoid this risk by  **dynamically fetching secrets**  at runtime, keeping them  **safe**  and  **secure**. When we combine Terraform with Vault, we get the best of both worlds: Infrastructure as Code (IaC) and secure secret management.

----------

### [](https://100daysdevops.hashnode.dev/day-84-of-100-days-vault-and-terraform-integration-continued#heading-conclusion "Permalink")**Conclusion**

We’ve just taken another big step in our 100-day DevOps journey! Today, we learned how to create key-value pairs in Vault, how to integrate Vault with Terraform, and how to securely fetch secrets into our AWS resources. Tomorrow, we’ll dive deeper into the next exciting concept!

**Important Note**: As this is for practical learning purposes, once we are done with this demonstration and fully understand the concept, we will delete the key-value pair we created in Vault to keep our environment clean and secure. 🔐  **Please note: Do not copy-paste your sensitive values, such as role_id or secret_id, as those can expose your environment to risks. Always use them responsibly and make sure to delete them once done!**

Let’s keep learning and growing as DevOps engineers. Stay curious, and keep experimenting! ✨
