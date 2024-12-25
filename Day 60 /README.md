# AWS Continuous Integration Demo -Part 1
#### **Objective**

Today, we’ll be setting up an AWS Continuous Integration (CI) pipeline for our Python application. This process involves creating a GitHub repository to store the source code, setting up AWS services like **CodePipeline** and **CodeBuild**, and understanding the files required for the demo.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735121631813/6005fa55-f894-490f-a95a-3e5d696e18a9.png)

----------

#### **Step 1: Set Up GitHub Repository**

To start our CI journey, we need to set up a **GitHub repository** to store the Python application’s source code. If you already have a repository, feel free to skip this step. Otherwise, follow these steps to create a new one:

1.  Sign in to your **GitHub account** at [github.com](https://github.com/).
    
2.  Click on the **"+"** button in the top-right corner and select **"New repository"**.
    
3.  Give your repository a name (e.g., `AWS_EndtoEnd_CI`) and an optional description.
    
4.  Choose the appropriate visibility (public or private).
    
5.  Initialize the repository with a **README** file.
    
6.  Click **"Create repository"**.
    

Here’s the link to my GitHub repository for this project:  
[https://github.com/MunilakshmiP/AWS_EndtoEnd_CI.git](https://github.com/MunilakshmiP/AWS_EndtoEnd_CI.git)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735121690018/0fa4f08d-5dbd-4c1a-bfd6-3cd40ca1032c.png)

----------

#### **Step 2: Key Files in the Repository**

In the repository, we have a few essential files that will help us in setting up the CI pipeline.

1.  `app.py`: This file contains the Python code for a simple Flask web application.
    
    ```python
    from flask import Flask
    
    app = Flask(__name__)
    
    @app.route('/')
    def hello():
        return 'Hello, world!'
    
    if __name__ == '__main__':
        app.run()
    ```
    
    -   This is a basic Flask app that returns "Hello, world!" when accessed via a web browser.
        
    -   It serves as the backend of our application and will be containerized and deployed using AWS services.
        
2.  `Dockerfile`: This file defines how to containerize our Flask application.
    
    ```dockerfile
    # Base image
    FROM python:3.8
    
    # Set the working directory inside the container
    WORKDIR /app
    
    # Copy the requirements file
    COPY requirements.txt .
    
    # Install the project dependencies
    RUN pip install -r requirements.txt
    
    # Copy the application code into the container
    COPY . .
    
    # Expose the port the Flask application will be listening on
    EXPOSE 5000
    
    # Run the Flask application
    CMD ["python", "app.py"]
    ```
    
    -   This Dockerfile uses the `python:3.8` base image, installs the necessary dependencies from the `requirements.txt` file, and sets up the application to run on port 5000.
        
3.  `requirements.txt`: This file lists the dependencies required by the Python application.
    
    ```http
    flask
    ```
    
    -   For this demo, we're using the `flask` package to create a simple web application.
        

----------

#### **Step 3: Setting Up AWS CodePipeline & CodeBuild**

In the next part of the demo, we will move on to setting up the AWS services like **CodePipeline** and **CodeBuild**. But for now, our main focus was setting up the GitHub repository and understanding the key files. These files will play a critical role in building, testing, and deploying our application through the CI pipeline.

Stay tuned for **Part 2**, where we’ll dive into the AWS configuration, setting up the CodePipeline and CodeBuild, and automating the deployment process!

----------

#### **Conclusion**

In this post, we created a GitHub repository to store our Python Flask application and went through the essential files (`app.py`, `Dockerfile`, and `requirements.txt`) required for setting up the CI pipeline. In **Part 2**, we’ll focus on configuring **AWS CodePipeline** and **CodeBuild** for automating the entire deployment process.

Feel free to explore the GitHub repository and follow along as we continue building the CI pipeline in the upcoming posts.

----------

### **Next Steps**

-   Part 2: Setting up AWS CodePipeline and CodeBuild for automation
    
-   Watch out for troubleshooting steps and helpful screenshots to guide you through each stage.
