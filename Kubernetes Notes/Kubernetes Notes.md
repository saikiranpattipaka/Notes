## Kubernetes

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

#### Kubernetes Ingress
An Ingress is a collection of rules that allow inbound connections to reach the cluster services. It provides HTTP/S routing functionality, including:
- Routing based on hostnames.
- Routing based on URL paths.
- SSL/TLS termination.
- URL path rewrites.
- External DNS management.
- Load balancing.

Ingress allows you to configure a single entry point (URL or domain) to manage all your services, avoiding the need for separate LoadBalancer or NodePort services for each service exposed to the outside world.

#### Ingress Resource Definition
The Ingress resource defines the rules and configurations for how external traffic should be routed to services in your cluster. The Ingress resource can be customized to meet specific needs, such as SSL configuration, URL rewrites, etc.

Basic Ingress Example
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /app1
        pathType: Prefix
        backend:
          service:
            name: app1-service
            port:
              number: 80
      - path: /app2
        pathType: Prefix
        backend:
          service:
            name: app2-service
            port:
              number: 80
```
In this example:
- Requests to `http://example.com/app1` will be forwarded to the `app1-service` on port 80.
- Requests to `http://example.com/app2` will be forwarded to the `app2-service` on port 80.

Key Components of an Ingress Resource:
1. Host: The domain name (e.g., `example.com`) that the Ingress will match.
2. Path: The URL path (e.g., `/app1`) that triggers the rule.
3. PathType: Specifies how the path should be matched (`Prefix`, `Exact`, or `ImplementationSpecific`).
4. Backend: The Kubernetes Service that should handle the request.

#### Ingress Controllers
An Ingress Controller is a Kubernetes resource that implements the rules defined in the Ingress resource. The controller typically acts as a reverse proxy, load balancer, or ingress gateway, forwarding requests to the correct services based on Ingress rules.

Ingress controllers are implemented by different providers:
- NGINX Ingress Controller: One of the most popular Ingress controllers, typically used for managing HTTP(S) traffic, supports SSL termination, load balancing, and many other features.
- Traefik Ingress Controller: A modern ingress controller with dynamic reconfiguration and easy integration with containerized services.
- HAProxy Ingress Controller: Known for its high-performance capabilities, especially in complex routing scenarios.
- Istio (Envoy) Ingress Controller: A more advanced option that integrates with service meshes like Istio.


#### Ingress Path Types
Ingress has three types of path matching that help define how URLs should be routed:

1. Prefix (default): Matches any path that starts with the specified path prefix.
- For example, /app1 will match /app1, /app1/xyz, and /app1abc.

2. Exact: Matches the exact path.
- For example, /app1 will only match /app1 and nothing else (not /app1/xyz).
3. ImplementationSpecific: Path matching behavior depends on the Ingress controller implementation.

Example of Using Path Type:
```
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /images
        pathType: Exact
        backend:
          service:
            name: image-service
            port:
              number: 80
      - path: /api
        pathType: Prefix
        backend:
          service:
            name: api-service
            port:
              number: 80
```
In this case:
- `/images` will exactly match requests to `/images`.
- `/api` will match requests to `/api`,` /api/xyz`, and `/api/anything`.

#### TLS/SSL with Ingress
Kubernetes Ingress supports TLS termination. TLS termination means that the Ingress controller decrypts incoming HTTPS traffic and forwards it to the backend services over HTTP.

Steps to Enable TLS in Ingress:
1. Create a TLS Secret: You need a TLS certificate and its private key stored in a Kubernetes Secret. You can generate a secret using `kubectl`.

Example:
```
kubectl create secret tls my-tls-secret --cert=path/to/cert.crt --key=path/to/cert.key
```
2. Use the TLS Secret in an Ingress: You can then reference the TLS secret in the Ingress definition to enable HTTPS.

Example:
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  tls:
  - hosts:
    - example.com
    secretName: my-tls-secret
  rules:
  - host: example.com
    http:
      paths:
      - path: /app1
        pathType: Prefix
        backend:
          service:
            name: app1-service
            port:
              number: 80
```
This Ingress resource ensures that:
- Traffic to `https://example.com/app1` will be handled with SSL termination.
- The traffic will be forwarded to the `app1-service` on HTTP (port 80).

#### Ingress Annotations
Annotations are used in Ingress resources to provide specific configuration options to the Ingress controller.

Some common annotations include:
- nginx.ingress.kubernetes.io/rewrite-target: Specifies the target path for URL path rewrites.
```
nginx.ingress.kubernetes.io/rewrite-target: /
```
- nginx.ingress.kubernetes.io/ssl-redirect: Controls whether HTTP traffic should be redirected to HTTPS.
```
nginx.ingress.kubernetes.io/ssl-redirect: "true"
```
- nginx.ingress.kubernetes.io/proxy-body-size: Specifies the maximum allowed size for the request body.
```
nginx.ingress.kubernetes.io/proxy-body-size: "8m"
```
- nginx.ingress.kubernetes.io/force-ssl-redirect: Forces all HTTP requests to be redirected to HTTPS.
```
nginx.ingress.kubernetes.io/force-ssl-redirect: "true"
```
#### Advanced Features of Ingress
1. Path Rewriting: Ingress can rewrite paths as they are forwarded to the backend services, often used when the backend service is expecting different paths than those used externally.

