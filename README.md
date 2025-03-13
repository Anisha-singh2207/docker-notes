# What is Docker?
 
 Docker is a platform for developing, shipping, and running applications inside containers.
 Containers are lightweight, portable, and consistent environments that include everything an application needs to run (code, libraries, dependencies, etc.).

# Why do we need docker?
 One of the primary reasons we need Docker is its ability to ensure portability across different environments. By packaging applications with all their dependencies into containers, Docker ensures that the application runs consistently whether it’s on a developer’s local machine, staging, or production environments. This eliminates the common issue of "it works on my machine" since Docker containers encapsulate everything the app needs, such as code, libraries, and configurations, ensuring it behaves the same everywhere. Additionally, Docker provides isolation, allowing each application to run in its own container with its specific dependencies, avoiding conflicts that arise when different applications require different versions of the same libraries or services.

# What is a Container?
A way to package an application with all the necessary dependencies and configuration.It can be easily shared and Makes deployment and development efficient.

# Architecture of Docker
Docker Client: This is the command-line interface (CLI) that you use to interact with Docker. It sends commands to the Docker daemon to create and manage containers.

Docker Daemon: The Docker daemon (dockerd) runs in the background and is responsible for building, running, and managing containers and images. It listens to the client’s commands and executes them.

Docker Images: These are read-only templates that contain the code, libraries, and dependencies needed to run an application. Containers are created from images.

Docker Containers: Containers are lightweight, isolated environments that run an application using the image. They share the host system's OS kernel but are isolated from each other.

Docker Registry: A repository (like Docker Hub) where images are stored. You can pull images from or push custom images to a registry.

Docker Volumes: These are used for storing data persistently outside the container. Data in volumes can persist even if the container stops or is removed.

Docker Networks: Networks allow containers to communicate with each other. Docker provides various network types like bridge and host to manage communication.

# Docker Vs Virtual machine
Docker:
Shares the host system’s OS kernel.
Lightweight and faster to start.
More resource-efficient since it doesn’t require a full operating system.
Ideal for running microservices and applications in isolated environments.

Virtual Machines (VMs):
 Runs a full operating system with its own kernel.
 Heavier and slower to start.
 Requires more resources (CPU, memory, storage) because each VM runs its own OS.
  Better for running different OSes or full-system virtualization.

#What is docker file and images?
Dockerfile: A Dockerfile is a text file that contains a series of instructions to build a Docker image. It defines the environment and the application setup, such as the base image, dependencies, and how to run the application.

Docker Image: A Docker image is a read-only template that contains the application and its dependencies, as defined in the Dockerfile. It is used to create containers. Images are the blueprint for containers, and once an image is built, it can be reused to run containers on any system with Docker installed.

# What is docker Hub?
Docker Hub is a cloud-based registry service where you can store, share, and manage Docker images. It’s the default public registry for Docker images and provides access to a vast library of pre-built images, including popular ones like Ubuntu, Node.js, and MySQL

# How to create Docker files?
First set up react environement on VS code and name the folder as test-app 
Create dockerFile as the name of the file
Write all the codes attach in the below link.
![image](https://github.com/user-attachments/assets/73b79672-9e79-452d-bfd7-7fd5556ed730)

For executing the codes run command docker build .
After running your image will be downloaded.

# GENERAL COMMANDS USED IN DOCKER(WINDOWS)
1.Check Docker version:

# docker --version
 
2.Display Docker system info:

 # docker info

3.Pull an image from Docker Hub:

# docker pull <image_name>

4.List all images on your system:

# docker images

5.Remove an image:

# docker rmi <image_id>

6.Run a container:

# docker run <options> <image_name>
Example: docker run -d -p 8080:80 nginx

7.List running containers:

# docker ps

8.List all containers (running and stopped):

# docker ps -a

9.Stop a running container:

# docker stop <container_id>

10.Start a stopped container:

# docker start <container_id>

11.Remove a container:

# docker rm <container_id>

12.Remove a stopped container:

# docker container prune

# What is port mapping
Port Mapping in Docker allows you to expose a container's internal ports to the host machine so that external applications can access them. This is particularly useful when running web applications or services inside containers, as you need to map the container’s internal ports to the host machine’s ports.

When you run a Docker container, it has its own internal network (e.g., port 8080 inside the container), but to access it from the outside world (e.g., your browser or any external service), you need to map that port to a port on your host machine (e.g., localhost:8080).

Command to use it : docker run -p <host_port>:<container_port> <image_name>

<host_port>: The port on your local machine (host) that will be bound to the container.
<container_port>: The port inside the Docker container that is being exposed.
<image_name>: The name of the Docker image you are running.

# What if we want to run container of postgress and reddis for example
Write the configuration as shown in the below attachement in docker-compose.yml file
![image](https://github.com/user-attachments/assets/a60c84e2-ff8d-44bd-8469-fbc17afb64bf)

Run commmand docker compose up

# Docker networking

1. Bridge Network
 What is it?
 The Bridge network is the default network mode for containers in Docker. It creates a private internal network on your host machine, and all containers on the Bridge network can communicate with each other.

 How does it work?
 When containers are connected to the Bridge network, they can communicate with each other using their IP addresses within the network, but they can't directly communicate with the host machine unless you expose ports using port mapping (-p flag).

  When to use it?
 Use the Bridge network when you need containers to communicate with each other within the same host, but don’t need direct access to the host.

   Example: When you run a container like this: docker run -d --name container1 --network bridge nginx
  This will create a container connected to the default Bridge network, and you can map ports to access the container from the host.
  
  2.Host Network

  What is it?
 The Host network mode means that the container shares the network stack of the host machine. This means that the container will use the host's IP address and ports directly, without isolation.

  How does it work?
 When you use the Host network, the container doesn't get its own IP address. Instead, it uses the host’s IP and can access the host’s network directly. It’s as if the container is part of the host’s network.

   When to use it?
   Use the Host network when you need high performance and want the container to directly access the host’s network without any isolation.

   Example: When you run a container like this: docker run -d --name container1 --network host nginx
  This will run the container with the host's network. The container can directly use the host's IP and ports.

  # What is Volume Mounting in Docker?

  In Docker, volume mounting refers to the process of linking data between the host machine and the Docker container. This allows the container to persist  , share data between containers, and access data on the host system.

 Without volume mounting, any data created inside a container would be lost when the container is stopped or deleted. Volume mounting ensures that 
 important data is saved even if the container is removed or restarted.

 # Efficient Caching in Docker Layers

Docker images are built in layers, and each layer represents a set of file system changes that occur when an instruction in the Dockerfile is executed. Docker uses layer caching to speed up the image build process by reusing previously built layers when possible. This is particularly useful for optimizing Dockerfile builds and ensuring faster rebuilds when making changes to your application.
Why is Caching Important?

When Docker builds an image, it looks at each instruction in the Dockerfile (such as RUN, COPY, and ADD). For each instruction, Docker checks if it has previously built the layer with the same content. If the content is the same, Docker will reuse the cached version of the layer instead of rebuilding it, which speeds up the build process and makes the build more efficient.

# Docker Multi-Stage Builds

Multi-stage builds in Docker allow you to use multiple FROM statements within a single Dockerfile to create multi-step images. This is useful for reducing the size of your final Docker image by separating the build environment from the production environment.

With multi-stage builds, you can do things like:

  Build the application in one stage (using heavy build tools and dependencies).
 Copy the build artifacts to a second, more lightweight image that only includes the runtime dependencies.

This approach helps to minimize the size of the final image and improve security by reducing the attack surface.





 
