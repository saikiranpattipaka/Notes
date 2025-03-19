## Docker Notes

### 1. What is Docker?
#### Docker is a containerization platform used to develop, ship, and run applications inside containers. Containers are lightweight, portable, and isolated environments that allow you to run an application with all of its dependencies bundled together. Docker ensures that your application will run the same regardless of where it's deployed, providing consistency across multiple environments.

### Key Concepts:
#### Container: A lightweight, standalone, executable package that includes everything needed to run a piece of software, including the code, runtime, libraries, and dependencies.
#### Image: A snapshot of a container. It's a read-only template that defines the container’s environment.
#### Dockerfile: A script containing a series of instructions on how to build a Docker image.
#### Docker Engine: The core component that runs containers.
#### Docker Hub: A public registry where Docker images are stored and shared

### Docker Architecture
![alt text](image.png)

### container 
#### A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

#### A container is a bundle of Application, Application libraries required to run your application and the minimum system dependencies

### Docker vs Virtual Machines (VMs)
|Feature	         |Virtual Machines (VMs)	                |Docker (Containers)                                |
|------------------|----------------------------------------|---------------------------------------------------|
|Isolation	       |Full isolation, separate OS	            |Process-level isolation, shared kernel             |
|Resource Usage    |High (each VM needs full OS)            |Low (shares host OS)                               |
|Performance       |Slower due to OS overhead               |Faster due to lightweight design                   |
|Portability       |Less portable	                          |Highly portable across environments                |
|Start Time	       |Slow (full OS boot required)            |Fast (containers start instantly)                  |
|Security	         |Stronger (hardware-level isolation)	    |Weaker (shared kernel)                             |
|Management        |Complex at scale (hypervisor needed)    |Easier with tools like Docker Compose or Kubernetes|
|Use Case	         |Running multiple OSes, heavy workloads  |Microservices, CI/CD pipelines, lightweight apps   |



### Containers are light weight
#### Containers are lightweight because they use a technology called containerization, which allows them to share the host operating system's kernel and libraries, while still providing isolation for the application and its dependencies. This results in a smaller footprint compared to traditional virtual machines, as the containers do not need to include a full operating system. Additionally, Docker containers are designed to be minimal, only including what is necessary for the application to run, further reducing their size.

![alt text](image-2.png)

### 2. Core Concepts in Docker

#### Container: A container is a lightweight, standalone, and executable package that includes everything needed to run a piece of software (code, runtime, libraries, and dependencies). Containers are isolated from each other and from the host system.

#### Image: An image is a read-only template used to create containers. It includes the application code, libraries, dependencies, and the runtime needed for the container. Images are stored in a Docker registry (e.g., Docker Hub).

#### Dockerfile: A Dockerfile is a text document that contains instructions on how to build a Docker image. It specifies the base image, the necessary dependencies, and commands that should be executed to set up the container.

#### Docker Daemon: The Docker daemon (dockerd) is responsible for managing Docker containers and images. It listens for API requests and is the background service that runs on a host machine.

#### Docker Client: The Docker client (docker) is the command-line tool or API used to interact with Docker. It sends commands to the Docker daemon, such as starting, stopping, and managing containers.

#### Docker Registry: A Docker registry is a place where Docker images are stored. Docker Hub is the default public registry, but private registries can be created as well.

#### Docker Compose: Docker Compose is a tool for defining and running multi-container Docker applications. It allows you to use a docker-compose.yml file to configure the application’s services, networks, and volumes.

### Docker Desktop
#### Docker Desktop is an easy-to-install application for your Mac, Windows or Linux environment that enables you to build and share containerized applications and microservices. Docker Desktop includes the Docker daemon (dockerd), the Docker client (docker), Docker Compose, Docker Content Trust, Kubernetes, and Credential Helper. For more information, see Docker Desktop.

### 3. Advantages of Docker
#### Portability: Docker containers can run on any platform that supports Docker, making it easy to move applications between development, testing, and production environments.

#### Isolation: Each container runs in its own isolated environment, preventing conflicts between applications and making it easier to manage dependencies.

