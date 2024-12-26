# Practical Demo – Setting Up AWS CodeBuild for CI -Part 2

In today's blog, we're diving into the next step of our continuous integration journey by setting up  **AWS CodeBuild**. This part of the process automates the building and testing of our Python Flask application. So, let's get hands-on and walk through how to create the build environment, connect it with GitHub, and configure it to run your builds automatically.

## [](https://100daysdevops.hashnode.dev/day-61-of-100-days-practical-demo-setting-up-aws-codebuild-for-ci-part-2#heading-step-1-create-a-codebuild-project "Permalink")**Step 1: Create a CodeBuild Project**

First things first, let’s set up a new project in AWS CodeBuild. Follow these steps:

1.  **Project Name**: Choose a name that reflects the purpose of the project (e.g.,  `MyPythonAppBuild`).
    
2.  **Description**: You can provide a brief description of your project, but for this demo, we’ll keep it simple.
    
3.  **Concurrent Builds**: We won’t be enabling concurrent builds in this case. Why? Since this is a basic demo, there's no need to complicate things by allowing multiple builds to run at the same time. This keeps everything straightforward and easier to manage.
    

Now, let’s move to the next important step — connecting AWS CodeBuild with GitHub.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735121875549/40401a7e-a3ae-40cc-a709-87762cc1a277.png?auto=compress,format&format=webp)

----------

## [](https://100daysdevops.hashnode.dev/day-61-of-100-days-practical-demo-setting-up-aws-codebuild-for-ci-part-2#heading-step-2-connect-aws-codebuild-to-github "Permalink")**Step 2: Connect AWS CodeBuild to GitHub**

To integrate CodeBuild with GitHub, we'll use OAuth authentication, which simply asks you to log in with your GitHub credentials.

Here's what you need to do:

-   **GitHub Authentication**: You'll be prompted to enter your GitHub username and password to authorize AWS CodeBuild to access your repository. This allows CodeBuild to fetch the latest code whenever there’s a change in your repository.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735121912692/8a8aaa94-c7fb-4de3-a076-5e3609ccbae2.png?auto=compress,format&format=webp)
    

Once connected, it’s time to configure the  **environment**.

----------

## [](https://100daysdevops.hashnode.dev/day-61-of-100-days-practical-demo-setting-up-aws-codebuild-for-ci-part-2#heading-step-3-set-up-the-environment-in-codebuild "Permalink")**Step 3: Set Up the Environment in CodeBuild**

In the  **Environment**  section of AWS CodeBuild, we define the build environment and specify the Docker image that will run our application. This is where the real magic happens — CodeBuild will use this environment to execute the steps defined in the  `buildspec.yml`  file.

Let’s break this down:

1.  **Docker Image**: This image contains the software tools needed to build our application. AWS CodeBuild uses it to perform all the build and testing steps. Think of it as the container that holds everything your app needs to be built and tested.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735121984886/8354d7f7-6987-42f8-a517-5404925c4ffe.png?auto=compress,format&format=webp)
    
2.  **Buildspec File**: To automate our builds, we need to create a  `buildspec.yml`  file. This YAML file will contain all the commands AWS CodeBuild needs to run during each phase of the build process (like installing dependencies, running tests, and deploying the application).
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735122033063/cfb246ea-4b79-4dd1-b856-8d65fe621164.png?auto=compress,format&format=webp)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735122060360/2af18dff-2538-46b0-b49b-d7bab5abc0b0.png?auto=compress,format&format=webp)
    

----------

## [](https://100daysdevops.hashnode.dev/day-61-of-100-days-practical-demo-setting-up-aws-codebuild-for-ci-part-2#heading-step-4-understanding-the-buildspecyml-file "Permalink")**Step 4: Understanding the buildspec.yml File**

Now, let’s talk about the  `buildspec.yml`  file. This is where we define all the steps to build and deploy our application. I'll explain what each section does and how it helps automate the entire CI process.

### [](https://100daysdevops.hashnode.dev/day-61-of-100-days-practical-demo-setting-up-aws-codebuild-for-ci-part-2#heading-version "Permalink")**Version**

The  `version: 0.2`  line tells CodeBuild that we're using the latest version of the build specification format.

### [](https://100daysdevops.hashnode.dev/day-61-of-100-days-practical-demo-setting-up-aws-codebuild-for-ci-part-2#heading-env-environment-variables "Permalink")**Env (Environment Variables)**

In the  `env`  section, we're setting environment variables that are stored in AWS Systems Manager  **Parameter Store**. These credentials are securely managed, so no sensitive data is hardcoded in the buildspec file.

For example:

-   `DOCKER_REGISTRY_USERNAME`: The username for logging into the Docker registry.
    
-   `DOCKER_REGISTRY_PASSWORD`: The password for the Docker registry.
    
-   `DOCKER_REGISTRY_URL`: The URL where the Docker image will be stored.
    

**Fun fact:**  These values will be fetched at runtime, which makes our builds more secure by keeping secrets out of the code.

### [](https://100daysdevops.hashnode.dev/day-61-of-100-days-practical-demo-setting-up-aws-codebuild-for-ci-part-2#heading-phases "Permalink")**Phases**

The  `phases`  section breaks down the build process into different stages. Here's what each part does:

-   **Install**: In this phase, we define the runtime environment. For this project, we’re using  **Python 3.11**.
    
-   **Pre-Build**: Before the actual build, we install the dependencies. The command  `pip install -r simple-python-app/requirements.txt`  installs all the libraries needed for the Flask app.
    
-   **Build**: This is where the real action happens! We:
    
    1.  Log in to the Docker registry using the credentials we set earlier.
        
    2.  Build the Docker image for our Python Flask app.
        
    3.  Push the Docker image to the registry.
        
-   **Post-Build**: Once everything is built, we print a success message to confirm that the build process completed without any issues.
    

### [](https://100daysdevops.hashnode.dev/day-61-of-100-days-practical-demo-setting-up-aws-codebuild-for-ci-part-2#heading-artifacts "Permalink")**Artifacts**

After the build completes, we specify which files should be included as build artifacts. In this case, we're including all files from the  `simple-python-app`  directory.

In the next blog, we’ll dive into the details of  **AWS Parameter Store**  and how to securely manage the environment variables used in the build process. Stay tuned!

**Review and Create**

-   After reviewing the settings, click on  **"Create build project"**  to create your project.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735122463170/f49d755d-0d6c-41e0-8bdf-f34675da7673.png?auto=compress,format&format=webp)
    

**Conclusion**

In this post, we covered the steps to set up an AWS CodeBuild project for Continuous Integration:

1.  **GitHub Repository Setup**: We connected our GitHub repo to AWS CodePipeline to track code changes.
    
2.  **Build Project Creation**: We created and configured the CodeBuild project with the necessary environment and settings.
    
3.  **buildspec.yml File**: We explained the key sections of the buildspec file, including  `install`,  `pre_build`,  `build`, and  `post_build`, along with the use of parameter-store for storing credentials.
    

This setup automates the CI process for your Python app. Stay tuned for the next part, where we’ll explore how CodePipeline integrates with CodeBuild.
