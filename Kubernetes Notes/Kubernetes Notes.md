## Kubernetes

#### While Docker is a powerful tool for creating and running containers, it has some drawbacks when compared to Kubernetes (K8s), especially when scaling and managing large, complex applications. Here are the main drawbacks of Docker compared to Kubernetes:

### 1. Limited Orchestration Capabilities
- Docker on its own does not have advanced orchestration capabilities. It can run individual containers, but it lacks features like automated scaling, self-healing, and load balancing across a cluster of machines.
- Kubernetes is designed for orchestration at scale. It can automatically manage the deployment, scaling, and operation of containers across multiple machines (nodes). It also offers built-in features like automatic failover, self-healing, and rolling updates, which Docker does not provide out-of-the-box.

### 2. No Native Multi-Host Management
- Docker is primarily focused on managing containers on a single host. While Docker Swarm (Docker's own orchestration tool) can manage containers on multiple nodes, its capabilities are much more limited compared to Kubernetes.
- Kubernetes is designed from the ground up to manage containers across multiple nodes (a cluster). It provides advanced features such as service discovery, load balancing, and auto-scaling across multiple machines.

### 3. Manual Scaling
- Docker requires you to manually scale containers. You have to handle the creation and distribution of containers across hosts manually or with simple tools like Docker Compose, but it doesn't offer automated scaling based on load.
- Kubernetes provides automated scaling. With Kubernetes, you can set up Horizontal Pod Autoscalers to scale containers up or down based on demand. It can dynamically adjust resources and replicate containers across the cluster based on real-time metrics (CPU usage, memory, etc.).

### 4. Stateful Applications Handling
- Docker has limited native support for managing stateful applications. For example, managing databases or services that require persistent storage can be challenging.
- Kubernetes provides robust solutions for managing stateful applications, like StatefulSets (for managing stateful workloads), and offers persistent storage management through Persistent Volumes (PVs) and Persistent Volume Claims (PVCs), making it easier to manage state and data persistence across containers.

### 5. Self-Healing and Fault Tolerance
- Docker does not natively offer self-healing capabilities. If a container crashes, you would need to manually intervene to restart or replace it.
- Kubernetes has built-in self-healing features. If a container crashes, Kubernetes can automatically detect the failure and restart the container. It can also automatically reschedule containers on other nodes if a node fails, ensuring high availability and minimal downtime.

### 6. Complexity in Large-Scale Environments
- Docker becomes harder to manage at scale without proper orchestration tools. As you add more containers and hosts, managing them manually becomes cumbersome.
- Kubernetes is designed to manage large-scale containerized applications efficiently. It abstracts the complexity of managing a large number of containers, ensuring that scaling, deployment, and updates are handled seamlessly.

### 7. Networking Complexity
- Docker's networking model is simpler but can be limiting in more complex distributed systems. It can be difficult to manage network policies, service discovery, and communication between containers spread across different hosts.
- Kubernetes provides advanced networking capabilities, including service discovery, network policies, and ingress controllers, to manage complex inter-container communication and expose services in a more structured and secure manner.

### 8. Updates and Rollbacks
- Docker has basic capabilities for updating containers, but it lacks built-in features for performing zero-downtime updates or rolling back to previous versions of containers.
- Kubernetes provides advanced deployment strategies such as rolling updates and canary releases, allowing you to upgrade your applications without downtime. It also allows for easy rollbacks if something goes wrong.

### 9. Security and Resource Isolation
- Docker provides some level of isolation between containers, but Kubernetes takes it a step further with more advanced security features, such as Pod Security Policies, Network Policies, and Role-Based Access Control (RBAC).
- Kubernetes offers more granular control over security, resource limits (CPU, memory), and access to containers within the cluster, ensuring better security and compliance in larger, multi-tenant environments.

#### While Docker is a fantastic tool for building and running individual containers, it lacks the advanced orchestration, scalability, and fault-tolerance features that Kubernetes provides. Kubernetes is more suitable for large-scale, distributed containerized applications that need automated management, scaling, and high availability across multiple hosts or a cluster of machines. Docker can be used in small-scale environments, but as complexity and scale increase, Kubernetes offers a more comprehensive solution for managing and orchestrating containerized workloads.

#### Kubernetes (K8s) is a powerful platform for managing containerized applications and automating deployment, scaling, and operations of application containers across clusters of hosts. The architecture of Kubernetes is complex but can be broken down into its core components that work together to create a unified container orchestration system.


### Kubernetes Architecture Overview
#### At a high level, Kubernetes follows a Master-Node architecture with the master components managing the cluster, and the node components running the actual workloads (pods, containers). Kubernetes consists of the following main components:
 - Master Components (Control Plane)
 - Node Components
 
![K8S Architecture](https://github.com/user-attachments/assets/d75c192b-dfc4-4180-bfaa-9caea43bed6c)

### 1. Master Components (Control Plane)
#### The Control Plane is responsible for managing the overall state of the Kubernetes cluster. The control plane makes decisions about scheduling, managing the cluster’s state, and responding to events in the cluster (e.g., deploying a new pod). The main master components include:
#### a) kube-apiserver
 - Role: The API server (`kube-apiserver`) is the central management point for all interactions in the cluster. It exposes the Kubernetes REST API, and all the cluster components communicate with each other through the API server.
 - Responsibilities:
  - Serves the Kubernetes API.
  - Handles HTTP requests from external users and internal components (like `kubectl` or controllers).
  - Validates and configures data for the API objects (e.g., pods, deployments).
  - Acts as the gateway to the entire cluster.

  b) etcd
  - Role: `etcd` is a distributed key-value store that is used to store all of Kubernetes' configuration data, cluster state, and metadata.
  - Responsibilities:
    - Stores the configuration and state of the cluster, such as the configuration of nodes, pods, and other resources.
    - Provides strong consistency and reliability (distributed consensus).
    - Serves as the source of truth for the cluster state.
  - Note: `etcd` is a critical component for cluster availability. Losing access to etcd can cause issues with the cluster, as it cannot function without it.

  c) kube-scheduler
   - Role: The `kube-scheduler` is responsible for selecting which node an unscheduled pod should run on, based on various scheduling policies and available resources.
   - Responsibilities:
     - Monitors the state of the cluster for unscheduled pods.
     - Uses available resources and constraints (like CPU, memory, and affinity rules) to decide where to place the pod.
     - Makes decisions based on resource requests, node selectors, taints, tolerations, etc.

  d) kube-controller-manager
   - Role: The `kube-controller-manager` is a set of controllers that regulate the state of the cluster. It watches the state of resources and makes changes to bring the cluster to the desired state.
   - Responsibilities:
     - Node Controller: Handles node status, watches for node failures.
     - Replication Controller: Ensures the specified number of pod replicas are running.
     - Deployment Controller: Ensures deployments are running as specified.
     - Job Controller: Manages the execution of batch jobs.
     - EndPoint Controller: Ensures the correct Endpoints are associated with services.

  e) cloud-controller-manager
   - Role: The `cloud-controller-manager` allows Kubernetes to interact with the cloud provider’s API (AWS, GCP, etc.) to manage infrastructure resources.
   - Responsibilities:
     - Manages cloud resources like load balancers, storage, and network configurations.
     - Specifically useful when running Kubernetes on cloud providers (e.g., AWS, Azure).