Example of path rewrite:
```
nginx.ingress.kubernetes.io/rewrite-target: /newpath/
```
2. Multiple Hosts: You can have multiple host definitions within the same Ingress resource, allowing routing based on the hostname.

Example:
```
spec:
  rules:
  - host: app1.example.com
    http:
      paths:
      - path: /
        backend:
          service:
            name: app1-service
            port:
              number: 80
  - host: app2.example.com
    http:
      paths:
      - path: /
        backend:
          service:
            name: app2-service
            port:
              number: 80
```              
3. Rate Limiting: Some Ingress controllers (like NGINX) support rate limiting of incoming requests.

#### Best Practices for Using Ingress
- Use HTTPS: Always use TLS to encrypt traffic to and from your Kubernetes cluster. Avoid exposing services over HTTP without TLS, especially in production environments.
- Limit Ingress Annotations: While annotations offer flexibility, limit their use to only what's necessary to avoid complexity and ensure maintainability.
- Leverage Load Balancing: Use Ingress controllers for load balancing and high availability, ensuring that traffic is spread evenly across your services.
- Custom Domains: Use custom domain names (e.g., app1.example.com) for more meaningful and manageable URL structures.

#### Troubleshooting Ingress
- Check the Ingress Controller Logs: Inspect the logs of your Ingress controller to diagnose issues with routing and configuration.
```
kubectl logs <nginx-ingress-controller-pod> -n ingress-nginx
```
- Verify Ingress Resource: Ensure that the Ingress resource is correctly defined and applied.
```
kubectl describe ingress my-ingress
```
- Inspect Service Health: Make sure the target services behind the Ingress are running and healthy.

### Kubernetes RBAC (Role-Based Access Control)
Kubernetes RBAC (Role-Based Access Control) is a method for regulating access to resources within a Kubernetes cluster based on the roles of individual users or services. With RBAC, you can define who can perform what actions on which resources in the cluster, thus enhancing security and controlling access.

RBAC uses the concept of Roles and RoleBindings to allow or deny actions, providing fine-grained access control to the Kubernetes API resources.

1. Core Concepts of Kubernetes RBAC
RBAC in Kubernetes involves the following key components:

1.1. Roles
A Role defines a set of permissions within a namespace or across the entire cluster. It specifies what resources can be accessed and what operations (verbs) are allowed on those resources.

There are two types of roles:
- Role: Defines permissions within a specific namespace.
- ClusterRole: Defines permissions across the entire cluster.

1.2. RoleBindings
A RoleBinding grants the permissions defined in a Role to a user or set of users within a specific namespace. The binding associates a Role or ClusterRole with a user, group, or service account.

There are two types of bindings:
- RoleBinding: Grants the permissions of a Role within a specific namespace.
- ClusterRoleBinding: Grants the permissions of a ClusterRole across the entire cluster.

1.3. Verbs (Actions)
Verbs represent the actions that can be performed on resources. Some of the most common verbs are:
- get: Retrieve a resource.
- list: List resources.
- create: Create a new resource.
- update: Modify an existing resource.
- delete: Remove a resource.
- watch: Watch resources for changes.
- patch: Apply partial changes to a resource.

1.4. Resources
Resources are the objects or entities on which operations can be performed. Examples of resources include:
- pods
- deployments
- services
- secrets
- namespaces

1.5. Namespaces
RBAC can be configured to apply within specific namespaces or globally to the entire cluster. The Role is namespace-scoped, while ClusterRole applies to the entire cluster.

2. RBAC Policies
RBAC policies are created using Role and ClusterRole resources, which define the permissions for users or groups, and RoleBinding or ClusterRoleBinding, which specify who receives these permissions.

2.1. Role Definition
A Role defines a set of permissions in a particular namespace. Here is an example of a Role that grants read-only access to Pods in the default namespace:
```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- verbs: ["get", "list"]
  apiGroups: [""]
  resources: ["pods"]
```
In this example:
- verbs: `get`, `list` — The user can read information about pods.
- resources: `pods` — The user is allowed to interact with pod resources.
- apiGroups: `""` refers to the core Kubernetes API group (used for resources like pods, services, etc.).

2.2. ClusterRole Definition
A ClusterRole defines permissions at the cluster level, affecting resources across all namespaces. For instance, a ClusterRole that grants read-only access to all Pods in the cluster:
```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: cluster-pod-reader
rules:
- verbs: ["get", "list"]
  apiGroups: [""]
  resources: ["pods"]
```
This ClusterRole grants read-only access to Pods across all namespaces in the cluster.

2.3. RoleBinding Definition
A RoleBinding assigns a Role to a user, group, or service account within a specific namespace.

Example of a RoleBinding for assigning the `pod-reader` role to a user named `jane` in the `default` namespace:
```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods-binding
  namespace: default
subjects:
- kind: User
  name: jane
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```
In this example:
- subjects: Specifies the user jane to whom the role is granted.
- roleRef: Refers to the pod-reader role in the default namespace.

