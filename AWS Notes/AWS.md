<p align="center">
  <img src="Images/AWS LOGO.png" alt="Logo" width="80"/>
</p>

### ☁️ Cloud Computing
- Cloud computing is the delivery of computing services—servers, storage, databases, networking, software, analytics, and intelligence—over the Internet (**the cloud**) to offer faster innovation, flexible resources, and economies of scale.

### 📦 Real-Life Analogy:
Like renting an apartment instead of buying a house. You use what you need and pay as you go.

### 🧠 Key Characteristics
1. On-Demand Self-Service – Users can provision computing resources automatically.
2. Broad Network Access – Services are accessible from anywhere via the internet.
3. Resource Pooling – Resources (storage, CPU, memory) are pooled and shared among multiple customers.
4. Rapid Elasticity – Resources can scale up/down automatically depending on demand.
5. Measured Service – Usage is monitored, controlled, and billed (like utilities).

### ✅ Benefits of Cloud Computing
- Cost-Effective – No upfront hardware costs.
- Scalable – Easily increase or decrease resources.
- Reliable – Backups, disaster recovery, data replication.
- Global Access – Access services anytime, from anywhere.
- Maintenance-Free – Handled by providers.

#### 🔹Types of Cloud Computing
☁ 1. Public Cloud
- Owned and operated by third-party providers.
- Example: AWS, Microsoft Azure, Google Cloud.
  
🏠 2. Private Cloud
- Exclusive to one organization.
- Higher control and security.

🌐 3. Hybrid Cloud
- Combination of public and private clouds.
- Balance of flexibility and security.


#### 🔹Cloud Service Models
🧱 1. IaaS (Infrastructure as a Service)
- You rent infrastructure like virtual machines, networks, storage.
- Example: AWS EC2, Azure Virtual Machines

🧰 2. PaaS (Platform as a Service)
- You get an environment to develop, test, and deploy software.
- Example: Google App Engine, Heroku

💻 3. SaaS (Software as a Service)
- Ready-to-use applications delivered via the internet.
- Example: Gmail, Microsoft 365, Dropbox

#### 🔹Components of Cloud Computing
1. Compute – Virtual machines, containers, serverless computing.
2. Storage – Object storage (S3), Block storage, File storage.
3. Database – Managed databases (SQL/NoSQL).
4. Networking – Load balancers, Virtual Private Cloud (VPC).
5. Security – Firewalls, encryption, identity & access management.
6. Monitoring & Logging – Track usage, performance, alerts.

### 🔹Popular Cloud Providers
|Provider	                  |Key Services                               |
|---------------------------|-------------------------------------------|
|AWS (Amazon Web Services)	|EC2, S3, Lambda, RDS                       |
|Microsoft Azure            |Azure VMs, Blob Storage, Azure Functions   |
|Google Cloud Platform (GCP)|Compute Engine, Cloud Storage, BigQuery    |
|IBM Cloud	                |Watson AI, IBM VPC                         |
|Oracle Cloud	              |Autonomous Database, OCI                   |

### 🔹Core Concepts
-  Virtualization - Allows multiple virtual machines to run on a single physical machine.
-  Containerization - Lightweight, portable units (e.g., Docker) to run applications.
-  Serverless Computing - Run code without managing servers (e.g., AWS Lambda).
-  Auto-Scaling - Automatically increase/decrease resources based on traffic.

### 🔹Security in Cloud
- 🔐 Identity & Access Management (IAM) – Controls who can access what.
- 🔐 Encryption – Protects data at rest and in transit.
- 🔐 Compliance – GDPR, HIPAA, ISO, etc.
- 🔐 Firewalls & Network ACLs – Control traffic flow.

### 🔹Use Cases of Cloud Computing
- Hosting websites & applications
- Data analytics & machine learning
- File storage & backup
- Development & testing environments
- Streaming services (e.g., Netflix runs on AWS)
- IoT device data management

