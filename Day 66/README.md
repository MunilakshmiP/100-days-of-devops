# # Host Your Static Website on AWS S3 and CloudFront

### Introduction

Hello, DevOps enthusiasts! 🚀 Welcome to another insightful day of learning. Today, I’ll walk you through hosting a static website using  **AWS S3**  and  **CloudFront**. If you’re looking for a secure, scalable, and cost-effective solution for your portfolio, blog, or documentation site, this guide has you covered. Let’s dive in!

----------

### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-why-host-static-websites-on-aws "Permalink")Why Host Static Websites on AWS?

1.  **Scalability**: Handle high traffic without breaking a sweat.
    
2.  **Security**: Keep your bucket private while serving files securely.
    
3.  **Performance**: Use CloudFront’s edge locations for lightning-fast delivery.
    
4.  **Cost-Effectiveness**: Pay only for what you use—perfect for small projects.
    

----------

### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-step-by-step-guide-to-hosting "Permalink")Step-by-Step Guide to Hosting

#### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-1-create-and-configure-an-s3-bucket "Permalink")1. Create and Configure an S3 Bucket

AWS S3 is your storage solution for static files.

-   Log in to the  **AWS Management Console**  and navigate to S3.
    
-   Click on  **Create Bucket**  and give it a unique name like  `my-static-site-bucket`.
    
-   Once created, go to the  **Properties**  tab and enable  **Static Website Hosting**:
    
    -   Set your  **index document**  (e.g.,  `index.html`) and optionally, an error document (e.g.,  `404.html`).
        
    -   Save the configuration.
        

#### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-2-upload-website-files "Permalink")2. Upload Website Files

Now, it’s time to add your static website files:

-   Drag and drop your  `index.html`, CSS, JS, and other files into the S3 bucket.
    
-   Keep public access disabled for now (we’ll use CloudFront for secure access).
    

#### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-3-test-your-bucket-url "Permalink")3. Test Your Bucket URL

-   Locate the bucket URL in the  **Properties**  section.
    
-   Open the URL in your browser. If you see a  **403 Forbidden error**, don’t worry—it means the bucket is private as expected.
    

----------

### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-configure-cloudfront-for-global-distribution "Permalink")Configure CloudFront for Global Distribution

#### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-4-create-a-cloudfront-distribution "Permalink")4. Create a CloudFront Distribution

AWS CloudFront acts as a CDN (Content Delivery Network) to serve your website globally.

-   Go to the  **CloudFront**  service in the AWS Console.
    
-   Click  **Create Distribution**  and choose:
    
    -   **Origin Domain Name**: Select your S3 bucket.
        
    -   **Enable Origin Access Identity (OAI)**: This allows CloudFront to access the bucket securely.
        
    -   Update the bucket policy to grant OAI permissions.
        

#### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-5-optimize-cloudfront-settings "Permalink")5. Optimize CloudFront Settings

-   **Redirect HTTP to HTTPS**  for secure connections.
    
-   Set the  **Default Root Object**  as  `index.html`.
    
-   Optionally, configure caching and regional restrictions for better performance.
    

#### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-6-deploy-the-distribution "Permalink")6. Deploy the Distribution

-   Save your changes and deploy the distribution. It may take a few minutes to propagate.
    
-   Once deployed, you’ll get a CloudFront domain name (e.g.,  [`example123.cloudfront.net`](http://example123.cloudfront.net/)).
    

----------

### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-verify-your-setup "Permalink")Verify Your Setup

-   Access your CloudFront domain name in a browser to check your website.
    
-   Ensure the S3 bucket is private—accessible only through CloudFront.
    

----------

### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-tips-for-enhancing-your-website "Permalink")Tips for Enhancing Your Website

#### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-security-best-practices "Permalink")Security Best Practices

-   Always use HTTPS for secure communication.
    
-   Keep public access to the S3 bucket disabled.
    

#### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-cost-management "Permalink")Cost Management

-   Monitor your usage to avoid unexpected charges.
    
-   Utilize CloudFront caching to reduce data transfer costs.
    

#### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-advanced-enhancements "Permalink")Advanced Enhancements

-   Link a custom domain via  **Route 53**.
    
-   Add an SSL certificate for custom domain HTTPS.
    
-   Enable logging and monitoring for insights into traffic and performance.
    

----------

### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-real-life-example "Permalink")Real-Life Example

Imagine hosting your portfolio site:

-   Files are securely stored in an S3 bucket.
    
-   CloudFront serves the site globally, ensuring faster load times.
    
-   HTTPS ensures secure access for your audience.
    

With just a few steps, your website is live, fast, and secure!

----------

### [](https://100daysdevops.hashnode.dev/day-66-of-100-days-host-your-static-website-on-aws-s3-and-cloudfront#heading-wrapping-up "Permalink")Wrapping Up

AWS S3 and CloudFront make hosting a static website straightforward, secure, and scalable. Whether for personal projects or professional use, this setup ensures performance and reliability with minimal effort.

Got questions? Drop them in the comments below! See you next time with more exciting DevOps insights. 🌟