### 2. Node Components
#### Each node in the Kubernetes cluster runs several key components that allow it to interact with the control plane and run workloads. These node components are:

  a) kubelet
   - Role: The `kubelet` is the primary agent that runs on each node. It ensures the containers (pods) are running as expected.
   - Responsibilities:
     - Continuously monitors the state of the node and reports back to the master (API server).
     - Manages the lifecycle of containers on the node.
     - Ensures the containers are running as per the desired state defined by the control plane (e.g., pods defined by deployments).

  b) kube-proxy
   - Role: The `kube-proxy` manages network rules on nodes. It enables communication between pods across different nodes and ensures services are exposed properly.
   - Responsibilities:
    - Manages and routes traffic for services (load balancing).
    - Implements the Kubernetes Service concept, which helps expose pods to other pods or external traffic.
    - Supports both iptables and IPVS-based routing for load balancing.

  c) Container Runtime
   - Role: The container runtime is responsible for running containers on the node. Kubernetes supports several container runtimes, such as Docker, containerd, or CRI-O.
   - Responsibilities:
    - Pulls container images from registries.
    - Creates and runs containers from images.
    - Reports container status to the kubelet.

### 3. Kubernetes Objects
#### Kubernetes uses a set of API objects to represent the cluster's desired state. These objects allow users to describe the system’s behavior, including how containers should be run, scaled, and connected. Some key Kubernetes objects are:

a) Pod
 - Definition: A pod is the smallest deployable unit in Kubernetes, which can contain one or more containers that share the same network namespace and storage.
 - Role: A pod is the basic execution unit that runs containers and provides the environment for running applications.

b) ReplicaSet
 - Definition: A ReplicaSet ensures that a specified number of identical pods are running at any given time.
 - Role: It ensures the desired state of the application by maintaining the required number of pods.

c) Deployment
 - Definition: A deployment provides declarative updates for pods and ReplicaSets.
 - Role: It manages updates to your application, like rolling updates and rollbacks. It allows you to specify the number of replicas of a pod.

d) Service
 - Definition: A Service is a logical abstraction that defines a set of pods and a policy by which to access them.
 - Role: It provides stable networking and load balancing to expose the pod or set of pods.

e) Namespace
 - Definition: A Namespace provides a way to divide cluster resources between multiple users.
 - Role: It helps isolate groups of resources within the same cluster (e.g., for different teams or environments).