#### Consistency: Docker ensures that an application behaves the same across different environments by encapsulating all dependencies.

#### Resource Efficiency: Containers share the host OS kernel, which makes them more lightweight and faster than virtual machines (VMs).

#### Version Control and Reusability: Docker images can be versioned, making it easy to roll back or update applications. You can reuse base images to simplify configuration.

#### Scalability: Docker works well in microservices architectures and supports horizontal scaling, making it easier to manage distributed systems.

### Files and Folders in containers base images
```
/bin: contains binary executable files, such as the ls, cp, and ps commands.

/sbin: contains system binary executable files, such as the init and shutdown commands.

/etc: contains configuration files for various system services.

/lib: contains library files that are used by the binary executables.

/usr: contains user-related files and utilities, such as applications, libraries, and documentation.

/var: contains variable data, such as log files, spool files, and temporary files.

/root: is the home directory of the root user.
```
### Files and Folders that containers use from host operating system

#### The host's file system: Docker containers can access the host file system using bind mounts, which allow the container to read and write files in the host file system.

#### Networking stack: The host's networking stack is used to provide network connectivity to the container. Docker containers can be connected to the host's network directly or through a virtual network.

#### System calls: The host's kernel handles system calls from the container, which is how the container accesses the host's resources, such as CPU, memory, and I/O.

#### Namespaces: Docker containers use Linux namespaces to create isolated environments for the container's processes. Namespaces provide isolation for resources such as the file system, process ID, and network.

#### Control groups (cgroups): Docker containers use cgroups to limit and control the amount of resources, such as CPU, memory, and I/O, that a container can access.
    
### 4. How Docker Works
#### Docker works by using the host machine’s operating system to create isolated environments for containers. It uses OS-level virtualization to create these containers. Unlike virtual machines (VMs), which run a full operating system on top of a hypervisor, containers share the host system's OS kernel but run isolated processes.

#### Docker Engine: The Docker engine is the core part of Docker. It consists of three components:

#### Docker Daemon (Server)
#### Docker API
#### Docker CLI (Client)
#### Namespaces: Docker uses namespaces to provide isolation for containers. Namespaces allow processes in containers to have their own view of system resources, such as processes, network, and storage.

#### Control Groups (cgroups): Docker uses cgroups to limit the amount of resources (such as CPU, memory, and disk) available to each container, ensuring efficient resource usage.

### 5. Basic Docker Commands
#### docker --version: Check the installed Docker version.
#### docker pull <image>: Pull an image from a registry (e.g., Docker Hub).
#### docker build -t <image_name> .: Build a Docker image from a Dockerfile in the current directory.
#### docker run <image_name>: Create and start a container from an image.
#### docker ps: List running containers.
#### docker ps -a: List all containers (including stopped).
#### docker stop <container_id>: Stop a running container.
#### docker start <container_id>: Start a stopped container.
#### docker restart <container_id>: Restart a container.
#### docker exec -it <container_id> bash: Access the container’s shell for interactive commands.
#### docker rm <container_id>: Remove a container.
#### docker iamges : Verify Docker image is created.
#### docker rmi <image_name>: Remove a Docker image.

```
# Update the package repository
sudo apt update -y

# Install required packages
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common

# Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Add Docker repository to apt sources
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker
sudo apt update -y
sudo apt install -y docker-ce

# Start Docker service
sudo systemctl start docker

# Enable Docker to start on boot
sudo systemctl enable docker

# verify Docker Installation
docker --version

# Add your user to the Docker group (optional but recommended)
sudo usermod -aG docker $USER #ubuntu/windows

```
#### After running these commands, you may need to log out and back in (or restart the EC2 instance) for the Docker group changes to take effect

### Push Your Docker Image to Docker Hub

#### Login to Docker Hub from your EC2 instance:
```
docker login
```
#### Tag your image (replace yourusername with your Docker Hub username):
```
docker tag my-first-image yourusername/my-first-image
```
#### Push your image
```
docker push yourusername/my-first-image
```
