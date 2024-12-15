# Securing Sensitive Data and Hosting Static Websites with Amazon S3
Today, we’ll explore two critical use cases for Amazon S3: restricting access to sensitive data using bucket policies and hosting a static website. This hands-on guide will demonstrate how to implement these concepts step-by-step.

----------

### [](https://100daysdevops.hashnode.dev/day-46-of-100-days-securing-sensitive-data-and-hosting-static-websites-with-amazon-s3#heading-scenario-1-restricting-access-to-sensitive-data "Permalink")**Scenario 1: Restricting Access to Sensitive Data**

As a DevOps Engineer, you might need to store sensitive information in an S3 bucket and ensure that even users with broader S3 access can't access this specific bucket. Here's how to secure your bucket:

#### [](https://100daysdevops.hashnode.dev/day-46-of-100-days-securing-sensitive-data-and-hosting-static-websites-with-amazon-s3#heading-step-1-create-an-iam-user "Permalink")**Step 1: Create an IAM User**

1.  Navigate to the IAM Console.
    
2.  Create a user named  `demo-s3-bucket-user`.
    
    -   Assign console access with a custom password.
3.  Do not attach any permissions initially to demonstrate default behavior.
    

#### [](https://100daysdevops.hashnode.dev/day-46-of-100-days-securing-sensitive-data-and-hosting-static-websites-with-amazon-s3#heading-step-2-test-default-access "Permalink")**Step 2: Test Default Access**

1.  Open an incognito window and log in with the new IAM user credentials.
    
2.  Navigate to S3 in the AWS Console.
    
3.  Notice that the user cannot list or access any S3 buckets (expected behavior).
    

#### [](https://100daysdevops.hashnode.dev/day-46-of-100-days-securing-sensitive-data-and-hosting-static-websites-with-amazon-s3#heading-step-3-grant-s3-permissions "Permalink")**Step 3: Grant S3 Permissions**

1.  In the IAM Console, attach the  `AmazonS3FullAccess`  policy to the IAM user.
    
2.  Refresh the S3 Console for the IAM user.
    
3.  The user can now list all buckets and access files within them.
    

#### [](https://100daysdevops.hashnode.dev/day-46-of-100-days-securing-sensitive-data-and-hosting-static-websites-with-amazon-s3#heading-step-4-restrict-access-with-bucket-policies "Permalink")**Step 4: Restrict Access with Bucket Policies**

1.  Go to the S3 Console and select your bucket.
    
2.  Navigate to the  **Bucket Permissions**  tab and locate the  **Bucket Policy**  section.
    
3.  Click  **Edit**  and use the AWS Policy Generator to create a policy. Here's an example:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733068707609/cd1bdfb0-31e6-4782-b5ab-fbebd625c881.png?auto=compress,format&format=webp)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733068752713/3077a525-0e4f-4eb0-8d77-7ed8db1c9626.png?auto=compress,format&format=webp)
    
4.  Save the policy.
    

#### [](https://100daysdevops.hashnode.dev/day-46-of-100-days-securing-sensitive-data-and-hosting-static-websites-with-amazon-s3#heading-step-5-verify-restrictions "Permalink")**Step 5: Verify Restrictions**

1.  Switch back to the IAM user.
    
2.  Attempt to access the bucket or download files.
    
3.  The user will now see an "Insufficient Permissions" error, even though they have S3 full access.
    

----------

### [](https://100daysdevops.hashnode.dev/day-46-of-100-days-securing-sensitive-data-and-hosting-static-websites-with-amazon-s3#heading-scenario-2-hosting-a-static-website-on-s3 "Permalink")**Scenario 2: Hosting a Static Website on S3**

S3 provides a cost-effective way to host static websites.

#### [](https://100daysdevops.hashnode.dev/day-46-of-100-days-securing-sensitive-data-and-hosting-static-websites-with-amazon-s3#heading-step-1-prepare-your-website-files "Permalink")**Step 1: Prepare Your Website Files**