### 4. Cluster Communication
#### Kubernetes components communicate with each other through the Kubernetes API server, typically using HTTP/HTTPS. The components like `kube-apiserver`, `kube-controller-manager`, and `kube-scheduler` make API calls to manage and monitor resources.
 - Control Plane Communication: The control plane components communicate with the `etcd` store to keep track of the cluster state.
 - Node Communication: Nodes interact with the control plane via `kubelet` and `kube-proxy` for managing pod and service state.

### 5. High Availability and Fault Tolerance
#### To ensure high availability, Kubernetes can run multiple replicas of control plane components (such as `kube-apiserver`, `kube-controller-manager`, and `kube-scheduler`) in a clustered mode. Additionally, a distributed key-value store (etcd) is also replicated across multiple nodes to ensure fault tolerance.

### 6. Key Features
#### Kubernetes offers several features to ensure that applications run efficiently and reliably:
 - Self-healing: Automatically restarts failed containers, replaces containers, kills containers that don’t respond to your user-defined health check, and doesn't advertise them to clients until they’re ready.
 - Horizontal scaling: Kubernetes can scale your applications up and down with a simple command or automatically based on resource usage (CPU, memory).
 - Load balancing: Kubernetes provides automatic load balancing for services.
 - Automated Rollouts and Rollbacks: Kubernetes can automatically roll out and roll back updates to your application, providing better release management.
 - Service Discovery: Kubernetes offers service discovery for containers, making it easier to access other pods and services within the cluster.

## Installation

#### To install Kubernetes (K8s) on an AWS EC2 Ubuntu instance, you will need to follow a series of steps. Here’s a simple guide to get you started with Kubernetes on EC2:

Prerequisites:
- AWS EC2 instance with Ubuntu - Ensure that your EC2 instance is running an Ubuntu operating system.
- SSH Access to your EC2 instance.
- Sudo access to install and configure required tools.

### Step-by-Step Guide:
#### 1. Update the System
#### SSH into your EC2 instance and update the system packages to the latest versions.
```
sudo apt-get update
sudo apt-get upgrade -y
```
#### 2. Install Docker
#### Kubernetes uses Docker as the default container runtime, so you need to install Docker.
```
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce
```
#### Verify Docker installation:
```
sudo docker --version
```
#### 3. Install Kubernetes Components (kubeadm, kubelet, kubectl)
#### Kubernetes provides three main components: `kubeadm`, `kubelet`, and `kubectl`. `kubeadm` helps in setting up a Kubernetes cluster, `kubelet` is the agent that runs on every node in the cluster, and `kubectl` is the command-line tool for interacting with the cluster.