## 🌍 AWS Global Infrastructure
- AWS global infrastructure is the foundation that enables cloud services to be delivered securely, reliably, and with low latency. It’s made up of:
1. **Regions**
2. **Availability Zones (AZs)**
3. **Edge Locations**
4. **Local Zones**
5. **Wavelength Zones**
6. **Outposts**

**🌐 1. AWS Regions**
- A Region is a geographical area with multiple, physically separated, and isolated Availability Zones.

**📌 Key Points:**
- Each region is a separate geographical area (e.g., `us-east-1` = N. Virginia).
- Regions are completely isolated from each other to ensure fault tolerance and stability.
- Users choose regions based on data residency, latency, and compliance needs.

**🧠 Examples:**
- `us-east-1` → N. Virginia
- `us-west-2` → Oregon
- `eu-west-1` → Ireland
- `ap-south-1` → Mumbai

**🏢 2. Availability Zones (AZs)**
- An Availability Zone is one or more data centers within a region, equipped with independent power, cooling, and networking, connected via low-latency links.

**📌 Key Points:**
- Each Region has **2–6 AZs.**
- AZs offer **fault isolation**, but **interconnected** with other AZs in the same region.
- Best practice: Deploy applications across multiple AZs for high availability and fault tolerance.

**📦 3. Edge Locations**
- Edge Locations are data centers that AWS uses to deliver content via services like **Amazon CloudFront** (CDN), **AWS Global Accelerator**, and **Route 53**.

**📌 Key Points:**
- Located closer to end users for low-latency delivery.
- Used for caching, DNS, and DDoS protection.
- Thousands of edge locations globally.

**📍 4. Local Zones**
- AWS Local Zones bring AWS services closer to **large metropolitan areas**, reducing latency for applications that require real-time responses.

**📌 Key Points:**
- Extend your VPC to Local Zones.
- Useful for applications like gaming, media streaming, AR/VR, machine learning inference, etc.


**📡 5. AWS Wavelength Zones**
- Wavelength Zones bring AWS services to the edge of **5G networks**, allowing developers to build ultra-low-latency applications for **mobile and connected devices.**

**📌 Use Cases:**
- Real-time gaming
- Live video streaming
- Augmented Reality/Virtual Reality (AR/VR)
- Autonomous vehicles

**🏭 6. AWS Outposts**
- AWS Outposts is a **fully managed service** that extends AWS infrastructure, services, APIs, and tools to on-premises environments.

**📌 Key Points:**
- Offers a hybrid cloud model.
- Use cases include low-latency workloads, data residency requirements, local data processing.

**🛡️ Security in Global Infrastructure**
- **End-to-end encryption** between regions and AZs.
- **Physical security** with multiple layers of access control.
- **Resilient design:** Redundancy, fault isolation, and disaster recovery built-in.

**🧮 Summary Table**

|Component           |Description                         |Key Use Case                        |
|--------------------|------------------------------------|------------------------------------|
|Region              |Geographic area with multiple AZs   |Data residency, latency             |
|Availability Zone	 |Isolated data centers in a region   |High availability, fault tolerance  |
|Edge Location	     |CDN endpoints for caching           |Fast content delivery               |
|Local Zone	         |AWS infra in metro areas	          |Real-time apps with low latency     |
|Wavelength Zone	   |Edge of 5G network for mobile apps  |Ultra-low latency on mobile         |
|Outposts	           |AWS on-premise extension	          |Hybrid cloud, local data processing |

✅ Best Practices
- Choose region based on **compliance, latency, and price.**
- Design apps using **multi-AZ deployments** for HA.
- Use **CloudFront** + **Edge Locations** for global content delivery.
- Extend to **Local Zones** or **Outposts** for low-latency edge computing.

### 🛡️ AWS IAM
#### 1. Introduction to IAM
- IAM (Identity and Access Management) is a web service that helps securely control access to AWS resources.
- IAM enables authentication (who you are) and authorization (what you can do).
- It is global—not region-specific.

#### 2. IAM Identities
➤ IAM Users
- Represents a single person or service.
- Assigned credentials:
  - Username/password for AWS Console
  - Access keys for CLI/SDK/API
- Can be assigned permissions via policies.

