## Discovering Docker Init – Your Shortcut to Stress-Free Containerization!🚀




Hey there, amazing people! 👋 Welcome to Day 19 of my 100 Days of DevOps journey! Today’s topic is all about  **Docker Init**  – a handy tool designed to make containerization as smooth as possible. If you’ve ever found yourself buried under the complexities of setting up Docker configurations, get ready to breathe a sigh of relief! Docker Init is here to make things faster and easier. Let’s dive right in!

----------

### [](https://100daysdevops.hashnode.dev/day-20-of-100-days-discovering-docker-init-your-shortcut-to-stress-free-containerization#heading-so-what-exactly-is-docker-init "Permalink")So, What Exactly is Docker Init?

Imagine having a friend who always knows what you need before you even ask – that’s Docker Init! Instead of laboring over Docker configurations line by line, Docker Init does it for you. With this tool, you’ll have a ready-to-go Docker setup in no time, saving energy for what really matters: getting your application up and running.

### [](https://100daysdevops.hashnode.dev/day-20-of-100-days-discovering-docker-init-your-shortcut-to-stress-free-containerization#heading-lets-kick-things-off-setting-up-a-practice-app "Permalink")Let’s Kick Things Off: Setting Up a Practice App

To get the most out of Docker Init, we’ll use a sample app that’s perfect for this exercise. It’s not my app, but it’s an ideal pick to practice containerizing.

1.  **Clone the App**  
    First, let’s bring in the app:
    
    Copy
    
    Copy
    
    ```
     git clone https://github.com/iam-veeramalla/python-for-devops.git
     cd python-for-devops/simple-python-app
    
    ```
    
    This app is a simple Python-based "Hello World" application that runs on port 8000.
    
2.  **Test the App on Your Machine**  
    Before we start containerizing, let’s make sure it’s running smoothly on our local system:
    
    Copy
    
    Copy
    
    ```
     pip3 install -r requirements.txt
     python3 app.py
    
    ```
    
    Now, head over to  [`http://localhost:8000`](http://localhost:8000/), and you should see the welcoming "Hello World" message.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731487631583/e9aa022e-7e08-41ed-8a1f-61842d54f48a.png?auto=compress,format&format=webp)
    

----------

### [](https://100daysdevops.hashnode.dev/day-20-of-100-days-discovering-docker-init-your-shortcut-to-stress-free-containerization#heading-lets-make-things-happen-with-docker-init "Permalink")Let’s Make Things Happen with Docker Init!

Now for the best part – Docker Init is going to take the lead on setting up our Docker configuration. Run the following command and let Docker Init guide you:

Copy

Copy

```
docker init

```

Docker Init will ask a few questions to get things just right:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731487805225/d43d2664-15d1-4de3-857e-1257bb9d1ca3.png?auto=compress,format&format=webp)

-   **Language**: Select Python (it’s usually detected automatically).
    
-   **Version**: Confirm your preferred Python version.
    
-   **Port**: Set to 8000 (to match our app).
    
-   **Start Command**: Enter  `python3`  [`app.py`](http://app.py/).
    

Once that’s done, Docker Init will generate the essentials for you:

-   **Dockerfile**
    
-   **docker-compose.yml**
    
-   [](http://readme.md/)**[README.md](http://readme.md/)**  with basic setup instructions
    

With just a few questions answered, Docker Init has prepared all the files needed to containerize the app. Easy, right?

----------

### [](https://100daysdevops.hashnode.dev/day-20-of-100-days-discovering-docker-init-your-shortcut-to-stress-free-containerization#heading-running-the-app-in-a-container-lets-see-it-in-action "Permalink")Running the App in a Container – Let’s See It in Action!

With our files ready to go, it’s time to see this app running from inside a Docker container.

1.  **Build and Run the App with Docker Compose**  
    Using Docker Compose, we can build and start the container all at once:
    
    Copy
    
    Copy
    
    ```
     docker compose up --build
    
    ```
    
    Once it’s up and running, open  [`http://localhost:8000`](http://localhost:8000/)  again. This time, you’ll see "Hello World" served up straight from inside the container!
    
2.  **Take a Peek at the Dockerfile**  
    Docker Init’s Dockerfile comes with some smart configurations right out of the box:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731487870070/280d60ef-b66a-4e63-a951-331faa47b289.png?auto=compress,format&format=webp)
    
    -   **Non-root User**: A non-root user is added for extra security.
        
    -   **Efficient Layering**: Dependencies are installed in layers, which makes future builds faster.
        
    -   **Slim Base Image**: Keeps the container light and efficient.
        

### [](https://100daysdevops.hashnode.dev/day-20-of-100-days-discovering-docker-init-your-shortcut-to-stress-free-containerization#heading-wrapping-up "Permalink")Wrapping Up

And that’s a wrap for today! Docker Init is an incredibly helpful tool that makes containerizing applications quick and easy. Whether you’re just starting out with Docker or have some experience, Docker Init is a time-saver you’ll appreciate.

Thanks for joining me on this journey – stay tuned for more containerization tips and tricks tomorrow!