#### - Add the Kubernetes APT repository:
```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
#### - Install the Kubernetes components:
```
sudo apt-get update
sudo apt-get install -y kubeadm kubelet kubectl
```
#### - Hold the installed versions to prevent updates:
```
sudo apt-mark hold kubeadm kubelet kubectl
```
#### 4. Disable Swap
#### Kubernetes requires that swap is disabled. You can disable it temporarily or permanently.
#### To disable swap temporarily:
```
sudo swapoff -a
```
#### To disable swap permanently, remove or comment out any swap entries in `/etc/fstab`.
```
sudo nano /etc/fstab
```
#### 5. Initialize the Kubernetes Cluster (Master Node)
#### On the EC2 instance that you want to set up as the master node, run the following command to initialize the Kubernetes cluster:
```
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```
#### This will output a command with a kubeadm join token, which is needed for worker nodes to join the cluster. It will look like:
```
kubeadm join <your-cluster-ip>:6443 --token <your-token> --discovery-token-ca-cert-hash sha256:<hash>
```
#### Take note of this output as it will be required when adding worker nodes to the cluster.

#### 6. Set Up kubeconfig for kubectl
#### Once the cluster is initialized, you need to set up `kubectl` to interact with the cluster. Run the following commands:
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
#### 7. Install a Pod Network Add-on
#### Kubernetes requires a network plugin to enable communication between the pods in your cluster. Flannel is a commonly used network plugin, but you can choose others like Calico or Weave. To install Flannel, run:
```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```
#### Check if the pods are running:
```
kubectl get pods --all-namespaces
```
#### 8. Allow Scheduling on the Master Node (Optional)
#### By default, the master node cannot run pods. If you want to run pods on the master node (for testing purposes or small clusters), run the following:
```
kubectl taint nodes --all node-role.kubernetes.io/master-
```
#### 9. Join Worker Nodes to the Cluster
#### On each worker node (EC2 instances), run the `kubeadm join` command that was output during the k`ubeadm init` step:
```
sudo kubeadm join <your-cluster-ip>:6443 --token <your-token> --discovery-token-ca-cert-hash sha256:<hash>
```
#### This will join the worker nodes to the master node, and you can verify their status by running:
```
kubectl get nodes
```
#### 10. Verify Kubernetes Cluster
#### After completing the above steps, your Kubernetes cluster should be up and running. Check the cluster status:
```
kubectl get nodes
kubectl get pods --all-namespaces
```


## Kubernetes Distributions
#### A Kubernetes distribution refers to a pre-configured package of the Kubernetes platform, usually with additional tools, integrations, or enterprise features. The purpose is to simplify the deployment and operation of Kubernetes clusters, ensuring that users don't need to handle all the complexities of setting up Kubernetes from scratch.

### 1. Popular Kubernetes Distributions
### Managed Kubernetes Services:
#### These distributions are fully managed by cloud providers and abstract away much of the complexity of running Kubernetes.
- Amazon EKS (Elastic Kubernetes Service): AWS's managed Kubernetes service, which takes care of the Kubernetes control plane, letting you focus on running and scaling workloads on worker nodes.
- Google Kubernetes Engine (GKE): A managed Kubernetes offering by Google Cloud Platform, providing automatic scaling, patching, and integration with Google Cloud services.
- Azure Kubernetes Service (AKS): A managed Kubernetes service on Microsoft Azure, simplifying Kubernetes cluster setup and management with integrated tools.

### Enterprise Kubernetes Distributions:
#### These versions of Kubernetes are enhanced with enterprise features like better security, application monitoring, CI/CD integration, and more.
- Red Hat OpenShift: A Kubernetes distribution built by Red Hat with additional tools for CI/CD, monitoring, logging, and more. OpenShift has a more opinionated approach compared to vanilla Kubernetes and includes a web-based dashboard for cluster management.
- VMware Tanzu Kubernetes Grid (TKG): VMware’s Kubernetes distribution designed to work with their infrastructure, offering features like enterprise-grade security, multi-cluster management, and integrations with VMware products.
- Rancher: Rancher is a Kubernetes management platform that allows you to manage multiple clusters across any infrastructure. It provides a rich user interface and central management.
- Canonical’s MicroK8s: A lightweight, single-node Kubernetes solution that can be used for local development, IoT, and edge computing environments.
- K3s: A lightweight, low-overhead Kubernetes distribution designed for edge computing, IoT, and small-scale deployments, with simplified installation and reduced resource consumption.

### 2. Why Use Kubernetes Distributions?
- Ease of Installation: Most distributions come with simplified installation and management tools that make setting up Kubernetes much easier.
- Security Enhancements: Many distributions offer additional security features, such as integrated identity management, role-based access control (RBAC), and compliance features.
- Enterprise Support: Distributions like OpenShift or Tanzu offer commercial support and professional services to help enterprises with their Kubernetes operations.
- Additional Tools: Kubernetes distributions may come with integrated monitoring, logging, networking, and other operational tools that are often necessary for large-scale production deployments.

### Kubernetes Lifecycle Management
#### Kubernetes lifecycle management refers to the set of processes, tools, and practices used to manage the entire lifecycle of a Kubernetes cluster, including setup, maintenance, scaling, monitoring, and decommissioning. A proper lifecycle management strategy helps ensure smooth and reliable operation of Kubernetes clusters in production.

#### Tools for Kubernetes Lifecycle Management
#### 1. eksctl:
- A command-line tool designed by AWS to simplify the creation, management, and deletion of Amazon EKS clusters. It helps manage EKS clusters with ease and is the recommended tool for managing AWS-based Kubernetes clusters.
#### 2. Kops (Kubernetes Operations):
- What it is: Kops is an open-source tool that helps with the creation, management, and operation of Kubernetes clusters. It is particularly useful for running Kubernetes on AWS but also works on other cloud platforms like GCP, and even on-premise infrastructure.
- Use case: Kops provides a way to automate the deployment and lifecycle management of Kubernetes clusters on AWS, including provisioning infrastructure like EC2 instances, load balancers, and VPCs.

### Kops Lifecycle Management:
#### Kops is used to manage the lifecycle of Kubernetes clusters. It enables the creation of clusters with multiple nodes, scaling, and upgrading the Kubernetes version in production environments.
#### Kops Workflow:
- Create Cluster: Setup infrastructure, configure Kubernetes components, and initialize the control plane.
- Manage Node Groups: Manage groups of worker nodes, scale nodes, or update them.
- Upgrade Cluster: Upgrading the Kubernetes version in a controlled manner across all components.
- Cluster Maintenance: Performing updates, applying patches, or adjusting the configuration.
- Cluster Deletion: Safely decommissioning and deleting a cluster.

#### Kops Commands for Kubernetes Cluster Installation
##### Pre-Requisites:
Before using `kops`, ensure you have:
AWS CLI configured.
kubectl installed.
Terraform (if required for some features).

##### 1. Install Kops:
##### For Linux:
```
curl -LO https://github.com/kubernetes/kops/releases/download/v1.26.0/kops-linux-amd64
chmod +x kops-linux-amd64
mv kops-linux-amd64 /usr/local/bin/kops
```
##### 2. Install Kubectl:
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.26.0/bin/linux/amd64/kubectl
chmod +x kubectl
mv kubectl /usr/local/bin/kubectl
```
##### 3. Set up an S3 Bucket for Kops State Store:
##### Kops requires an S3 bucket to store the state of your Kubernetes cluster.
```
aws s3 mb s3://my-kops-state-store
```
##### 4. Configure Environment Variables:
##### Set environment variables to specify your region and state store.
```
export KOPS_STATE_STORE=s3://my-kops-state-store
export NAME=mycluster.k8s.local
```
##### 5. Create Cluster Configuration:
##### You can create a cluster using the following command:
```
kops create cluster --name $NAME --zones us-west-2a,us-west-2b --node-count 3 --node-size t2.medium --master-size t2.medium --dns-zone mydomain.com
```

