# Parameter Store, Build Process, and CodePipeline Integration-Part 3
Hello, everyone! 🌟

Welcome back to another exciting part of our Continuous Integration journey! I’m super excited to dive into this next phase where we’ll be setting up our Docker credentials securely in AWS, kicking off the build process for our Python application, and integrating everything with AWS CodePipeline. It’s going to be an awesome learning experience—let’s get started!

----------

#### **1. Storing Docker Credentials in Parameter Store: Keeping It Secure! 🔐**

Security is key, right? We want to keep our credentials safe and sound! And that’s exactly what we’re going to do with **AWS Systems Manager Parameter Store**. This handy tool helps us store Docker credentials securely, so we don’t have to worry about exposing them in our code.

Here’s how easy it is to store your credentials securely:

1.  **Hop over to Parameter Store**: In your AWS Management Console, just search for "Systems Manager," and click on **Parameter Store**.
    
2.  **Create Your Parameters**:
    
    -   **Username**: Click **Create parameter**, name it `/myapp/docker-credentials/username`, select **SecureString**, and enter your Docker username.
        
    -   **Password**: Same steps for the password—create a parameter called `/myapp/docker-credentials/password` and enter your Docker password.
        
    -   **Registry URL**: And lastly, create a parameter for the Docker registry URL, such as `/myapp/docker-credentials/url`, and set the URL of your Docker registry.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735129236450/f269ae0b-5a44-415f-ac65-87365a7010d3.png)

Now, your sensitive credentials are locked up tight and ready for use when the build process kicks in!

----------

#### **2. Let’s Get the Build Process Rolling! 🚀**

Okay, this is where the magic happens! 🪄 Once your credentials are securely stored, we can trigger the build process. The excitement I felt when my **8th build** finally succeeded was unbelievable. The key takeaway here is: **Every failure is a lesson, and every lesson brings you closer to success**. 💡

Here’s how the build process goes:

-   **Pulling the latest changes** from your GitHub repository.
    
-   **Setting up the environment** (like installing dependencies).
    
-   **Building the Docker image**.
    
-   **Pushing the image to Docker Hub**, where it’s ready to be deployed anywhere!
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735129292038/11da6902-9586-4881-8ee1-23e4688a918f.png)![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735129314415/f3e65102-c9fb-4ed5-b1da-fdb8b82f73be.png)

It took me a few tries, but now, every build is a huge win. And let me tell you—seeing that green checkmark of success is _always_ worth it! 🎉

----------

#### **3. Docker Hub: Your Application’s New Home 🏠**

Once the build is successful, it’s time to show off your application by hosting it on **Docker Hub**! 🚀 Docker Hub is like the public showcase for your Docker images, and once the app is uploaded, it’s ready to be pulled and deployed anywhere in the world. 🌍

Here’s how my application looks on Docker Hub! It’s so cool to see everything come together. 🖼️

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735129355577/c1ee3e9f-f4b5-4a01-b1e1-f49a55f191a6.png)

----------

#### **4. Time to Automate with CodePipeline! ⚡**

Here’s where we add a little bit of automation magic ✨ with **AWS CodePipeline**. This tool connects everything, so every time you push changes to GitHub, the build happens automatically. Talk about **efficiency**! 🙌

Let’s break it down:

1.  **Create a Pipeline**: Head over to **AWS CodePipeline** and click **Create pipeline**.
    
    -   Give your pipeline a name
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735129424749/e0966ed6-d0af-4acb-8d8c-4a174dc7e210.png)
2.  **Source Stage**:
    
    -   Select **GitHub** as your source provider and connect your GitHub account via OAuth.
        
    -   Choose the repository and branch you want to monitor. From now on, every change you make in GitHub will trigger this pipeline. **How cool is that?!**
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735129454175/dff93d21-fec1-411b-bf44-f1fd951dacb5.png)
3.  **Build Stage**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735129528140/2aba297d-6c72-4d4d-9bb7-a789e686b369.png)
4.  **Skip Deployment Stage**:
    
    -   For now, we’re focusing on the CI pipeline, so no need for the deployment stage just yet. We’ll leave that for a later blog!
        
5.  **Hit Create Pipeline**: Click **Create**, and **Boom!** AWS automatically creates the pipeline and triggers everything in the background!
    

----------

#### **5. Watch It All Come Together: Build, Automate, and Celebrate! 🎉**

Now the real fun begins! Every time a change is pushed to GitHub, **AWS CodePipeline** automatically triggers the build process through **AWS CodeBuild**. The result? A smooth, seamless, automated workflow that gets us one step closer to our deployment. No manual intervention required!

Here’s a screenshot of the build triggered after I pushed a change. The feeling of automation at work is priceless!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735129584413/98cf9a1c-bd6d-47af-a2f5-3e832c0fc38c.png)![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735129606931/61a36fa0-d7bd-4f1a-8d07-338f705c586d.png)

----------

#### **Overall Recap: Celebrate Your Progress! 🎉**

Let’s take a moment to appreciate all the hard work we’ve done so far. Today, we’ve successfully set up a CI pipeline that automates the build process of our Python Flask application. Here’s what we accomplished:

1.  **Security First**: We stored our Docker credentials securely in **AWS Parameter Store** so we can access them without exposing them in the code. ✅
    
2.  **Build Process**: We’ve set up a smooth build process using **AWS CodeBuild**, where we pull changes, install dependencies, build the Docker image, and push it to Docker Hub. ✅
    
3.  **Automated with CodePipeline**: We integrated everything with **AWS CodePipeline**, making the entire process automatic. Now, every time you push to GitHub, CodePipeline will handle the rest. **How awesome is that?** 🙌
    

I hope you’re as pumped as I am about the progress we’ve made. Automation is such a game changer, and now you have a fully automated CI pipeline in place!

Stay tuned for the next part of our journey, where we’ll take things even further. **The best is yet to come!**