2.4. ClusterRoleBinding Definition
A ClusterRoleBinding binds a ClusterRole to a user, service account, or group across the entire cluster.

Example of a ClusterRoleBinding for assigning the `cluster-pod-reader` ClusterRole to a service account named `read-only-sa` in the default namespace:
```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: read-cluster-pods-binding
subjects:
- kind: ServiceAccount
  name: read-only-sa
  namespace: default
roleRef:
  kind: ClusterRole
  name: cluster-pod-reader
  apiGroup: rbac.authorization.k8s.io
```
In this example:
- subjects: Specifies the `read-only-sa` service account to which the role is bound.
- roleRef: Refers to the `cluster-pod-reader` ClusterRole.

3. RBAC Use Cases
3.1. Namespace-Based Access Control
If you want to limit access to resources within a specific namespace, use Role and RoleBinding.
- Role for read-only access to Pods within a namespace.
- RoleBinding to bind the Role to a user or service account.

3.2. Cluster-Wide Access Control
To grant permissions to resources across the entire cluster (such as managing nodes or creating namespaces), use ClusterRole and ClusterRoleBinding.
- ClusterRole for full control of resources across all namespaces.
- ClusterRoleBinding to assign cluster-wide permissions to users or service accounts.

3.3. Service Accounts and Pod Security
RBAC is often used to define access for Service Accounts within Pods. For example, you might create a ServiceAccount that a pod will use to access the Kubernetes API, and then define roles and bindings to control what the pod can access.

4. Advanced RBAC Features
4.1. Aggregated ClusterRoles
You can combine multiple ClusterRoles into a single role. This is done by creating a new ClusterRole and referring to other existing ClusterRoles.

Example of aggregating multiple ClusterRoles:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: full-access
rules:
  - kind: ClusterRole
    name: admin
  - kind: ClusterRole
    name: edit
```
This new `full-access` role aggregates the `admin` and `edit` ClusterRoles.

4.2. RBAC with Groups
RBAC allows you to assign roles to groups (e.g., Active Directory groups). This is useful for managing access at scale.

Example with a group:
```
subjects:
- kind: Group
  name: developers
  apiGroup: rbac.authorization.k8s.io
```
This binds a role to the developers group.

5. Best Practices for RBAC
- Principle of Least Privilege: Always assign only the minimal permissions necessary for a user or service to perform their tasks.
- Use Namespaces: Where possible, define RBAC rules within namespaces to limit the scope of permissions.
- Service Accounts for Applications: Assign service accounts to your applications and bind roles to those service accounts rather than using default service accounts.
- Regular Auditing: Regularly audit roles and role bindings to ensure that permissions are aligned with actual needs and security policies.
- ClusterRoles for Global Access: Use ClusterRoles only when you need permissions across the entire cluster.
- Manage Group Permissions: Instead of assigning roles to individual users, assign roles to groups for easier management and scalability.

6. Troubleshooting RBAC Issues
- kubectl auth can-i: Use this command to check whether a user has permission to perform a specific action.
```
kubectl auth can-i get pods --as=jane --namespace=default
```
- Audit Logs: Kubernetes has built-in audit logging that can help trace permission issues.
- Describe Role/RoleBinding: Use `kubectl describe` to inspect roles and bindings:
```
kubectl describe role pod-reader --namespace=default
kubectl describe rolebinding read-pods-binding --namespace=default
```

### Kubernetes Custom Resources (CR)
Kubernetes (K8s) allows users to extend its functionality by defining custom resources. A Custom Resource (CR) is an extension of the Kubernetes API that allows you to define your own object types. These resources allow you to store and manage your application's state in the Kubernetes API server and build custom controllers to manage the lifecycle of your application.

#### Key Concepts
1. Custom Resource Definitions (CRD):
- Custom Resource Definition (CRD) is the schema or blueprint that defines the structure of a custom resource.
- CRDs allow you to create and manage custom resources in your Kubernetes cluster.
- Once a CRD is created, Kubernetes will automatically manage the API group and versioning for your custom resources.

2. Custom Resources (CR):
- A Custom Resource (CR) is an instance of a custom resource type that is created based on the CRD.
- CRDs define the API schema, and CRs are the actual instances of the resources defined by the CRD.
- Custom resources behave similarly to native Kubernetes resources (like Pods, Services, etc.).

3. Controller:
- A Controller is an application that watches the state of the custom resource and takes appropriate actions based on that state.
- Controllers are usually written to reconcile the desired state (described in the custom resource) with the current state of the system.

#### Benefits of Custom Resources
- Extensibility: You can define resources that are specific to your application.
- Declarative Management: Use the same declarative YAML approach as other Kubernetes resources.
- Automated Lifecycle Management: Custom resources can be managed by custom controllers to automatically update, create, or delete resources based on the state of the custom resource.
- Standardized API: CRDs leverage Kubernetes' API server to expose resources, so users can interact with them in a familiar way using kubectl.

#### Steps to Define and Use a Custom Resource
1. Define a Custom Resource Definition (CRD)
A CRD specifies the schema for your custom resource and enables Kubernetes to manage your custom objects.
```
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: myresources.example.com
spec:
  group: example.com
  versions:
    - name: v1
      served: true
      storage: true
      schema:
        openAPIV3Schema:
          type: object
          properties:
            spec:
              type: object
              properties:
                replicas:
                  type: integer
                image:
                  type: string
  scope: Namespaced
  names:
    plural: myresources
    singular: myresource
    kind: MyResource
    shortNames:
      - mr
