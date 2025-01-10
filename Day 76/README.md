# Terraform-ing AWS: Crafting CloudWatch, S3, and IAM Like a Pro!
Hey everyone! 🌟 Today’s post is all about automating some core infrastructure components on AWS using Terraform. We’ll walk through creating an S3 bucket for storage, managing IAM users for access control, and setting up CloudWatch for monitoring and logging. Ready to dive in? Let’s go! 😎

----------

### [](https://100daysdevops.hashnode.dev/day-76-of-100-days-terraform-ing-aws-crafting-cloudwatch-s3-and-iam-like-a-pro#heading-1-s3-bucket-object-storage "Permalink")**1. S3 Bucket (Object Storage)**

#### [](https://100daysdevops.hashnode.dev/day-76-of-100-days-terraform-ing-aws-crafting-cloudwatch-s3-and-iam-like-a-pro#heading-terraform-code "Permalink")**Terraform Code:**

```
provider "aws" {
  region = "ap-south-1"
}

# Create an S3 Bucket
resource "aws_s3_bucket" "example_bucket" {
  bucket = "my-example-terraform-bucket"  # Replace with a unique bucket name
  acl    = "private"

  tags = {
    Name = "ExampleS3Bucket"
  }
}

```

#### [](https://100daysdevops.hashnode.dev/day-76-of-100-days-terraform-ing-aws-crafting-cloudwatch-s3-and-iam-like-a-pro#heading-explanation "Permalink")**Explanation:**

-   `provider "aws" { region = "ap-south-1" }`: This tells Terraform that we want to use AWS resources in the Mumbai (ap-south-1) region.
    
-   `resource "aws_s3_bucket" "example_bucket" {...}`: This block is where we create an S3 bucket. It’s like creating a storage container in the cloud.
    
    -   `bucket = "my-example-terraform-bucket"`: This is the name of the S3 bucket. Make sure it’s unique across all AWS accounts.
        
    -   `acl = "private"`: This ensures that only the owner of the bucket can access it.
        
    -   `tags = { Name = "ExampleS3Bucket" }`: This is like adding a label to the bucket to help identify it.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736441464940/a4e6c8e0-5c36-4589-b63a-13dd0e2768b3.png?auto=compress,format&format=webp)
        

----------

### [](https://100daysdevops.hashnode.dev/day-76-of-100-days-terraform-ing-aws-crafting-cloudwatch-s3-and-iam-like-a-pro#heading-2-iam-user-with-access-keys-identity-and-access-management "Permalink")**2. IAM User with Access Keys (Identity and Access Management)**

#### [](https://100daysdevops.hashnode.dev/day-76-of-100-days-terraform-ing-aws-crafting-cloudwatch-s3-and-iam-like-a-pro#heading-terraform-code-1 "Permalink")**Terraform Code:**


```
provider "aws" {
  region = "ap-south-1"
}

# Create an IAM User
resource "aws_iam_user" "example_user" {
  name = "example-terraform-user"
}

# Create Access Key for IAM User
resource "aws_iam_access_key" "example_access_key" {
  user = aws_iam_user.example_user.name
}

# Attach Policy to IAM User (e.g., full S3 access)
resource "aws_iam_user_policy_attachment" "example_policy" {
  user       = aws_iam_user.example_user.name
  policy_arn = "arn:aws:iam::aws:policy/AmazonS3FullAccess"
}

```

#### [](https://100daysdevops.hashnode.dev/day-76-of-100-days-terraform-ing-aws-crafting-cloudwatch-s3-and-iam-like-a-pro#heading-explanation-1 "Permalink")**Explanation:**

-   `resource "aws_iam_user" "example_user" {...}`: Creates a new user in AWS. This user can be given permissions to access AWS resources.
    
-   `resource "aws_iam_access_key" "example_access_key" {...}`: Creates an  **access key**  for the user, which is used to authenticate and interact with AWS programmatically.
    
-   `resource "aws_iam_user_policy_attachment" "example_policy" {...}`: This gives the user access to specific AWS services—in this case, full access to S3, so the user can upload, download, and manage files in S3.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736441624341/6bee5b0b-d513-413c-92f3-d1cbc3442089.png?auto=compress,format&format=webp)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736441677493/70ce4946-d857-4982-8aca-6eda9d32d2c4.png?auto=compress,format&format=webp)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736441710243/25fe6e4b-04a0-49b8-b4de-17675ae36725.png?auto=compress,format&format=webp)
    

----------

### [](https://100daysdevops.hashnode.dev/day-76-of-100-days-terraform-ing-aws-crafting-cloudwatch-s3-and-iam-like-a-pro#heading-3-cloudwatch-log-group-monitoring-and-logging "Permalink")**3. CloudWatch Log Group (Monitoring and Logging)**

#### [](https://100daysdevops.hashnode.dev/day-76-of-100-days-terraform-ing-aws-crafting-cloudwatch-s3-and-iam-like-a-pro#heading-terraform-code-2 "Permalink")**Terraform Code:**


```
provider "aws" {
  region = "ap-south-1"
}

# Create a CloudWatch Log Group
resource "aws_cloudwatch_log_group" "example_log_group" {
  name = "example-terraform-log-group"

  retention_in_days = 30  # Optional: Retain logs for 30 days
}

# Create a CloudWatch Log Stream
resource "aws_cloudwatch_log_stream" "example_log_stream" {
  log_group_name = aws_cloudwatch_log_group.example_log_group.name
  name           = "example-terraform-log-stream"
}

```

#### [](https://100daysdevops.hashnode.dev/day-76-of-100-days-terraform-ing-aws-crafting-cloudwatch-s3-and-iam-like-a-pro#heading-explanation-2 "Permalink")**Explanation:**

-   `resource "aws_cloudwatch_log_group" "example_log_group" {...}`: This creates a  **log group**  in CloudWatch, which is a place to store logs from your resources, like EC2 instances.
    
    -   `retention_in_days = 30`: This tells CloudWatch to keep the logs for 30 days.
-   `resource "aws_cloudwatch_log_stream" "example_log_stream" {...}`: A  **log stream**  is where the logs are stored within a log group. Think of it as a specific source of logs, like logs from a specific server or service.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736441844025/cd72472f-6f19-4d82-a20e-59cb2e16ca17.png?auto=compress,format&format=webp)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1736441914756/d6508469-0656-4362-8970-89706eeb9903.png?auto=compress,format&format=webp)
    

----------

### [](https://100daysdevops.hashnode.dev/day-76-of-100-days-terraform-ing-aws-crafting-cloudwatch-s3-and-iam-like-a-pro#heading-conclusion "Permalink")**Conclusion:**

Today we automated some key AWS resources with Terraform! From setting up an S3 bucket for file storage to managing user permissions with IAM and keeping track of logs with CloudWatch, we’ve built out some of the essential components for a scalable, secure infrastructure.

That’s it for today! Hope this gives you a clearer understanding of how to use Terraform for AWS. Let me know if you have any questions or if you’re ready to dive deeper into Terraform’s capabilities. Happy building! 🚀