1.  Create or download a simple  `This_is_Munilakshmi.html`  file. (You can use  [W3Schools](https://www.w3schools.com/html/html_intro.asp)  for sample templates.)

#### [](https://100daysdevops.hashnode.dev/day-46-of-100-days-securing-sensitive-data-and-hosting-static-websites-with-amazon-s3#heading-step-2-upload-files-to-s3 "Permalink")**Step 2: Upload Files to S3**

1.  Create a new S3 bucket.
    
2.  Upload the  `This_is_Munilakshmi.html`  file to the bucket.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733069690928/f44ab50c-571f-4465-b287-3c0a3c7d4830.png?auto=compress,format&format=webp)
    

#### [](https://100daysdevops.hashnode.dev/day-46-of-100-days-securing-sensitive-data-and-hosting-static-websites-with-amazon-s3#heading-step-3-enable-static-website-hosting "Permalink")**Step 3: Enable Static Website Hosting**

1.  Go to the  **Properties**  tab of the bucket.
    
2.  Scroll to  **Static Website Hosting**  and enable it.
    
3.  Specify  `This_is_Munilakshmi.html`  as the  **Index Document**.
    
4.  Save changes.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733069632004/f0cd2441-b631-4674-8f7a-fe8e7438c8ef.png?auto=compress,format&format=webp)
    

#### [](https://100daysdevops.hashnode.dev/day-46-of-100-days-securing-sensitive-data-and-hosting-static-websites-with-amazon-s3#heading-step-4-set-permissions-for-public-access "Permalink")Step 4 : Set Permissions for Public Access

1.  **Allow public access to the files**:
    
    -   Go to the  **Permissions**  tab of your S3 bucket.
        
    -   Under  **Block public access (bucket settings)**, click  **Edit**.
        
    -   Uncheck  **Block all public access**  to allow anyone to access your website files.
        
    -   Confirm the changes by clicking  **Save**.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733069885363/a38c21f8-ce72-4ba4-8507-8953873b294f.png?auto=compress,format&format=webp)
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733069912063/597a8a14-52ed-4618-b4a9-e08f4e1a6e60.png?auto=compress,format&format=webp)
        

2.  **Configure bucket policy to allow public access**:
    
    -   In the  **Permissions**  tab, click on  **Bucket Policy**.
        
    -   Paste the following JSON policy to allow public read access to all objects in the bucket:
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733069943264/74b32a85-1227-4874-9e22-4c88104e4a7a.png?auto=compress,format&format=webp)
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733070094793/f0c17c5c-5357-42bd-b448-bc5eb59ccf34.png?auto=compress,format&format=webp)
        
    -   Click  **Save changes**  to apply the policy.
        

**Step 5: Access the Website**

1.  Copy the  **Bucket Endpoint**  provided in the Static Website Hosting section.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733070251710/479a5415-0a8a-4ed1-a601-f9f3dfae14da.png?auto=compress,format&format=webp)
    
2.  Open the URL in a browser to see your static website live.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733070279485/9eceba8c-5715-45fa-b4d9-8c8398a4caa9.png?auto=compress,format&format=webp)
    

----------

### [](https://100daysdevops.hashnode.dev/day-46-of-100-days-securing-sensitive-data-and-hosting-static-websites-with-amazon-s3#heading-hands-on-exercise "Permalink")**Hands-On Exercise**

1.  **Secure Your Bucket:**  Use the provided JSON policy to block access to your bucket for all users except yourself. Test it with multiple IAM users.
    
2.  **Host a Website:**  Create a simple static website using HTML, upload it to S3, and enable hosting.
    

----------

### [](https://100daysdevops.hashnode.dev/day-46-of-100-days-securing-sensitive-data-and-hosting-static-websites-with-amazon-s3#heading-key-learnings "Permalink")**Key Learnings**

-   **Bucket Policies**  are essential for controlling access to sensitive data.
    
-   Hosting static websites on S3 is a cost-effective solution for simple web applications.
    

**Conclusion**  
We’ve explored how to effectively host static websites using Amazon S3. By understanding bucket policies, configuring static hosting, and testing deployment, you now have the foundational knowledge to host your own static websites on AWS. With the scalable and cost-effective features of S3, you can ensure reliable website delivery to users worldwide.

Keep experimenting, keep building, and let your curiosity guide you toward mastering AWS. Happy learning! 🚀

----------