```
In this example:
- `group` is the API group of your custom resource.
- `versions` specifies the version of the custom resource (e.g., v1).
- `scope: Namespaced` indicates that the custom resource is namespace-scoped.
- `names` defines the plural, singular, and kind of the custom resource.
- `openAPIV3Schema` defines the structure of the resource, including fields like `spec.replicas` and `spec.image`.

2. Create a Custom Resource
Once the CRD is created, you can create custom resources (CRs) of that type.
```
yaml
Copy
apiVersion: example.com/v1
kind: MyResource
metadata:
  name: myresource-instance
spec:
  replicas: 3
  image: nginx
```
- `apiVersion: example.com/v1` refers to the custom API version defined in the CRD.
- `kind: MyResource` matches the kind defined in the CRD.
- `spec` contains the actual data for the resource, in this case, the number of replicas and the image name.

3. Apply the CRD and Custom Resource
To create the CRD, run:
```
kubectl apply -f crd.yaml
```
To create the custom resource, run:
```
kubectl apply -f custom-resource.yaml
```
4. Create a Controller for the Custom Resource
A custom controller is responsible for interacting with the custom resource. It listens for changes to the resource and then takes actions like creating, updating, or deleting other Kubernetes resources.
- Custom controllers can be built using the Operator SDK or by writing your own controller in a programming language like Go, Python, or Java.
- The controller watches the Kubernetes API for changes in the custom resource and performs actions accordingly.

Example: A custom controller might watch the custom resource `MyResource` and automatically create the specified number of replicas of a Pod running the defined image.

5. Interact with Custom Resources
Once a CRD and custom resource are defined, you can manage your custom resource with `kubectl`.

- List custom resources:
```
kubectl get myresources
```
- Get details of a custom resource:
```
kubectl describe myresource myresource-instance
```
- Delete a custom resource:
```
kubectl delete myresource myresource-instance
```
6. Use Custom Resources in your Application
Custom resources can help automate and manage application-specific configurations. For example:
- Stateful Applications: You can define a custom resource to manage a stateful application and automatically handle replicas, failover, backups, etc.
- Third-Party Integrations: Use CRDs to represent integration with third-party services, like database clusters or message queues, and manage them through Kubernetes.

#### Advanced Topics
1. Validation and Schema Enforcement:
- The CRD schema can enforce validation on custom resources (e.g., require that certain fields are non-empty, have specific values, etc.) by defining the schema in `openAPIV3Schema` within the CRD.
- You can use regular expressions or specific types (like `string`, `integer`, `boolean`, etc.) to enforce constraints.
2. Subresources in Custom Resources:
- You can define subresources for your custom resources, such as `status` or `scale`.
- For example, `status` is often used to store the current state of the resource (e.g., `replicas`), while `scale` can be used to modify the number of replicas of the resource.
3. Multiple Versions:
- You can define multiple versions of the same custom resource within a CRD.
- Kubernetes supports versioning of CRDs, and you can introduce breaking changes by defining new versions while still supporting old versions for backward compatibility.
4. API Aggregation Layer:
- The CRD API is part of the Kubernetes API aggregation layer. It allows third-party APIs to be available in a seamless manner alongside native Kubernetes resources.
5. Helm and Custom Resources:
- Helm can be used to deploy custom resources and their associated CRDs. You can package your CRDs and resources in Helm charts and deploy them in a Kubernetes cluster.

#### Example Use Cases for Custom Resources
1. Kubernetes Operators:
- Kubernetes Operators are a popular use case for CRDs. They extend Kubernetes to manage complex, stateful applications by managing the lifecycle of the application based on custom resources.
2. Infrastructure as Code:
- You can use CRDs to represent infrastructure resources, such as load balancers, databases, or queues, and manage them declaratively in Kubernetes.
3. CI/CD Pipelines:
- Custom resources can be used to represent various stages or tasks in a CI/CD pipeline and trigger specific actions like deployments, tests, or monitoring.
4. Custom Workloads:
- You can create custom resource types to represent specific workloads or resources (e.g., virtual machines, special databases) that are not native to Kubernetes.

### Kubernetes ConfigMap:
A ConfigMap is a Kubernetes API object used to store non-sensitive configuration data in key-value pairs. ConfigMaps are typically used for storing configuration files, command-line arguments, environment variables, or other settings that applications can consume.

#### Purpose:
- To separate configuration from application code, allowing the application to be more portable and easier to manage across different environments (development, staging, production).
- ConfigMaps provide a way to inject configuration into Pods at runtime.

#### Usage:
1. Storing Configuration Data: ConfigMaps store data that can be consumed by Pods, either as environment variables or by mounting the ConfigMap as files.
2. Injection into Pods: Configuration can be injected into Pods as environment variables or volume mounts (files).
3. Environment Variables: You can inject the data in a ConfigMap into a container as environment variables, which the application can read at runtime.
4. File Mounting: A ConfigMap can also be mounted as a file inside a container. Each key in the ConfigMap is represented as a file, with the content of the value as the file content.

#### Creating a ConfigMap:
1. From literal values:
```
kubectl create configmap my-config --from-literal=key1=value1 --from-literal=key2=value2
```
2. From a file:
```
kubectl create configmap my-config --from-file=config-file.txt
```
3. From a directory:
```
kubectl create configmap my-config --from-file=/path/to/directory
```
4. From a YAML file:
You can also define a ConfigMap using YAML. Example:
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  key1: value1
  key2: value2
```
Then apply it:
```
kubectl apply -f configmap.yaml
```
#### Using ConfigMap in Pods:
1. As environment variables:
```
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
spec:
  containers:
  - name: my-container
    image: nginx
    envFrom:
    - configMapRef:
        name: my-config
```
2. As a volume mount:
```
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
spec:
  containers:
  - name: my-container
    image: nginx
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config
  volumes:
  - name: config-volume
    configMap:
      name: my-config
```
#### Advantages of ConfigMap:
- Easy to manage configuration changes without needing to rebuild or redeploy your application.
- Supports versioning of configuration.
- Enables easy modification of environment-specific configurations.


