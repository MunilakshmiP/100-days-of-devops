#  Mastering Multi-Stage Builds in Docker




Welcome to **Day 14 of my 100 Days of DevOps journey**! Today, we’re diving deep into **multi-stage builds** in Docker, a crucial technique for building lean and efficient Docker images. In this post, I'll walk you through the concepts behind multi-stage builds, the step-by-step process of setting up a multi-stage Dockerfile, a hands-on experience with building a calculator app, and an exploration of distroless images.

----------

### 🌟 Concept Overview: What Are Multi-Stage Builds?

Multi-stage builds are a feature in Docker that allows us to break the build process into several stages. Each stage can have its own base image, and in the final output, we keep only the parts we actually need. Here’s why they’re so valuable:

1.  **Optimized Image Size**: In a traditional Docker build, all dependencies and tools used in the build process remain in the final image, leading to unnecessary bloating. Multi-stage builds let us remove unneeded parts after each step.
    
2.  **Security Benefits**: Smaller images contain fewer components, which reduces the surface area for vulnerabilities. For production environments, this is a huge advantage.
    
3.  **Enhanced Performance**: Leaner images reduce the time needed to deploy and start containers. This translates to better resource management and faster delivery pipelines.
    

----------

### 🛠️ When To Use Multi-Stage Builds: A Real-World Scenario

Imagine you’re building a **Go-based calculator application** in Docker. Here’s a traditional approach and how multi-stage builds improve upon it:

#### Traditional Build Process:

1.  **Base Image with Dependencies**: We’d usually start with a full **Ubuntu** image, then install Golang, and copy the application files to build the app.
    
2.  **Bloated Final Image**: This process includes all the libraries and tools needed to build the app, leading to a large image (e.g., ~900 MB). This size is due to retaining the OS layers, libraries, and Golang compiler that are not necessary for running the app.
    

#### Multi-Stage Build Process:

1.  **Stage 1 - Build Stage**: Here, we compile the app using a full base image (e.g., **Ubuntu** with Golang installed).
    
2.  **Stage 2 - Runtime Stage**: We copy the compiled app from the first stage into a minimal image, keeping only the essentials. In this example, we could use the lightweight **scratch** base image to reduce the size to ~1.96 MB.
    

----------

### 📝 Step-by-Step Guide: Writing a Multi-Stage Dockerfile

To illustrate this, let’s walk through a multi-stage Dockerfile for our **Go calculator app**:

#### Dockerfile Code Example

**Dockerfile (Single-Stage Build)**:

```bash
# This single-stage build installs Golang, copies source files, and compiles the app
FROM ubuntu AS build
RUN apt-get update && apt-get install -y golang-go
ENV GO111MODULE=off
COPY . .
RUN CGO_ENABLED=0 go build -o /app .

# This single-stage build has the compiled app, but it retains all dependencies, resulting in a larger image
ENTRYPOINT ["/app"]
```

> **Result**: This single-stage Dockerfile leads to a bloated image of around 900 MB.

**Multi-Stage Dockerfile (Optimized)**:

```bash
# Stage 1 - Building the application
FROM ubuntu AS build
RUN apt-get update && apt-get install -y golang-go
ENV GO111MODULE=off
COPY . .
RUN CGO_ENABLED=0 go build -o /app .

# Stage 2 - Minimal final image
FROM scratch
COPY --from=build /app /app
ENTRYPOINT ["/app"]
```

> **Result**: With the multi-stage build, our image size is drastically reduced to around 1.96 MB.

----------

### 🧪 Hands-On: My Experience Building the Multi-Stage Image

Here’s a summary of my hands-on experience with building and testing a multi-stage Docker image.

1.  **Repository Cloning**
    
    -   First, I cloned the [Docker-Zero-to-Hero repository](https://github.com/iam-veeramalla/Docker-Zero-to-Hero.git) to work with the sample files:
        
        ```bash
        git clone https://github.com/iam-veeramalla/Docker-Zero-to-Hero.git
        cd Docker-Zero-to-Hero/examples/golang-multi-stage-docker-build
        ```
        
2.  **Building the Docker Image**
    
    -   With the multi-stage Dockerfile, I built the image:
        
        ```bash
        docker build -t simplecalculator .
        ```
        
3.  **Results**
    
    -   The final image size was only **1.96 MB**, compared to ~900 MB in the traditional single-stage build. This size reduction demonstrates the effectiveness of multi-stage builds in Docker!
        

----------

### 📈 Benefits of Multi-Stage Builds

1.  **Reduced Image Size**: Only essential components are kept, making the final image much smaller.
    
2.  **Simplified Dependency Management**: Since build tools don’t appear in the runtime stage, the image is easier to maintain.
    
3.  **Improved Security**: Smaller images reduce the risk of vulnerabilities and potential attack surfaces.
    
4.  **Ideal for Production**: Lightweight, efficient images make multi-stage builds particularly suitable for deploying to production environments where resources and security are crucial.
    

----------

### 🚀 Going Further: Distroless Images for Enhanced Security

For even leaner and more secure images, **distroless images** provide an ultra-minimal approach. These images, pioneered by Google, omit OS-level tools and provide only the necessary runtime environment (e.g., Python for Python applications).

#### Distroless Benefits:

-   **Minimal Attack Surface**: No shell or package manager means fewer entry points for attackers.
    
-   **Improved Security**: With fewer components, distroless images reduce exposure to vulnerabilities.
    
-   **Efficiency**: Only the runtime environment is included, which means faster deployments and less storage.
    

> **💡 Pro Tip**: You can check out [Google’s Distroless GitHub repository](https://github.com/GoogleContainerTools/distroless) to explore different distroless base images for languages like Python, Java, and Go.

----------

### 💬 Interactive Q&A

I hope this guide to multi-stage builds in Docker was helpful! Feel free to try building a similar Docker image and let me know how it goes. Here’s a question for you:

**🔹 Question:** Have you tried using multi-stage builds for any of your projects? If yes, what difference did you notice in the final image size and performance?

**🔹 Follow-Up:** If you’ve explored distroless images, what challenges or benefits did you experience compared to using lightweight images like `alpine`?

----------

### 📢 Wrapping Up

Multi-stage builds are an essential tool for anyone working with Docker, especially when building production-ready containers. They bring performance improvements, enhanced security, and reduced resource consumption. With the added option of distroless images, you have even more control over the containerized environment.
