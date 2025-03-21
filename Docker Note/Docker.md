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
|Feature	       |Virtual Machines (VMs)	                |Docker (Containers)                                |
|------------------|----------------------------------------|---------------------------------------------------|
|Isolation	       |Full isolation, separate OS	            |Process-level isolation, shared kernel             |
|Resource Usage    |High (each VM needs full OS)            |Low (shares host OS)                               |
|Performance       |Slower due to OS overhead               |Faster due to lightweight design                   |
|Portability       |Less portable	                        |Highly portable across environments                |
|Start Time	       |Slow (full OS boot required)            |Fast (containers start instantly)                  |
|Security	       |Stronger (hardware-level isolation)	    |Weaker (shared kernel)                             |
|Management        |Complex at scale (hypervisor needed)    |Easier with tools like Docker Compose or Kubernetes|
|Use Case	       |Running multiple OSes, heavy workloads  |Microservices, CI/CD pipelines, lightweight apps   |



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


#### A Dockerfile is a text document containing a set of instructions on how to build a Docker image. Docker images are used to create containers, which are lightweight, portable, and executable software packages that contain everything needed to run an application (including the code, libraries, environment variables, and dependencies). Dockerfiles are the blueprint for creating these images.

### Components of a Dockerfile
#### Below is a detailed explanation of common Dockerfile instructions:

### 1. FROM
#### The `FROM` instruction defines the base image for your Docker image. This is the starting point of your Docker image and dictates the environment in which your app will run.

```
FROM python:3.9-slim
```
#### In this case, the base image is the official Python 3.9 image, and `slim` indicates a smaller version of the image.

### 2. LABEL
#### The `LABEL` instruction is used to add metadata to your image, such as the author, version, or description. This can help with identification and organization.

```
LABEL maintainer="youremail@example.com"
```

### 3. RUN
#### The RUN instruction is used to execute commands during the image build process, such as installing software packages or setting up your application environment. These commands are run on top of the base image.

```
RUN apt-get update && apt-get install -y curl
```
#### This will update the package list and install `curl`.

### 4. COPY
#### The `COPY` instruction copies files or directories from your local machine (or build context) into the Docker image.

```
COPY . /app
```
#### This copies the entire contents of the current directory on your local machine to the /app directory inside the Docker image.

### 5. ADD
#### The `ADD` instruction is similar to `COPY`, but it has some additional features:

#### It can handle URLs to download files.
#### It can extract TAR archives automatically.
```
ADD https://example.com/somefile.tar.gz /app/
```
#### This will download `somefile.tar.gz` from the URL and extract it to `/app/`.

### 6. WORKDIR
#### The `WORKDIR` instruction sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD` instructions that follow it. If the directory doesn't exist, Docker will create it.

```
WORKDIR /app
```
#### This sets the working directory to `/app`.

### 7. ENV
#### The ENV instruction sets environment variables in the Docker image. These variables can be accessed later in the image or container.

```
ENV APP_ENV=production
```
#### This sets an environment variable `APP_ENV` to `production`.

### 8. EXPOSE
#### The `EXPOSE` instruction informs Docker that the container listens on the specified network ports at runtime. It doesn’t publish the port, it just documents it for people using the image.

```
EXPOSE 8080
```
#### This tells Docker that the application inside the container will listen on port 8080.

### 9. CMD
#### The `CMD` instruction specifies the default command to run when a container starts. There can only be one `CMD` in a Dockerfile. If there are multiple `CMD` instructions, only the last one will take effect.

```
CMD ["python", "app.py"]
```
#### This command will run the `app.py` file using the `python` interpreter when the container starts.

### 10. ENTRYPOINT
#### The `ENTRYPOINT` instruction defines a command that will always run when the container starts. It can be overridden by `CMD`, but if both are used together, `ENTRYPOINT` is the primary command.

```
ENTRYPOINT ["python", "app.py"]
```
#### This sets python app.py as the entrypoint of the container.

### 11. VOLUME
#### The `VOLUME` instruction creates a mount point with a specific path in the container that can be linked to a directory on the host system.
```
VOLUME ["/data"]
```
### This creates a mount point at /data inside the container.

### 12. USER
#### The `USER` instruction sets the user name or UID (user ID) to use when running the container. By default, containers run as the root user, but you can specify a non-root user for security reasons.