### Kubernetes Secrets:
A Secret is similar to a ConfigMap, but it is specifically designed to store sensitive data such as passwords, OAuth tokens, SSH keys, or any other sensitive information. Secrets are encoded in base64 to avoid exposing plain text but are not encrypted by default.

#### Purpose:
- To store and manage sensitive information, such as passwords, access tokens, and private keys, securely.
- Secrets can be mounted into Pods as environment variables or volumes, or they can be accessed by applications to authenticate or connect to services.

#### Creating a Secret:
1. From literal values:
```
kubectl create secret generic my-secret --from-literal=password=myPassword123 --from-literal=token=myToken
```
2. From a file:
```
kubectl create secret generic my-secret --from-file=ssh-key=./ssh/id_rsa
```
3. From a directory:
```
kubectl create secret generic my-secret --from-file=/path/to/secret-files
```
4. From a YAML file:
You can define a Secret using YAML:
```
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  password: bXlQYXNzd29yZDEyMw==  # base64 encoded password
```
Then apply it:
```
kubectl apply -f secret.yaml
```
### Accessing Secrets in Pods:
1. As environment variables:
```
apiVersion: v1
kind: Pod
metadata:
  name: secret-example-pod
spec:
  containers:
  - name: my-container
    image: nginx
    env:
    - name: SECRET_PASSWORD
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: password
```
2. As a volume mount:
```
apiVersion: v1
kind: Pod
metadata:
  name: secret-example-pod
spec:
  containers:
  - name: my-container
    image: nginx
    volumeMounts:
    - name: secret-volume
      mountPath: /etc/secret
  volumes:
  - name: secret-volume
    secret:
      secretName: my-secret
```
#### Secret Types:
- Opaque (default): The data is arbitrary and not tied to any specific type.
- dockerconfigjson: Used to store Docker configuration, such as credentials for Docker registries.
- kubernetes.io/service-account-token: Used to store service account token data.
- kubernetes.io/basic-auth: Stores credentials for basic HTTP authentication.
- kubernetes.io/ssh-auth: Stores SSH private keys for authentication.
- kubernetes.io/tls: Stores TLS certificates and private keys.

#### Security Considerations:
- Base64 encoding is not encryption; it only makes the data unreadable without decoding. Base64 encoded data can be easily decoded back to its original format.
- Kubernetes Secrets can be encrypted at rest using features like KMS (Key Management Service) in cloud environments.
- By default, Secrets are stored in etcd, which should be secured and encrypted.

#### Advantages of Secrets:
- Secrets are better suited for sensitive data, with Kubernetes providing mechanisms to manage and control access to them.
- Secrets can be encoded, but you should also encrypt them to protect against potential leaks.
- Secrets can be accessed programmatically, and Kubernetes allows access control via RBAC to limit which Pods can access specific Secrets.


#### Comparison between ConfigMap and Secret
|Feature	      |ConfigMap	                             |Secret                                                 |
|--------------|---------------------------------------|-------------------------------------------------------|
|Purpose	      |Store non-sensitive configuration data |Store sensitive information (passwords, tokens, etc.)  |
|Data Encoding |Plain text	                            |Base64 encoded                                         |
|Use Case	     |Configuration for apps                 |Authentication, authorization, and sensitive data      |
|Security	     |No encryption	                         |Can be encrypted at rest (but not by default)          |
|Access Control|Through RBAC and environment variables |Through RBAC, environment variables, or volumes        |


### Kubernetes Monitoring
Kubernetes monitoring involves tracking the health and performance of the Kubernetes clusters, nodes, containers, and applications running inside the cluster. It helps in identifying issues, optimizing performance, ensuring high availability, and maintaining the overall stability of the system.