##### 6. Update Cluster:
##### To apply changes after cluster creation or if you have edited configuration files, use:
```
kops update cluster --name $NAME --yes
```
##### 7. Validate Cluster:
##### Once the cluster is created, validate that it's running correctly:
```
kops validate cluster
```
##### 8. Export Kubeconfig:
##### Configure `kubectl` to access the new Kubernetes cluster:
```
kops export kubecfg --name $NAME
```
##### 9. Scale Node Groups:
##### If you want to scale the number of worker nodes:
```
kops edit ig --name $NAME nodes
kops update cluster --name $NAME --yes
```
##### 10. Upgrade Cluster Version:
##### To upgrade Kubernetes or other components:
```
kops upgrade cluster --name $NAME --yes
```
##### 11. Delete Cluster:
##### To delete a Kubernetes cluster managed by `kops`, use:
```
kops delete cluster --name $NAME --yes
```
#### Additional Considerations:
- Auto-scaling: Both Kops and EKS support node auto-scaling, which can automatically scale worker nodes based on resource usage.
- Monitoring: Integrate tools like Prometheus, Grafana, or AWS CloudWatch for monitoring Kubernetes clusters.
- CI/CD: Kubernetes distributions often integrate with continuous integration/continuous deployment pipelines to facilitate automated testing and deployment of applications.


## Kubernetes Pods
#### A Kubernetes Pod is the smallest and most basic deployable unit in Kubernetes. It encapsulates one or more containers, storage resources, a unique network IP, and options that govern how the containers should run. Pods are the primary unit of execution in Kubernetes.

### Key Characteristics of a Kubernetes Pod:
#### 1. Container Grouping:
- A Pod can contain one or more containers. These containers share the same resources, including storage volumes, network IP, and port space. This is particularly useful for tightly coupled applications that must share data or resources.
#### 2. Networking:
- All containers in a Pod share the same network namespace, meaning they share the same IP address and can communicate with each other using `localhost`.
- Containers within a Pod can also expose ports to communicate externally.
#### 3. Storage:
- Pods can include volumes that allow containers to share data and persist storage beyond the lifetime of a single container.
- Volumes in a Pod are mounted at the same path for each container within the Pod.
#### 4. Ephemeral:
- Pods are ephemeral in nature. If a Pod fails or is deleted, it is not automatically replaced unless managed by a higher-level abstraction like a Deployment or ReplicaSet.
#### 5. Lifecycle:
- Pods go through several phases: Pending, Running, Succeeded, and Failed.
- Kubernetes manages the Pod lifecycle and ensures that the desired state (e.g., the number of Pods) is maintained.
#### 6. Pod Scheduling:
- Pods are scheduled onto nodes in the cluster by the Kubernetes scheduler based on resource availability and constraints defined in the Pod specification.

#### Types of Pods:
- Single-container Pods: A Pod that contains only one container. This is the simplest and most common use case.
- Multi-container Pods: A Pod that contains multiple containers. The containers in the Pod share the same network and storage resources, and they often need to operate closely together, such as a main application container and a helper sidecar container.

#### Pod Use Cases:
- Single-container Pods: Running a single application, like a microservice.
- Multi-container Pods: Running tightly coupled services that need to share resources, like logging agents, monitoring tools, etc.

### Anatomy of a Pod:
A Pod has two main components:
1. Spec: Defines the configuration of the Pod, including the containers, volumes, and ports to be exposed.
2. Status: Describes the current state of the Pod (e.g., Pending, Running, Succeeded, etc.).

Example of a Simple Pod YAML Definition:
```
apiVersion: v1
kind: Pod
metadata:
  name: my-nginx-pod
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```
- name: The name of the Pod.
- containers: Defines the container(s) in the Pod.
  - name: The name of the container.
  - image: The Docker image to use for the container (in this case, `nginx:latest`).
  - containerPort: The port on which the container will listen.

#### Pod Lifecycle:
- 1.Pending: The Pod is created, but Kubernetes has not yet scheduled it to a node.
- 2.Running: The Pod is running on a node.
- 3.Succeeded: The containers in the Pod have successfully completed.
- 4.Failed: The containers in the Pod failed to start or completed unsuccessfully.
- 5.Unknown: The status of the Pod could not be determined.

