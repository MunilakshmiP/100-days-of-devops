#  Creating and Running a Dockerized Web Application🌟Deep Dive into Docker Containers


Welcome to Day 12! Today, we’ll embark on an exciting journey where you’ll take a web application and make it run inside a Docker container. By the end of this lesson, you’ll have Dockerized a Django web app, built a Docker image, run it in a container, and even accessed it from your browser. Let’s dive into the details!

----------

#### [](https://100daysdevops.hashnode.dev/day-13-of-100-days-creating-and-running-a-dockerized-web-application#heading-step-1-choose-your-web-application "Permalink")🚀  **Step 1: Choose Your Web Application**

To make this process easy to follow, we’ll work with a sample Django application. Don’t worry if you’re new to Django; we’re mainly focusing on Docker concepts. Here’s how we’ll start:

1.  **Clone the Repository**: Let’s use an existing project so you can focus on Docker without getting sidetracked by setting up the app. Open your terminal and run:
    
    Copy
    
    ```
     git clone https://github.com/iam-veeramalla/Docker-Zero-to-Hero.git
    
    ```
    
    This command clones a repository containing sample Docker projects.
    
2.  **Navigate to the Web App Folder**: Change directories to locate the web app files. Run:
    
    Copy
    
    ```
     cd Docker-Zero-to-Hero/examples/python-web-app
    
    ```
    
    Now you’re in the folder where we’ll add a Dockerfile to package and run this app in Docker.
    

----------

#### [](https://100daysdevops.hashnode.dev/day-13-of-100-days-creating-and-running-a-dockerized-web-application#heading-step-2-create-a-dockerfile "Permalink")📄  **Step 2: Create a Dockerfile**

A Dockerfile is a text document containing all the instructions needed to build your Docker image. This file defines the environment Docker will create to run your application, specifying base images, dependencies, files, and commands.

1.  **Create the Dockerfile**: Open a new file named  `Dockerfile`  in the  `python-web-app`  directory. Here’s the content to include:
    
    Copy
    
    ```
     # Use the official Ubuntu image as the base
     FROM ubuntu
    
     # Set the working directory inside the container
     WORKDIR /app
    
     # Copy the dependencies file and application code into the container
     COPY requirements.txt /app
     COPY devops /app
    
     # Update the package list and install Python and its package manager, pip
     RUN apt-get update && \
         apt-get install -y python3 python3-pip && \
         pip install -r requirements.txt && \
         cd devops
    
     # Set the entry point to start the application
     ENTRYPOINT ["python3"]
     CMD ["manage.py", "runserver", "0.0.0.0:8000"]
    
    ```
    
2.  **Explanation of Each Line**:
    
    -   `FROM ubuntu`: This line sets the base image. Here, we’re using Ubuntu as our starting point, which provides a clean and flexible environment.
        
    -   `WORKDIR /app`: The  `WORKDIR`  command sets the default directory inside the container where subsequent commands will execute. Here, it creates and navigates to  `/app`.
        
    -   `COPY requirements.txt /app`  and  `COPY devops /app`: These lines copy necessary files from our local machine to the container.  `requirements.txt`  includes the Python libraries our app depends on, and  `devops`  contains the application code.
        
    -   `RUN apt-get update ...`: This installs Python 3 and pip, then uses pip to install all required packages listed in  `requirements.txt`. This step sets up the environment for the Django app to run.
        
    -   `ENTRYPOINT`  and  `CMD`: Together, these define the commands to start the Django development server.  `manage.py runserver 0.0.0.0:8000`  will start the server on port  `8000`, making it accessible from outside the container.
        

This Dockerfile is now a blueprint that Docker will use to create our application image.

----------

#### [](https://100daysdevops.hashnode.dev/day-13-of-100-days-creating-and-running-a-dockerized-web-application#heading-step-3-build-the-docker-image "Permalink")🛠  **Step 3: Build the Docker Image**

Now, let’s build the Docker image, which will package everything our application needs into a single, portable unit.

1.  **Build the Image**: In your terminal, run:
    
    Copy
    
    ```
     docker build -t my-django-app .
    
    ```
    
    -   The  `-t`  flag lets us add a tag to the image, in this case,  `my-django-app`. This tag gives the image a readable name, making it easy to refer to later.
        
    -   The  `.`  at the end specifies the current directory as the build context, meaning Docker will include all files in this directory when building the image.
        
2.  **Watch for Completion**: As Docker processes each line in your Dockerfile, you’ll see a series of steps building your image. Once it finishes, your Docker image is ready!
    
    To verify, you can list all Docker images with:
    
    Copy
    
    ```
     docker images
    
    ```
    

----------

#### [](https://100daysdevops.hashnode.dev/day-13-of-100-days-creating-and-running-a-dockerized-web-application#heading-step-4-run-the-docker-container "Permalink")▶️  **Step 4: Run the Docker Container**

With our Docker image built, it’s time to run it as a container. Running a container will allow us to interact with our application as if it were on a live server.

1.  **Start the Container**: Execute the following command:
    
    Copy
    
    ```
     docker run -p 8000:8000 -it my-django-app
    
    ```
    
    -   The  `-p`  option maps port  `8000`  on your machine to port  `8000`  inside the container, allowing you to access the application in your browser.
        
    -   The  `-it`  flag makes the container interactive and enables a terminal session.
        
    -   `my-django-app`  refers to the tag of the image we built.
        
2.  **Test in Your Browser**: Open a browser and go to  [localhost:8000](http://localhost:8000/). If everything is set up correctly, you should see the running Django application! 🎉
    

----------

#### [](https://100daysdevops.hashnode.dev/day-13-of-100-days-creating-and-running-a-dockerized-web-application#heading-step-5-publish-your-docker-image-to-docker-hub "Permalink")🌐  **Step 5: Publish Your Docker Image to Docker Hub**

To make your image available for others or use it on other machines, you can push it to Docker Hub. Follow these steps:

1.  **Login to Docker Hub**: If you haven’t logged in, use:
    
    Copy
    
    ```
     docker login
    
    ```
    
    Enter your Docker Hub username and password when prompted.
    
2.  **Tag the Image**: For Docker Hub, tag your image with your Docker Hub username:
    
    Copy
    
    ```
     docker tag my-django-app <your_dockerhub_username>/my-django-app
    
    ```
    
    Replace  `<your_dockerhub_username>`  with your actual Docker Hub username.
    
3.  **Push the Image**: Finally, push your image to Docker Hub with:
    
    Copy
    
    ```
     docker push <your_dockerhub_username>/my-django-app
    
    ```
    
    You’ll see a progress bar as Docker uploads your image. Once done, it’s public on Docker Hub, and anyone can download and run it.
    

----------

#### [](https://100daysdevops.hashnode.dev/day-13-of-100-days-creating-and-running-a-dockerized-web-application#heading-stopping-the-container "Permalink")🔄  **Stopping the Container**

When you’re done, you can stop your container by using  `CTRL + C`  in the terminal running the container, or open a new terminal window and run:

Copy

```
docker stop <container-id>

```

To get the container ID, use  `docker ps`  to list running containers.

----------

#### [](https://100daysdevops.hashnode.dev/day-13-of-100-days-creating-and-running-a-dockerized-web-application#heading-recap "Permalink")📝  **Recap**

Today, you:

1.  Created a Dockerfile for a Django web app.
    
2.  Built and ran a Docker image of the app.
    
3.  Verified the app in a browser and published your image to Docker Hub.
    

Great job! You now have a solid grasp of Dockerizing a web application and sharing it. Let’s keep building on this foundation! 🚀