```
USER appuser
```

#### This makes `appuser` the user under which the container runs.

### 13. ARG
#### The `ARG` instruction defines build-time variables that can be passed to the Docker build process. They can be used to customize the build process.

```
ARG version=1.0
```

#### This defines a build-time variable version with a default value of 1.0.

### 14. SHELL
#### The `SHELL` instruction allows you to specify a custom shell to use during the execution of `RUN` instructions.

```
SHELL ["/bin/bash", "-c"]
```
#### This makes the bash shell the default shell for all RUN instructions.

### Example Dockerfile
#### Here’s an example of a Dockerfile for a Python application:
```

# Set the base image
FROM python:3.9-slim

# Set metadata
LABEL maintainer="youremail@example.com"
LABEL version="1.0"

# Set environment variable
ENV APP_ENV=production

# Create and set working directory
WORKDIR /app

# Copy local files to the container
COPY . /app

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Expose port
EXPOSE 5000

# Set the default command to run the application
CMD ["python", "app.py"]

```

### How to Build and Run a Dockerfile

#### 1.Build the Docker image: Run this command in the directory where the Dockerfile is located:
```
docker build -t my-python-app .
```
#### 2.Run a container from the image: Run this command to start a container from the built image:

```
docker run -p 5000:5000 my-python-app
```
#### This will start the container, and it will be listening on port 5000


#### Difference between `CMD` & `ENTRYPOINT`
|Feature           |CMD	                                                    |ENTRYPOINT                                            |
|------------------|--------------------------------------------------------|------------------------------------------------------|
|Purpose	       |Default command to run in the container	                |Defines the main command to run                       |
|Overridable       |Yes, can be overridden by passing a different command	|Cannot be easily overridden without --entrypoint flag |
|Typical Use       |Set default command/arguments	                        |Set the main command (core process)                   |
|Syntax	           |CMD ["executable", "param1"]                            |ENTRYPOINT ["executable", "param1"]                   |


### Multi-Stage Docker Build
#### A multi-stage Docker build is a technique that allows you to create smaller, more efficient Docker images by using multiple `FROM` statements in a single Dockerfile. Each `FROM` defines a new stage in the build process, and this method is especially useful for reducing the final image size by separating the build and runtime environments.

### Key Benefits of Multi-Stage Builds:
#### Smaller Image Sizes: You can reduce the size of the final image by only copying the necessary artifacts from earlier stages, leaving behind development tools and dependencies used only for building the app.
#### Cleaner Dockerfiles: Helps in organizing and structuring the build process in a clear and maintainable manner.
#### Faster Builds: It allows the reuse of intermediate stages and layers, which can speed up the build process when only a small part of the Dockerfile changes.

#### How Multi-Stage Build Works
#### In a multi-stage Dockerfile, each stage can have its own `FROM` statement and is treated as an isolated environment for building. You define multiple `FROM` blocks in the same Dockerfile, but only the final stage is used for the final image. You can copy the necessary files from one stage to another using the `COPY --from=<stage>` command.

#### Basic Syntax
```
# Stage 1: Build Stage
FROM build-image AS build
# Install dependencies and build application
RUN install dependencies
COPY . /app
WORKDIR /app
RUN build command

# Stage 2: Final Image
FROM runtime-image
COPY --from=build /app /app
CMD ["app command"]
```

#### Here, the first stage builds the application and the second stage creates the runtime image, which only contains the necessary files for running the app, keeping it minimal.

#### Detailed Example
#### Let's break down a real-world example using a Go application.

#### 1. Stage 1: Build Stage
#### The first stage is used to build the Go binary. It uses a Golang image, installs dependencies, and builds the app.

```
# Stage 1: Build the Go binary
FROM golang:1.18 AS builder

# Set the Current Working Directory inside the container
WORKDIR /go/src/app

# Copy the Go Modules manifests
COPY go.mod go.sum ./

# Download all dependencies. Dependencies will be cached if the go.mod and go.sum files are not changed
RUN go mod download

# Copy the source code into the container
COPY . .

# Build the Go app
RUN go build -o /go/bin/app
```

#### 2. Stage 2: Final Image (Runtime Stage)
#### The second stage creates a final image for running the application. It starts with a minimal base image (e.g., `alpine`), copies the compiled binary from the builder stage, and sets the command to run the application.