## Deploying Your First Application in Kubernetes: Step-by-Step
In this section, we'll walk through how to deploy a simple Nginx web server in a Kubernetes Pod.
##### 1. Set up the Kubernetes Cluster:
Make sure you have a running Kubernetes cluster. You can use:
- Minikube for local development.
- EKS (AWS), GKE (Google Cloud), AKS (Azure), or any other Kubernetes service for cloud environments.

If you’re using Minikube, you can start a local cluster with:
```
minikube start
```
Verify the status of your cluster:
```
kubectl cluster-info
```
##### 2. Create a Pod Definition File (YAML):
Create a file called `nginx-pod.yaml` with the following content:
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```
This YAML file defines a Pod named `nginx-pod` that runs a container based on the `nginx:latest` image and exposes port 80.

##### 3. Apply the Pod Configuration:
Use the kubectl command to create the Pod using the YAML file.
```
kubectl apply -f nginx-pod.yaml
```
This will create the Pod in the Kubernetes cluster.

##### 4. Check the Status of the Pod:
To see the status of your Pod, use the `kubectl get pods` command:
```
kubectl get pods
```
You should see an output similar to:
```
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          30s
```
- READY: Indicates how many containers are running in the Pod.
- STATUS: Shows the current state of the Pod (e.g., Running).
- RESTARTS: How many times the containers in the Pod have restarted.
- AGE: How long the Pod has been running.

##### 5. Access the Nginx Web Server:
To access the Nginx server, you need to expose the Pod’s port. You can do this by creating a Service.
- 1. Expose the Pod as a Service: Create a service to expose the Pod’s port (port 80) to the outside world.
```
kubectl expose pod nginx-pod --type=NodePort --port=80 --name=nginx-service
```
- 2. Find the NodePort: After exposing the service, you can find the external port (NodePort) using the following command:
```
kubectl get services
```
You will see an output like this:
```
NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
nginx-service   NodePort    10.107.153.12   <none>        80:31388/TCP     1m
```
The NodePort is `31388`, which means you can access your Nginx web server at:
```
http://<minikube-ip>:31388
```
If you’re using Minikube, you can find the IP using:
```
minikube ip
```
##### 6. Clean Up:
To delete the Pod and the service when you're done, run:
```
kubectl delete pod nginx-pod
kubectl delete service nginx-service
```
#### Important Kubernetes Concepts for Pod Management
##### 1. Deployment:
- A Deployment manages a set of identical Pods and ensures the specified number of Pods are always running. It also handles updates and scaling.
- To create a Deployment instead of a Pod, you can use a similar YAML file with the Deployment kind instead of Pod.

##### 2. ReplicaSet:
- A ReplicaSet ensures that a specified number of Pod replicas are running at any given time. Deployments use ReplicaSets to manage Pods.


### Deployment
A Deployment in Kubernetes is a higher-level API object that manages the lifecycle of Pods and ReplicaSets. It provides features like:
- Declarative updates to Pods (rolling updates and rollbacks)
- Scaling applications easily
- Self-healing (recreating Pods if they fail)
- Version control for updates with rollbacks

Key Features:
- Rollouts & Rollbacks
- Zero Downtime Deployments
- Automated Scaling
- Declarative Management (you declare the desired state, and Kubernetes makes it happen)

#### ReplicaSet
A ReplicaSet ensures that a specified number of pod replicas are running at any given time. If a pod fails, the ReplicaSet automatically creates a new one to maintain the desired count.
- Main Role: Maintain the desired number of Pods.
- Dependency: Deployments automatically create and manage ReplicaSets.

Key Features:
- Ensures high availability
- Manages Pod replication
- Handles Pod failures gracefully

#### How Deployments and ReplicaSets Work Together
Deployment → ReplicaSet → Pods
- When you create a Deployment, Kubernetes automatically creates a ReplicaSet.
- The ReplicaSet manages the Pods (creates, deletes, and maintains the desired count).
- When updating a Deployment, Kubernetes creates a new ReplicaSet with the updated configuration and gradually transitions Pods.

### Deployment YAML Example
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
spec:
  replicas: 3  # Desired number of Pods
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app-container
        image: my-app:1.0
        ports:
        - containerPort: 80
```
Explanation:
- `replicas`: 3: Ensures 3 Pods are running.(Number of Pods)
- `selector`: Matches Pods with the label `app: my-app`.(Determines which Pods the Deployment manages)
- `template`: Defines the Pod spec (containers, ports, etc.).


#### Deployment Strategies
1. Rolling Update (default):
- Gradually replaces old Pods with new ones.
- Zero downtime during updates.

2. Recreate:
- Deletes all old Pods before creating new ones.
- Not ideal for zero-downtime apps.

3. Blue/Green & Canary Deployments: (advanced)
- Manage traffic between old and new versions during updates.

### Managing Deployments
- Create a Deployment:
```
kubectl apply -f deployment.yaml
```
- Check Deployment Status:
```
kubectl get deployments
kubectl describe deployment my-app-deployment
```
- Scale Up/Down:
```
kubectl scale deployment my-app-deployment --replicas=5
```
- Rolling Back to Previous Version:
```
kubectl rollout undo deployment my-app-deployment
```
- Monitor Rollouts:
```
kubectl rollout status deployment my-app-deployment
```
### ReplicaSet YAML Example
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-app-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app-container
        image: my-app:1.0
        ports:
        - containerPort: 80