Monitoring Kubernetes effectively requires a combination of tools and techniques to monitor:
- Cluster health (nodes, control plane)
- Application performance (pods, containers, services)
- Resource usage (CPU, memory, disk, network)
- Logs and events (for troubleshooting)

#### Key Components of Kubernetes Monitoring
- Control Plane: The set of components responsible for the overall management of the cluster, such as the Kubernetes API server, scheduler, controller manager, etc.
- Nodes: The physical or virtual machines on which the workloads run.
- Pods and Containers: The smallest deployable units in Kubernetes.
- Cluster-wide Metrics: Metrics like resource usage, pod status, node conditions, etc.
- Application Metrics: Specific to the applications running in the cluster (e.g., request latency, error rates).
- Logs: Logs from Kubernetes components, application logs, and event logs.

#### Monitoring Metrics in Kubernetes
Kubernetes provides various types of metrics that can help you monitor the health of the system and the applications running within it:

a. Cluster Metrics:
- Node Metrics: CPU usage, memory usage, disk usage, and network traffic for each node.
- Pod Metrics: CPU and memory usage for individual pods.
- Cluster Utilization: Number of running pods, available resources, and pod resource requests/limits.

b. Application Metrics:
Request Latency: Time taken by the application to process a request.
- Error Rates: Number of errors encountered by the application.
- Request Count: Total number of requests or transactions processed by the app.
- Service Availability: Uptime and response time of the services deployed.

c. Health Metrics:
- Pod Readiness and Liveness: The health of pods, whether they are healthy (ready) or not.
- Container Restarts: Number of times a container has been restarted.

d. Cluster Health Metrics:
- Control Plane Health: API server status, etcd health, and scheduler availability.
- Node Status: Whether nodes are in a ready state or not.
- Pod and Container Status: Pod and container lifecycle status (running, pending, failed, etc.).

#### Popular Tools for Kubernetes Monitoring
a. Prometheus:
- Prometheus is one of the most widely used open-source tools for monitoring Kubernetes clusters.
- It collects metrics from Kubernetes components, nodes, and applications.
- Prometheus uses a pull-based model to scrape data from endpoints exposed by Kubernetes components, containers, and applications.
- Prometheus + Grafana is a popular combination to visualize metrics.

Key features of Prometheus:
- Metric scraping with a flexible query language (`PromQL`).
- Automatic discovery of Kubernetes targets (pods, nodes).
- Data storage and long-term retention.
- Alerting via Prometheus Alertmanager.

How to integrate Prometheus with Kubernetes:
- Install Prometheus using Helm or K8s manifests.
- Use the Prometheus Operator for easy setup and management.
- Set up ServiceMonitor to monitor specific services.

b. Grafana:
- Grafana is a visualization tool that integrates well with Prometheus.
- It allows you to create dashboards for monitoring Kubernetes metrics.
- Commonly used to visualize Prometheus metrics, but can also be used with other data sources.
- Pre-configured dashboards for Kubernetes monitoring are available in Grafana.

Setting up Grafana with Kubernetes:
- Install Grafana using Helm or manifests.
- Integrate Grafana with Prometheus as a data source.
- Use built-in Kubernetes dashboards or create custom dashboards.

c. Kubernetes Metrics Server:
- The Metrics Server is a lightweight aggregator of resource usage data in Kubernetes.
- It collects metrics like CPU and memory usage for nodes and pods and is used by other components like the Horizontal Pod Autoscaler (HPA).
- It does not store data but provides a way to get metrics for real-time queries.

How to install and use Metrics Server:
- Install via Helm or K8s manifests.
- Use `kubectl top` command to view resource usage.
- Metrics Server is essential for scaling and resource management.

d. Kube-State-Metrics:
- Kube-State-Metrics exposes metrics related to the state of Kubernetes resources (deployments, statefulsets, nodes, etc.).
- It provides more detailed metrics on the status of Kubernetes objects (e.g., the number of available replicas in a deployment).
- Often used in combination with Prometheus for more comprehensive cluster monitoring.

How to install and use Kube-State-Metrics:
- Install via Helm or manifests.
- Integrate with Prometheus for collection of resource state metrics.

e. Elastic Stack (ELK):
- The Elastic Stack (Elasticsearch, Logstash, Kibana) is commonly used for logging, but it can also be used for monitoring.
- Filebeat can be installed as a DaemonSet to collect logs from nodes and containers, which are then sent to Elasticsearch.
- Kibana is used to visualize logs and metrics collected by Elasticsearch.

f. Datadog:
- Datadog is a commercial monitoring solution that provides full-stack observability for Kubernetes.
- It can monitor the Kubernetes cluster, containers, and applications in real-time.
- It offers integration with other tools and cloud providers, giving a unified monitoring experience.

g. New Relic:
- New Relic provides comprehensive monitoring for Kubernetes, offering infrastructure monitoring, APM (Application Performance Monitoring), and real-time observability.
- It integrates seamlessly with Kubernetes and provides visual dashboards for monitoring.

