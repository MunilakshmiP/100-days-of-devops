## Setting Up AWS Config Compliance Rules and Lambda for Security
**Overview of AWS Config Compliance**  
AWS Config is a powerful service that helps you assess, audit, and evaluate the configurations of your AWS resources. With Config, you can monitor and manage your AWS resource configurations to ensure compliance with internal policies, industry standards, and security best practices. By using  **AWS Config Rules**, you can evaluate your AWS resource configurations for compliance automatically.

**Importance of Compliance in Security**  
Compliance in cloud security is crucial for ensuring that your resources and infrastructure are configured in a manner that meets both security and operational best practices. Non-compliance with certain policies can lead to data breaches, security vulnerabilities, and non-adherence to regulatory requirements. AWS Config allows you to continuously monitor your resource configurations and track changes to maintain a secure and compliant environment.

### [](https://100daysdevops.hashnode.dev/day-67-of-100-days-setting-up-aws-config-compliance-rules-and-lambda-for-security#heading-step-by-step-process-for-setting-up-aws-config-rules "Permalink")Step-by-Step Process for Setting Up AWS Config Rules

#### [](https://100daysdevops.hashnode.dev/day-67-of-100-days-setting-up-aws-config-compliance-rules-and-lambda-for-security#heading-1-set-up-aws-config "Permalink")1.  **Set Up AWS Config**

-   Navigate to the  **AWS Config Console**.
    
-   Select  **“Set up AWS Config”**  to begin the configuration process.
    
-   Choose the resources you want to track (e.g., EC2, S3, IAM) and the regions to monitor.
    
-   Enable  **SNS**  notifications for alerts on configuration changes.
    

#### [](https://100daysdevops.hashnode.dev/day-67-of-100-days-setting-up-aws-config-compliance-rules-and-lambda-for-security#heading-2-create-aws-config-rules "Permalink")2.  **Create AWS Config Rules**

-   Go to  **AWS Config**  and select  **Rules**  from the left-hand menu.
    
-   Choose  **Add Rule**  and either create a custom rule or use a predefined managed rule from AWS Config.
    
-   Select the rule that fits your compliance needs, such as  `s3-bucket-logging-enabled`  to ensure logging is enabled on your S3 buckets or  `ec2-instance-no-public-ip`  for EC2 instances to not have public IP addresses.
    
-   Review and confirm the settings to create the rule.
    

#### [](https://100daysdevops.hashnode.dev/day-67-of-100-days-setting-up-aws-config-compliance-rules-and-lambda-for-security#heading-3-configuring-remediation-for-non-compliant-resources "Permalink")3.  **Configuring Remediation for Non-Compliant Resources**

-   For each rule, you can choose an automated remediation action that will execute when a resource is found to be non-compliant.
    
-   AWS Config can trigger a  **Lambda function**  or use other services to bring the resource back into compliance.
    

### [](https://100daysdevops.hashnode.dev/day-67-of-100-days-setting-up-aws-config-compliance-rules-and-lambda-for-security#heading-creating-and-configuring-a-lambda-function-for-compliance "Permalink")Creating and Configuring a Lambda Function for Compliance

To handle non-compliant resources, you can set up a  **Lambda function**  that will be triggered by AWS Config to automatically remediate any violations. This could include actions such as disabling public IP addresses or enabling encryption on S3 buckets.

#### [](https://100daysdevops.hashnode.dev/day-67-of-100-days-setting-up-aws-config-compliance-rules-and-lambda-for-security#heading-1-create-lambda-function "Permalink")1.  **Create Lambda Function**

-   Go to  **AWS Lambda Console**.
    
-   Select  **Create function**  and choose  **Author from Scratch**.
    
-   Define the function name (e.g.,  `RemediateEC2PublicIP`) and choose a runtime (e.g., Python 3.x).
    
-   In the  **Function Code**, write the logic to handle the compliance task (e.g., stopping EC2 instances with public IPs).
    

Example code snippet for an EC2 instance compliance check:


```
import boto3

ec2 = boto3.client('ec2')

def lambda_handler(event, context):
    instance_id = event['detail']['resourceId']
    response = ec2.describe_instances(InstanceIds=[instance_id])
    public_ip = response['Reservations'][0]['Instances'][0].get('PublicIpAddress')

    if public_ip:
        ec2.modify_instance_attribute(InstanceId=instance_id, NoPublicIp=True)
        return f"Public IP removed from instance {instance_id}"
    else:
        return f"Instance {instance_id} is already compliant"

```

#### [](https://100daysdevops.hashnode.dev/day-67-of-100-days-setting-up-aws-config-compliance-rules-and-lambda-for-security#heading-2-set-permissions-for-lambda "Permalink")2.  **Set Permissions for Lambda**

Ensure that the Lambda function has the necessary  **IAM roles**  and  **permissions**  to manage resources. Assign a role that includes permissions like:

-   `ec2:DescribeInstances`
    
-   `ec2:ModifyInstanceAttribute`
    
-   `logs:CreateLogGroup`,  `logs:CreateLogStream`,  `logs:PutLogEvents`  (for logging)
    

### [](https://100daysdevops.hashnode.dev/day-67-of-100-days-setting-up-aws-config-compliance-rules-and-lambda-for-security#heading-permissions-and-iam-roles-required "Permalink")Permissions and IAM Roles Required

AWS Config will need permissions to access your resources and trigger Lambda functions. The Lambda function itself must also have permissions to remediate compliance issues (e.g., stopping instances, modifying security settings).

-   **IAM Role for AWS Config**:
    
    -   Create a custom IAM role with the necessary permissions to invoke Lambda functions.
        
    -   Attach the  `AWSConfigRole`  policy to allow AWS Config to execute the remediation.
        
-   **IAM Role for Lambda**:
    
    -   Create a separate IAM role with the permissions needed for the Lambda function (e.g., EC2 and S3 permissions).
        
    -   Make sure this role is attached to the Lambda function when setting it up.
        

### [](https://100daysdevops.hashnode.dev/day-67-of-100-days-setting-up-aws-config-compliance-rules-and-lambda-for-security#heading-explaining-code-and-debugging-tips "Permalink")Explaining Code and Debugging Tips

When creating Lambda functions to remediate non-compliant resources, debugging is essential to ensure that your code works as expected. Here are some tips:

-   **Use CloudWatch Logs**:
    
    -   Always enable logging for your Lambda function to capture output, errors, and trace logs. This helps you identify issues quickly.
-   **Test Functions with Sample Events**:
    
    -   Use the  **Test**  feature in Lambda to simulate events from AWS Config. This will help you debug before deploying the function live.
-   **Handle Errors Gracefully**:
    
    -   Always include error handling in your Lambda function, such as try-except blocks, to ensure that issues are logged and the system continues to function even if one resource cannot be remediated.

### [](https://100daysdevops.hashnode.dev/day-67-of-100-days-setting-up-aws-config-compliance-rules-and-lambda-for-security#heading-conclusion "Permalink")Conclusion

AWS Config compliance rules, when integrated with Lambda functions, create a powerful tool for maintaining a secure and compliant AWS environment. By automating the process of monitoring resource configurations and correcting violations, you ensure that your infrastructure adheres to security and operational best practices.

**Tip for DevOps Professionals**: Continuously monitor your AWS Config rules and Lambda function performance to ensure they meet evolving compliance requirements. Regularly update your compliance rules as new best practices and security standards are released.