```
Note: You usually don’t create ReplicaSets manually because Deployments handle them for you.

##### 3. StatefulSet:
- StatefulSets are used for applications that require stable identities, persistent storage, and ordered deployment and scaling (e.g., databases).

### Refer Kubernetes Doc for Commands
[Kubernetes cheat sheet](https://kubernetes.io/docs/reference/kubectl/quick-reference/)

### Deployment
A Deployment in Kubernetes is a higher-level API object that manages the lifecycle of Pods and ReplicaSets. It provides features like:
- Declarative updates to Pods (rolling updates and rollbacks)
- Scaling applications easily
- Self-healing (recreating Pods if they fail)
- Version control for updates with rollbacks

Key Features:
- Rollouts & Rollbacks
- Zero Downtime Deployments
- Automated Scaling
- Declarative Management (you declare the desired state, and Kubernetes makes it happen)

#### ReplicaSet
A ReplicaSet ensures that a specified number of pod replicas are running at any given time. If a pod fails, the ReplicaSet automatically creates a new one to maintain the desired count.
- Main Role: Maintain the desired number of Pods.
- Dependency: Deployments automatically create and manage ReplicaSets.

Key Features:
- Ensures high availability
- Manages Pod replication
- Handles Pod failures gracefully

#### How Deployments and ReplicaSets Work Together
Deployment → ReplicaSet → Pods
- When you create a Deployment, Kubernetes automatically creates a ReplicaSet.
- The ReplicaSet manages the Pods (creates, deletes, and maintains the desired count).
- When updating a Deployment, Kubernetes creates a new ReplicaSet with the updated configuration and gradually transitions Pods.

### Deployment YAML Example
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
spec:
  replicas: 3  # Desired number of Pods
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app-container
        image: my-app:1.0
        ports:
        - containerPort: 80
```
Explanation:
- `replicas`: 3: Ensures 3 Pods are running.(Number of Pods)
- `selector`: Matches Pods with the label `app: my-app`.(Determines which Pods the Deployment manages)
- `template`: Defines the Pod spec (containers, ports, etc.).


#### Deployment Strategies
1. Rolling Update (default):
- Gradually replaces old Pods with new ones.
- Zero downtime during updates.

2. Recreate:
- Deletes all old Pods before creating new ones.
- Not ideal for zero-downtime apps.

3. Blue/Green & Canary Deployments: (advanced)
- Manage traffic between old and new versions during updates.

### Managing Deployments
- Create a Deployment:
```
kubectl apply -f deployment.yaml
```
- Check Deployment Status:
```
kubectl get deployments
kubectl describe deployment my-app-deployment
```
- Scale Up/Down:
```
kubectl scale deployment my-app-deployment --replicas=5
```
- Rolling Back to Previous Version:
```
kubectl rollout undo deployment my-app-deployment
```
- Monitor Rollouts:
```
kubectl rollout status deployment my-app-deployment
```
### ReplicaSet YAML Example
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-app-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app-container
        image: my-app:1.0
        ports:
        - containerPort: 80