#### Kubernetes Monitoring Strategies
a. Collecting Metrics:
- Use Prometheus to scrape metrics from your Kubernetes cluster.
- Ensure that the Kubernetes API server, nodes, pods, and services are exposed as endpoints that Prometheus can scrape.
- Consider using Prometheus exporters to collect specific metrics from services or infrastructure outside of Kubernetes.

b. Setting up Alerts:
- Use Prometheus Alertmanager to create alerts based on your metrics.
- Common alerting scenarios include:
 - High CPU or memory usage.
 - Pod restarts or container crashes.
 - Node down or unresponsive.
 - Application-specific errors or latency.

c. Visualizing Metrics:
- Grafana is the best choice for visualizing Prometheus data, providing intuitive dashboards.
- Use pre-configured dashboards or create custom ones that meet your operational requirements.
- Set up dashboards for Kubernetes-specific metrics (e.g., node health, pod status) as well as application-level metrics.

d. Logging and Troubleshooting:
- Use Centralized Logging systems like Elasticsearch or Fluentd to aggregate logs from all containers and Kubernetes components.
- Integrate Prometheus and Grafana with log aggregation systems for more comprehensive monitoring.
- Monitor logs for errors, warnings, and critical events.

e. Autoscaling and Resource Management:
- Use the Horizontal Pod Autoscaler (HPA) with metrics from the Metrics Server to scale applications based on CPU and memory usage.
- Set resource limits and requests for pods to ensure efficient resource allocation.
- Use the Vertical Pod Autoscaler (VPA) for automatic resource adjustment for containers.

f. Observability and Tracing:
- Implement Distributed Tracing (e.g., using Jaeger or OpenTelemetry) to trace requests across multiple services within the Kubernetes cluster.
- Distributed tracing helps to identify bottlenecks, latency issues, and performance problems in microservices architectures.

#### Best Practices for Kubernetes Monitoring
- Centralized Monitoring: Use tools like Prometheus and Grafana for centralized metrics collection and visualization.
- Alerting: Set up appropriate alerting for resource consumption (CPU, memory), application errors, and critical failures (e.g., nodes or pods crashing).
- Log Aggregation: Use Elasticsearch, Fluentd, or other logging tools to aggregate logs from containers, nodes, and Kubernetes components.
- Autoscaling: Configure HPA and VPA to automatically adjust resources as required.
- Security Monitoring: Monitor cluster access and ensure that proper RBAC permissions are set up for all components.
- Regular Health Checks: Use liveness and readiness probes to ensure that applications and pods are healthy.
- Capacity Planning: Continuously monitor resource usage to ensure that your cluster can handle growing workloads.

### Real time problems with Kubernetes (K8s) in a production environment

1. Resource Quota Limits
Resource quotas control the amount of CPU, memory, and other resources that can be used by pods within a namespace.

Real-Time Problems:
- Unexpected Pod Failures: Pods may be evicted or fail to schedule if they exceed the quota.
- Resource Starvation: High-priority pods might get starved of resources due to strict quotas set for other namespaces.
- Complexity in Scaling: Quotas can make horizontal scaling tricky because new pods might not get scheduled if the quota is exhausted.

Example:
You’ve set a quota of 8 CPUs for a namespace, but a spike in traffic requires more. Even if the nodes have capacity, new pods won’t start because the quota limits are hit.

Mitigation 
- Set realistic quotas based on usage patterns.
- Use monitoring tools (like Prometheus) to track resource usage.


2. Limits for Pods (CPU & Memory Requests/Limits)
Kubernetes allows setting resource requests (minimum) and limits (maximum) for CPU and memory per pod.

Real-Time Problems:
- CPU Throttling: If the CPU limit is too low, pods get throttled, causing performance degradation.
- Memory OOM Kills: If memory limits are set too tight, the pod may get killed when it exceeds the limit, even if the node has free memory.
- Inefficient Resource Utilization: Overly conservative limits can lead to underutilized cluster resources.

Example:
A pod is running a heavy computation task. You’ve set a CPU limit of 500m (0.5 CPU), but the workload needs 1 CPU. The pod keeps getting throttled, leading to slow performance.

Mitigation 
- Fine-tune CPU and memory requests/limits based on load testing.
- Use Horizontal Pod Autoscaler (HPA) for dynamic scaling.

3. Upgrades (Cluster & Application)
Upgrading Kubernetes versions, node OS, or applications.

Real-Time Problems:
- Downtime During Upgrades: If rolling updates aren’t configured properly, there could be service interruptions.
- API Compatibility Issues: Applications relying on deprecated APIs may fail after an upgrade.
- Stateful Set Challenges: Upgrading stateful applications can be tricky, especially when handling data persistence.

Example:
Upgrading the Kubernetes control plane from v1.24 to v1.25 causes a disruption because a custom resource definition (CRD) was deprecated in the new version, causing certain pods to crash.

Mitigation 
- Test upgrades in staging environments first.
- Use blue-green deployments or canary releases for apps.

4. OOM Killed (Out of Memory)
When a container uses more memory than its limit, the Linux OOM Killer terminates it to free up memory.