➤ IAM Groups
- Collection of IAM users.
- Policies attached to groups are inherited by users.
- Best practice: Assign permissions to groups, not users.

➤ IAM Roles
- Temporary credentials.
- Used for:
  - AWS services (e.g., EC2, Lambda)
  - Cross-account access
- Federated identities (SSO, external IdPs)
- Assume roles using AWS STS.

➤ IAM Policies
- JSON documents that define permissions.
- Can be:
  - AWS-managed
  - Customer-managed
  - Inline (directly embedded)

#### 3. IAM Policies
➤ Structure of a Policy
```
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow" | "Deny",
    "Action": "s3:PutObject",
    "Resource": "arn:aws:s3:::my-bucket/*",
    "Condition": {
      "StringEquals": {
        "aws:username": "john"
      }
    }
  }]
}
```
- Version: Policy language version
- Statement: One or more individual permissions
- Effect: `Allow` or `Deny`
- Action: What actions are allowed (e.g., `s3:ListBucket`)
- Resource: Which resource the action applies to

➤ Types of Policies
- Identity-based policies – attached to users, groups, roles
- Resource-based policies – attached to resources like S3, Lambda
- Permissions boundaries – maximum permission limit
- Service control policies (SCPs) – for AWS Organizations
- Session policies – passed when assuming a role

➤ Evaluation Logic
- Deny always overrides Allow.
- If there’s no explicit Allow, access is implicitly denied.
- Conditions further refine access control.

#### 4. IAM Best Practices
- Use MFA for the root account and all users.
- Never use root account for daily tasks.
- Grant least privilege.
- Regularly rotate credentials.
- Use roles instead of long-term credentials (especially for EC2).
- Monitor with CloudTrail and Config.

#### 5. IAM Roles and Use Cases
➤ Use Cases
- EC2 instance accessing S3
- Lambda writing logs to CloudWatch
- Cross-account access (Account A assumes a role in Account B)
- Third-party applications (temporary credentials via STS)

➤ Role Trust Policy (Who can assume the role)
```
{
  "Effect": "Allow",
  "Principal": {
    "Service": "ec2.amazonaws.com"
  },
  "Action": "sts:AssumeRole"
}
```
#### 6. Permissions Boundaries
- Advanced feature to limit the maximum permissions an identity can have.
- Does not grant permissions, only restricts them.
- Useful for delegating permission management safely.

#### 7. IAM Access Analyzer
- Helps identify resources shared with external accounts or organizations.
- Generates findings if a policy allows unintended access.
- Good for auditing and compliance.
- Works with:
  - S3
  - IAM roles and policies
  - Lambda
  - KMS
  - SQS, SNS

#### 8. IAM Policy Conditions
➤ Common Condition Keys
- `aws:CurrentTime`
- `aws:SourceIp`
- `aws:username`
- `aws:MultiFactorAuthPresent`
- `s3:prefix`, `s3:x-amz-server-side-encryption`

➤ Example: Restrict access by IP
```
"Condition": {
  "IpAddress": {
    "aws:SourceIp": "203.0.113.0/24"
  }
}
```
#### 9. IAM Policy Simulator
- Tool to test and troubleshoot IAM policies.
- Simulates API calls to verify permissions.
- Can test:
  - User permissions
  - Role assumptions
  - Resource policies

#### 10. Logging and Monitoring IAM
➤ AWS CloudTrail
- Logs all IAM and STS API activity.
- Useful for auditing and compliance.

➤ AWS Config
- Tracks changes to IAM resources.
- Can create rules (e.g., check if MFA is enabled).

➤ AWS CloudWatch
- Set up alarms for suspicious IAM activity.
- Monitor login attempts, unauthorized access, etc.

#### 11. IAM and AWS Organizations
➤ Service Control Policies (SCPs)
- Set permission boundaries at the account or organizational unit (OU) level.
- Can’t grant permissions—only restrict.
- Applied in addition to IAM policies.

➤ Use Cases
- Prevent use of specific services (e.g., deny EC2 in dev accounts)
- Force tagging requirements
- Centralize access control