```
Note: You usually don’t create ReplicaSets manually because Deployments handle them for you.

### Kubernetes Services
A Kubernetes Service is an abstraction that defines a logical set of Pods and a policy to access them. It enables communication between different Pods, both inside and outside the cluster.

#### Key Concepts:
- Service: A stable endpoint (IP address & DNS name) to access Pods.
- Pod: Temporary; IPs can change. Services ensure stable access.
- ClusterIP (default): Accessible within the cluster.
- NodePort: Exposes the service on a static port on each node.
- LoadBalancer: Provisions an external load balancer (cloud-specific).
- ExternalName: Maps to an external DNS name.
  
![K8S Service](<K8S Service.png>)
### Service Types
1. ClusterIP (default)
 - Accessible only within the cluster.
 - Stable IP, DNS name.
 - Example: Internal API services.

2. NodePort
 - Exposes the service on a port on each node (e.g., `30000–32767`).
 - Access via NodeIP:NodePort.
 - Example: Dev/test environments.

3. LoadBalancer
 - Provisions an external load balancer (cloud provider-dependent).
 - Public IP for external access.
 - Example: Production web apps.

4. ExternalName
 - Maps the service to an external DNS name.
 - No proxying; DNS-based service discovery.

### Service YAML Example
```
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: ClusterIP
```
- `selector`: Matches Pods with `app: my-app`.
- `port`: Service port.
- `targetPort`: Pod port.

### Service Discovery
Service Discovery allows Pods to discover and communicate with each other automatically.

#### How It Works:
1. DNS-Based Discovery:
 - Kubernetes automatically creates DNS records for services (e.g., `my-service.default.svc.cluster.local`).
 - Pods can use DNS to access services.

2. Environment Variables:
 - Kubernetes injects environment variables into Pods for each Service (e.g.,` MY_SERVICE_SERVICE_HOST`, `MY_SERVICE_SERVICE_PORT`).
 - Deprecated in favor of DNS-based discovery.

#### Example: DNS-Based Discovery
```
curl http://my-service.default.svc.cluster.local:80
```
- `my-servic`e: Service name.
- `default`: Namespace (can vary).
- `svc.cluster.local`: Default cluster DNS suffix.

### Load Balancing
Kubernetes handles Load Balancing at multiple levels.

#### Types of Load Balancing:
1. Internal Load Balancing (Cluster-Level)
 - Kube-Proxy: Uses iptables or IPVS for internal load balancing.
 - Distributes traffic across Pods.

2. External Load Balancing (Outside the Cluster)
 - LoadBalancer Service Type: Provisions external load balancers in cloud environments (AWS ELB, GCP Load Balancer).
 - Ingress Controllers: Manage HTTP/S traffic, providing advanced routing, SSL termination, etc.

#### Kube-Proxy Load Balancing
- Mode 1: iptables-based (default)
- Mode 2: IPVS (better performance for large clusters)

How it works:
- For ClusterIP services, Kube-Proxy routes traffic to Pods using iptables rules.
- For NodePort/LoadBalancer, traffic is forwarded to the correct Pod via Kube-Proxy.

#### Load Balancer YAML Example (Cloud-based)
```
apiVersion: v1
kind: Service
metadata:
  name: my-loadbalancer
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: LoadBalancer
```
- Automatically provisions an external load balancer in supported cloud environments.

#### Kubernetes Networking
Kubernetes networking is the foundation for communication within and outside the cluster.

### Key Networking Components:
1. Pod-to-Pod Communication
- All Pods can communicate without NAT (thanks to the flat networking model).
- Each Pod has a unique IP.

2. Pod-to-Service Communication
- Services abstract Pod IPs with stable IPs/DNS.

3. External Communication
- Services like LoadBalancer and Ingress expose applications to external traffic.

#### Networking Model in Kubernetes
- Pod Network: Flat IP space for Pods (e.g., 10.0.0.0/16).
- Service Network: Separate CIDR (e.g., 10.96.0.0/12).
- Node Network: Each node has an IP in the cluster.

#### Network Policies (Security)
Network Policies control traffic between Pods.
- Allow/Deny Rules: Specify which Pods can talk to each other.
- Labels & Selectors: Define rules based on labels.

#### Example: Network Policy
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-app-traffic
spec:
  podSelector:
    matchLabels:
      app: my-app
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: frontend
```
- Only Pods with role: frontend can send traffic to Pods with app: my-app.

#### Ingress (Advanced Routing)
- Ingress Controller: Manages HTTP/S traffic routing.
- Supports:
  - SSL termination
  - Path-based routing
  - Host-based routing

##### Example: Ingress Resource
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-service
            port:
              number: 80

```
|Aspect	             |Details                                                   |
|--------------------|----------------------------------------------------------|
|Service Types       |ClusterIP, NodePort, LoadBalancer, ExternalName           |
|Service Discovery   |DNS (default), Environment Variables                      |
|Load Balancing	     |Internal (Kube-Proxy), External (LoadBalancer, Ingress)   |
|Networking	         |Flat Pod Network, Service Network, Node Network           |
|Security	           |Network Policies, RBAC                                    |
|Ingress	            |Advanced HTTP/S routing, SSL termination                  |

#### KubeShark
KubeShark is a tool designed to help with observability and debugging of Kubernetes environments. It is primarily used for monitoring and analyzing network traffic in Kubernetes clusters. Here’s a more detailed look at its use cases:

1. Network Traffic Monitoring: KubeShark allows users to capture and analyze network traffic between pods in a Kubernetes cluster. This is particularly useful for troubleshooting networking issues, understanding the flow of traffic, and detecting anomalies within the cluster.
2. Real-time Monitoring: It provides real-time insights into network activity, allowing you to observe the behavior of microservices and their communication patterns.
3. Distributed Tracing: KubeShark can be used for tracing requests as they travel across multiple services or pods, helping identify performance bottlenecks and any issues related to latency or failures.
4. Simplifying Debugging: With KubeShark, you can quickly diagnose networking-related problems like misconfigured services, failed connections, or unexpected behaviors without needing to manually inspect each individual pod’s logs or network configuration.
5. Visualization: It can visualize the network flows in the cluster, which helps in understanding the traffic between services and how data is moving within the cluster. This can aid in security auditing and performance monitoring.
6. Integration with Other Tools: KubeShark can integrate with other observability tools, like Prometheus, Grafana, or Jaeger, to provide a more holistic view of the cluster's performance and health.

In short, KubeShark helps Kubernetes operators and developers understand and manage network traffic in a microservices-based architecture, which is essential for troubleshooting, optimizing performance, and ensuring security.