Real-Time Problems:
- Pod Crashes: The pod is terminated abruptly, causing potential data loss or service disruption.
- Unpredictable Failures: OOM kills can happen without clear warnings, making it hard to debug.
- Impact on Dependent Services: If a critical pod is killed, it may cascade failures to other services depending on it.

Example:
A pod with a 512Mi memory limit starts processing large datasets. It consumes 700Mi, triggers an OOM kill, and the service becomes unavailable until the pod restarts.

Mitigation 
- Analyze OOM kill logs (`kubectl describe pod <pod-name>`) to identify the issue.
- Adjust memory limits or optimize the application to handle peak loads better.

### EKS Cluster Upgrade Process
🔑 1. Prerequisites Before Upgrading EKS
 ✅ 1.1 Cluster Preparation
- Cordon Control Plane and Nodes:
Prevent new workloads from being scheduled during the upgrade.
```
kubectl cordon <node-name>
```
- Drain Nodes (Optional):
Safely evict pods before the upgrade.
```
kubectl drain <node-name> --ignore-daemonsets --delete-local-data
```
- Verify Cluster Status:
Ensure nodes and pods are healthy.
```
kubectl get nodes
kubectl get pods --all-namespaces
```
✅ 1.2 Review Cluster Configuration
- Node Group & Auto Scaling:
Ensure the node group is configured with the latest AMI and proper scaling policies.
- Kubelet Version Compatibility:
Check if kubelet versions are compatible with the EKS control plane.
```
kubectl get nodes -o wide
```
✅ 1.3 Lower Environment Testing (Staging/Dev)
- Test in Lower Environments:
Always perform the upgrade in a staging or development environment before production.
- Backup Configurations:
Backup cluster data, manifests, and critical configurations.

✅ 1.4 Cluster Auto-Scaler Setup
- Ensure Auto-Scaler Is Configured:
Verify that Cluster Autoscaler is installed and configured correctly.
```
kubectl get deployment -n kube-system cluster-autoscaler
```
- Adjust Auto-Scaler for Upgrade:
Make sure the auto-scaler is not aggressively terminating nodes during the upgrade.

✅ 1.5 Networking Requirements
- 5 Available IP Subnets:
Ensure at least 5 available IP subnets for control plane, nodes, and load balancers.
- Security Group Rules:
Confirm security groups allow traffic for control plane and node communication.

🔄 2. EKS Upgrade Process
2.1 Upgrade the Control Plane
Using AWS CLI:
```
aws eks update-cluster-version \
  --region <region> \
  --name <cluster-name> \
  --kubernetes-version <new-version>
```
Using AWS Console:
1. Go to the EKS console.
2. Select your cluster → Update.
3. Choose the new Kubernetes version.

2.2 Upgrade Node Groups
Using eksctl:
```
eksctl upgrade nodegroup \
  --name <node-group-name> \
  --cluster <cluster-name> \
  --region <region>
```
AWS Console Steps:
1. Go to EKS → Select cluster → Compute tab.
2. Choose node group → Update now.

2.3 Upgrade Add-ons
Using eksctl:
```
eksctl utils update-kube-proxy \
  --cluster <cluster-name> \
  --region <region>

eksctl utils update-aws-node \
  --cluster <cluster-name> \
  --region <region>

eksctl utils update-coredns \
  --cluster <cluster-name> \
  --region <region>
```
Console Steps:
1. Navigate to Add-ons in your cluster.
2. Select each add-on (e.g., `kube-proxy`, `aws-node`, `coredns`) → Update now.

2.4 Upgrade Cluster Autoscaler (If Applicable)
1. Verify Cluster Autoscaler Deployment:
```
kubectl -n kube-system get deployment cluster-autoscaler
```
2. Update Image Version (if needed):
```
kubectl -n kube-system set image deployment/cluster-autoscaler \
  cluster-autoscaler=registry.k8s.io/autoscaling/cluster-autoscaler:v1.30.0
```
🔍 3. Post-Upgrade Validation
3.1 Check Node & Pod Status:
```
kubectl get nodes
kubectl get pods --all-namespaces
```
3.2 Validate Add-ons:
```
kubectl describe deployment -n kube-system aws-node
kubectl describe deployment -n kube-system coredns
kubectl describe deployment -n kube-system kube-proxy
```
3.3 Verify Cluster Autoscaler:
```
kubectl -n kube-system logs deployment/cluster-autoscaler
```
🔒 4. Rollback Plan (If Needed)
Rollback Control Plane:
```
aws eks update-cluster-version \
  --region <region> \
  --name <cluster-name> \
  --kubernetes-version <previous-version>
```
Rollback Node Group:
```
eksctl upgrade nodegroup \
  --name <node-group-name> \
  --cluster <cluster-name> \
  --region <region> \
  --version <previous-version>
```
⚡ 5. Best Practices for EKS Upgrades
- Always test in lower environments first.
- Monitor cluster performance during the upgrade.
- Ensure sufficient IPs and network capacity.
- Backup critical data before upgrades.
- Keep AWS CLI, eksctl, and kubectl updated.