```
# Stage 2: Create the runtime image
FROM alpine:latest

# Install any necessary dependencies for runtime
RUN apk --no-cache add ca-certificates

# Copy the Go binary from the builder stage
COPY --from=builder /go/bin/app /usr/local/bin/app

# Expose the port the app runs on
EXPOSE 8080

# Command to run the application
CMD ["app"]
```

#### 3. Building the Image
#### Once the multi-stage Dockerfile is ready, you can build the Docker image with the following command:

```
docker build -t my-go-app .
```

#### This command will execute the instructions in the Dockerfile, but only the final image will be used to create the container, keeping the image size small because it only contains the necessary runtime components.

#### 4. Why Multi-Stage Builds Work Well in This Case
#### Build Efficiency: The Go compiler and build tools (`golang:1.18`) are used only in the first stage to build the application and are not included in the final image.
#### Final Image Optimization: The final image is based on `alpine`, which is a much smaller image, and contains only the compiled binary (`app`) and the necessary runtime dependencies (`ca-certificates`).
#### Reduced Docker Image Size: The final image will be significantly smaller than a traditional single-stage image, which might have included unnecessary build tools, libraries, and other dependencies.

### Advanced Features of Multi-Stage Builds

#### 1. Named Stages
#### You can assign names to each stage in the Dockerfile for easier reference. This allows you to selectively copy artifacts between stages.

```
FROM node:14 AS build
WORKDIR /app
COPY . .
RUN npm install

FROM node:14-slim
WORKDIR /app
COPY --from=build /app /app
CMD ["node", "app.js"]
```
#### Here, the first stage is named `build`, and we copy files from that stage using `--from=build`.

#### 2. Using Different Base Images for Different Stages
#### Each stage can use a different base image. This is particularly useful for optimizing both the build and runtime environments.
```
# Stage 1: Build the app using a large image with build tools
FROM python:3.9 AS builder
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt

# Stage 2: Create the smaller runtime image using a minimal image
FROM python:3.9-slim
WORKDIR /app
COPY --from=builder /app /app
CMD ["python", "app.py"]
```

#### In this example, `python:3.9` (a larger image) is used in the build stage, while `python:3.9-slim` (a smaller image) is used in the runtime stage.

#### 3. Minimizing Final Image Size by Using Scratch
#### If your application doesn’t require any base operating system (for example, you’re building a static binary), you can use scratch as the final base image, which is an empty image.

```
FROM golang:1.18 AS builder
WORKDIR /go/src/app
COPY . .
RUN go build -o /go/bin/app

FROM scratch
COPY --from=builder /go/bin/app /app
CMD ["/app"]
```

#### Here, the final image contains only the app binary and no OS dependencies.

#### 4. Optimizing Build Context
#### In multi-stage builds, each stage has its own set of files, which can help reduce the amount of unnecessary files being included in each stage. For instance, you might copy only the required files to the build context in each stage rather than copying the entire repository.

```
# Stage 1: Only copy the necessary files for building the app
FROM golang:1.18 AS builder
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .

# Stage 2: Final image with only the built binary
FROM alpine:latest
COPY --from=builder /app/myapp /bin/myapp
CMD ["/bin/myapp"]
```
### 1.Best Practices for Multi-Stage Builds
#### Keep Build and Runtime Environments Separate: Only include the necessary components (e.g., compiled binaries or minimal runtime dependencies) in the final image.

#### 2.Use Smaller Base Images for Runtime: Always use the smallest possible image for the final image, such as `alpine` or `slim` variants, to minimize the image size.

#### 3.Copy Only Necessary Files: Avoid copying unnecessary files (e.g., .`git`, `tests`, build directories) into the Docker image.

#### 4.Use Caching to Speed Up Builds: Docker caches layers to avoid redoing work. Organize your Dockerfile so that the build dependencies (like installing dependencies or building the project) happen early in the Dockerfile. This way, Docker can reuse layers if the dependencies haven't changed.

#### Multi-stage Docker builds are an excellent way to optimize your Docker images by reducing their size, making the build process cleaner, and separating concerns between building and running the application. It is especially useful in scenarios where you need a specific build environment (e.g., full SDKs, compilers, etc.) but want to keep the final image as small and secure as possible. By following best practices like using smaller base images and only copying necessary files, you can significantly improve the efficiency of your Docker images.

