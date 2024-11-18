
## CI/CD Basics: Setting Up a Simple Pipeline in Jenkins (Let's Automate!)



Hello there, budding DevOps engineer! 🎉 Are you ready to explore the exciting world of  **Jenkins**  and  **CI/CD**? Jenkins is your automation wizard, helping you build, test, and deploy code effortlessly. Let’s create a fun pipeline to say "Hello, World!" while discovering why Jenkins is a cornerstone in the DevOps ecosystem. 🚀

----------

### [](https://100daysdevops.hashnode.dev/day-23-of-100-days-cicd-basics-setting-up-a-simple-pipeline-in-jenkins-lets-automate#heading-why-is-jenkins-so-loved "Permalink")**Why is Jenkins So Loved?**

Jenkins has a reputation for simplifying complex processes, and here’s why it’s a game-changer:

1.  **Flexible and Extensible**: With thousands of plugins, Jenkins can integrate seamlessly with tools like GitHub, Docker, Kubernetes, and more. 🛠️
    
2.  **User-Friendly Interface**: Whether you're a beginner or a pro, its intuitive UI makes navigation a breeze.
    
3.  **Open-Source and Free**: Supported by a vibrant community, Jenkins evolves constantly to meet industry needs. 💙
    
4.  **Automation at its Best**: From triggering builds to deploying applications, Jenkins saves you time and effort by automating everything!
    
5.  **Scalable for All Teams**: Whether you're running a small startup or a global enterprise, Jenkins can scale to match your requirements.
    

----------

### [](https://100daysdevops.hashnode.dev/day-23-of-100-days-cicd-basics-setting-up-a-simple-pipeline-in-jenkins-lets-automate#heading-lets-build-your-first-jenkins-pipeline "Permalink")**Let’s Build Your First Jenkins Pipeline!**

Now, let’s dive into creating a simple pipeline to print "Hello, World!" using Jenkins. 🌟

----------

#### [](https://100daysdevops.hashnode.dev/day-23-of-100-days-cicd-basics-setting-up-a-simple-pipeline-in-jenkins-lets-automate#heading-step-1-install-jenkins-if-you-havent-yet "Permalink")**Step 1: Install Jenkins (If You Haven’t Yet)**

-   Head to the  [official Jenkins website](https://www.jenkins.io/), download the latest version, and follow the installation instructions.
    
-   During setup, make sure to install the  **recommended plugins**  for a smooth experience. 🚀
    

----------

#### [](https://100daysdevops.hashnode.dev/day-23-of-100-days-cicd-basics-setting-up-a-simple-pipeline-in-jenkins-lets-automate#heading-step-2-create-a-new-pipeline-project "Permalink")**Step 2: Create a New Pipeline Project**

1.  Open Jenkins in your browser at  [`http://localhost:8080`](http://localhost:8080/).
    
2.  Click on  **"New Item"**  in the left-hand menu.
    
3.  Enter a name for your project (e.g., "HelloWorldPipeline").
    
4.  Choose  **Pipeline**  as the project type and click  **OK**  to create it.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731940519943/e29b89a9-7e80-430c-9827-f8a2deb86d9c.png?auto=compress,format&format=webp)
    

----------

#### [](https://100daysdevops.hashnode.dev/day-23-of-100-days-cicd-basics-setting-up-a-simple-pipeline-in-jenkins-lets-automate#heading-step-3-write-your-pipeline-code "Permalink")**Step 3: Write Your Pipeline Code**

Scroll down to the  **Pipeline**  section in the project configuration and:

1.  Select  **Pipeline script**.
    
2.  Paste this code:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731940576382/7f69d99c-6b17-4fa8-a826-81b1025c7617.png?auto=compress,format&format=webp)
    

💡  **What’s Happening Here?**

-   **Pipeline**: Defines the entire workflow.
    
-   **Agent**: Specifies where the pipeline should run.
    
-   **Stages**: Breaks the pipeline into steps (e.g., "Say Hello").
    
-   **Steps**: Contains the actual commands to execute.
    

----------

#### [](https://100daysdevops.hashnode.dev/day-23-of-100-days-cicd-basics-setting-up-a-simple-pipeline-in-jenkins-lets-automate#heading-step-4-save-and-run "Permalink")**Step 4: Save and Run**

1.  Click  **Save**  to store your configuration.
    
2.  On the project page, hit  **Build Now**  on the left-hand menu.
    
3.  Head to  **Console Output**  to see your pipeline in action. You’ll find  **"Hello, World! 🌍"**  printed with pride! 🎩✨
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731940626372/d9379fda-ab99-4d95-9afe-488a89c64121.png?auto=compress,format&format=webp)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731940665631/7be90e5b-cfa4-4867-8d62-9105e084752c.png?auto=compress,format&format=webp)
    

----------

### [](https://100daysdevops.hashnode.dev/day-23-of-100-days-cicd-basics-setting-up-a-simple-pipeline-in-jenkins-lets-automate#heading-what-makes-this-simple-pipeline-special "Permalink")**What Makes This Simple Pipeline Special?**

1.  **Agent Assignment**: Jenkins selects a workspace for the job.
    
2.  **Pipeline Execution**: Executes each stage sequentially.
    
3.  **Result**: Logs "Hello, World!"—your first automated task!
    

----------

### [](https://100daysdevops.hashnode.dev/day-23-of-100-days-cicd-basics-setting-up-a-simple-pipeline-in-jenkins-lets-automate#heading-why-are-pipelines-essential-in-devops "Permalink")**Why Are Pipelines Essential in DevOps?**

1.  **Automation Brilliance**: Pipelines eliminate repetitive tasks, making development faster and more efficient. 🏎️
    
2.  **Early Bug Detection**: Catch issues before they reach production with automated testing.
    
3.  **Collaboration Made Easy**: Developers can focus on coding while Jenkins handles the heavy lifting.
    

----------

### [](https://100daysdevops.hashnode.dev/day-23-of-100-days-cicd-basics-setting-up-a-simple-pipeline-in-jenkins-lets-automate#heading-next-steps-enhance-your-pipeline-skills "Permalink")**Next Steps: Enhance Your Pipeline Skills!**

Once you’ve mastered the basics, here’s what you can try next:

-   **Integrate Version Control**: Link your pipeline with GitHub or Bitbucket to trigger builds on code changes.
    
-   **Automate Tests**: Add stages to run unit or integration tests.
    
-   **Deploy Code**: Extend the pipeline to deploy your app to a server or cloud platform.
    
-   **Explore Plugins**: Use plugins to add functionality like email notifications or Docker builds. 🌈
    

----------

### [](https://100daysdevops.hashnode.dev/day-23-of-100-days-cicd-basics-setting-up-a-simple-pipeline-in-jenkins-lets-automate#heading-wrap-up "Permalink")**Wrap-Up**

Jenkins is more than a tool—it’s your partner in automation, ensuring efficiency and reliability in your DevOps workflows. Whether you’re setting up simple pipelines or deploying large-scale projects, Jenkins makes every step enjoyable. 🌟

So, what are you waiting for? Let’s automate, innovate, and take your DevOps journey to new heights! 💪🎉
