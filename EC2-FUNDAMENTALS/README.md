# EC2 Fundamentals

- EC2 stands for Elastic Compute Cloud.
- It is one of the most popular services provided by AWS.
- EC2 allows users to rent virtual servers to run applications.
- EC2 is Infrastructure as a Service (IaaS).
- Users can choose different instance types based on their needs (CPU, memory, storage).
- It mainly consists of:
  - Renting virtual servers (instances).
  - Storing data on virtual hard drives (EBS).
  - Distributing traffic using load balancers (ELB).
  - Scaling resources automatically (Auto Scaling).
- Knowing EC2 is essential to understand how the cloud works.

### EC2 Sizing & Configuration Options

- When selecting an EC2 instance, consider:
  - Operating Systems: Linux, Windows, etc.
  - How much computer power (CPU) you need.
  - How much memory (RAM) you need.
  - Storage options: SSD, HDD, etc.
    - Network attached storage (EBS).
    - Hardware/instance storage (local to the instance).
  - Network performance: bandwidth and latency.
  - Firewall settings (security groups).
  - Bootstrap scripts to set up the instance on launch.

### EC2 User Data

- It is possible to bootstrap (automatically configure) our EC2 instances at launch using an EC2 feature called "User Data".
- User Data scripts run only during the first boot cycle when the instance is launched.
- Common use cases for User Data include:
  - Installing software packages.
  - Applying operating system updates.
  - Configuring application settings.
  - Setting up monitoring agents.
- User Data scripts can be written in various scripting languages, such as Bash for Linux instances or PowerShell for Windows instances.
- To use User Data, you can provide the script when launching the instance via the AWS Management Console, CLI, or SDKs.

### EC2 Instance Types

- EC2 offers various instance types optimized for different use cases:

  - General Purpose: Balanced CPU, memory, and networking (e.g., t3, m5).
  - Compute Optimized: High CPU performance (e.g., c5).
  - Memory Optimized: High memory capacity (e.g., r5).
  - Storage Optimized: High I/O performance for storage-intensive applications (e.g., i3).
  - GPU Instances: For graphics-intensive applications and machine learning (e.g., p3, g4).

- AWS has the following naming convention for EC2 instance types:
  - A letter indicating the instance family (e.g., t, m, c, r, i, p).
  - A number indicating the generation (e.g., 3, 4, 5).
  - An optional suffix indicating specific features (e.g., .large, .xlarge).
- Example: m5.2xlarge is a General Purpose instance of the 5th generation with 2xlarge size.

### EC2 Instance Types - General Purpose

- General Purpose instances provide a balance of compute, memory, and networking resources.
- Suitable for a diverse range of applications from small to medium-sized databases, web servers, and development environments.

### EC2 Instance Types - Compute Optimized

- Compute Optimized instances are designed for compute-intensive workloads.
- Ideal for applications that require high CPU performance, such as batch processing, high-performance web servers, and scientific modeling.
  - Media transcoding
  - High-performance web servers
  - Scientific modeling
  - Dedicated gaming servers
  - Machine learning inference

### EC2 Instance Types - Memory Optimized

- Memory Optimized instances are designed for memory-intensive applications.
- Suitable for high-performance databases, in-memory caches, and real-time big data analytics.
  - High-performance databases
  - In-memory caches (e.g., Redis, Memcached)
  - Real-time big data analytics
  - SAP HANA
  - Apache Spark

### EC2 Instance Types - Storage Optimized

- Storage Optimized instances are designed for workloads that require high, sequential read and write access to large datasets on local storage.
- Ideal for applications such as NoSQL databases, data warehousing, and distributed file systems.
  - NoSQL databases (e.g., Cassandra, MongoDB)
  - Data warehousing (e.g., Amazon Redshift)
  - Distributed file systems (e.g., Hadoop HDFS)
  - Log processing applications
  - High-frequency online transaction processing (OLTP) systems

## Security Groups & Classic Ports

### Intro to Security Groups

- Security groups are a fundamental component of network security in AWS.
- Security groups act as virtual firewalls for your EC2 instances to control inbound and outbound traffic.
- Security groups only allow "allow" rules; there are no "deny" rules.
- Security groups rules can reference IP addresses or other security groups.
- By default, a security group denies all inbound traffic and allows all outbound traffic.

### Security Groups - Deeper Dive

- Security groups are acting as a firewall at the instance level, controlling both inbound and outbound traffic.
- They regulate:

  - Access to ports
  - Authorized IP ranges (IPv4 and IPv6)
  - Control inbound network (from other sources to the instance)
  - Control outbound network (from the instance to other destinations)

- Security groups are stateful, meaning if you allow an incoming request from an IP, the response is automatically allowed regardless of outbound rules.
- You can assign multiple security groups to an instance.
- Changes to security group rules are applied immediately.

### Security Groups - Good To Know

- Can be attached to multiple instances.
- They are locked down to a region or VPC combination (cannot span regions or VPCs).
- Lives "outside" the instance (not installed on the instance) -- if traffic is blocked, it never reaches the instance.
- **It is good to maintain one separate security group for SSH/RDP access** to make management easier.
- If your application is not accessible (timeout), check security group rules first! It mostly is a security group issue.
- If your application is refusing connection (immediate error), it is mostly an application issue.
- All inbound traffic is blocked by default.
- All outbound traffic is allowed by default.

### Commonly Used Ports

| Port | Protocol | Service               | Description             |
| ---- | -------- | --------------------- | ----------------------- | -------------------- |
| 22   | TCP      | SSH (Linux instances) | Secure Shell for Linux  |
| 21   | TCP      | FTP                   | File Transfer Protocol  |
| 22   |          | TCP                   | SFTP                    | Secure File Transfer |
| 80   | TCP      | HTTP                  | Web traffic             |
| 443  | TCP      | HTTPS                 | Secure web traffic      |
| 3389 | TCP      | RDP                   | Remote Desktop Protocol |

### EC2 Instance Roles (IAM Roles for EC2)

- EC2 Instance Roles are a way to securely provide permissions to your EC2 instances without using long-term credentials.
- An instance role is an IAM role that you can attach to an EC2 instance.
- When an instance role is attached to an EC2 instance, the instance can obtain temporary security credentials from the instance metadata service.
- This allows applications running on the instance to access AWS services securely.
- Benefits of using instance roles include:
  - Enhanced security by avoiding hard-coded credentials.
  - Simplified credential management.
  - Automatic rotation of temporary credentials.
- To create and use an instance role:
  - Create an IAM role with the necessary permissions.
  - Attach the role to your EC2 instance during launch or to an existing instance.

## EC2 Instances Purchasing Options

So far, we have been using **On-Demand Instances**.

On-Demand instances let you pay for compute capacity by the hour or second with no long-term commitments.

- Great for short-term, spiky, or unpredictable workloads.

There are other purchasing options available as well:

- **Reserved Instances**:

  - 1-year or 3-year term.
  - Great for long-term, steady-state workloads.
  - Significant cost savings compared to On-Demand.
  - **Convertible Reserved Instances** allow you to change the instance type during the term.

- **Savings Plans**:

  - 1-year or 3-year term.
  - This is a more modern alternative to **Reserved Instances**.
  - Commit to a consistent amount of usage (measured in $/hour) for 1 or 3 years.
  - Flexible across instance types, regions, and operating systems.

- **Spot Instances**:

  - Purchase unused EC2 capacity at a significant discount (up to 90% off On-Demand prices).
  - Great for fault-tolerant and flexible applications.
  - Instances can be interrupted by AWS with a 2-minute warning when the capacity is needed elsewhere.

- **Dedicated Hosts**:

  - Physical servers dedicated to your use.
  - Useful for meeting compliance requirements and licensing needs.

- **Dedicated Instances**:

  - Run in a VPC on hardware dedicated to a single customer.
  - Do not share hardware with instances from other accounts.

- **Capacity Reservations**:
  - Reserve capacity for your EC2 instances in a specific Availability Zone for any duration.
  - Ensures that you have access to EC2 capacity when you need it.

### EC2 On-Demand Instances

On-Demand Instances let you pay for compute capacity by the hour or second with no long-term commitments.

- You pay for what you use.
  - Linux or Windows - billed per second, with a minimum of 60 seconds.
  - All other OS types - billed per hour.
- Has the highest cost compared to other purchasing options but no upfront payment or long-term commitment is required.
- Recommended for:
  - Short-term, spiky, or unpredictable workloads that cannot be interrupted.
  - Applications being developed or tested on EC2 for the first time.

### EC2 Reserved Instances

Reserved Instances provide you with a significant discount (up to 75%) compared to On-Demand instance pricing (% discount changes over time).

- You reserve a specific instance type in a specific region for a 1-year or 3-year term.
- Reservation period options:
  - 1-year term (lower discount).
  - 3-year term (higher discount).
- Payment options:
  - All Upfront (highest discount).
  - Partial Upfront (moderate discount).
  - No Upfront (lowest discount).
- Reserved Instance's scope can be:
  - Regional (applies to any instance of the specified type in the region).
  - Zonal (applies to a specific Availability Zone, providing capacity reservation).
- Recommended for:
  - Steady-state workloads with predictable usage.
  - Example: Web servers, databases, and other applications that run continuously.
- You can buy or sell Reserved Instances on the AWS Reserved Instance Marketplace.

There is also another type of Reserved Instances called **Convertible Reserved Instances**.

Convertible Reserved Instances allow you to change the instance type, operating system, or tenancy during the term.

- Up to 54% discount compared to On-Demand pricing.
- Recommended for:
  - Workloads that may change over time but still require long-term commitment.

### EC2 Savings Plans

Savings Plans offer significant cost savings (up to 72%) compared to On-Demand pricing in exchange for a commitment to a consistent amount of usage (measured in $/hour) for a 1-year or 3-year term.

- With Savings Plans, you commit to a specific dollar amount per hour for a 1-year or 3-year term ($10/hour for 3 years = $262,800 total).
- Usage beyond your committed amount is billed at On-Demand rates.
- Instances are locked to specific instance families within a region (e.g., m5 in us-east-1).
- Flexible across instance sizes, operating systems, and tenancies (host, dedicated, default) within the chosen instance family.
- Recommended for:
  - Users who want cost savings but need flexibility in instance types and sizes.

### EC2 Spot Instances

Spot Instances allow you to take advantage of unused EC2 capacity at a significant discount (up to 90% off On-Demand prices).

- Spot Instances can be interrupted by AWS with a 2-minute warning when the capacity is needed elsewhere.
- This is the most cost-effective option for running EC2 instances.
- Recommended for:
  - Fault-tolerant and flexible applications that can handle interruptions.
  - Example: Big data analysis, containerized workloads, CI/CD, web crawling, and batch processing.

### EC2 Dedicated Hosts

Dedicated Hosts are physical servers dedicated to your use.

- Useful for meeting compliance requirements and licensing needs.
- You have full control over the placement of instances on the host.
- You can use your existing server-bound software licenses (e.g., Windows Server, SQL Server, SUSE Linux).
- Purchasing options:
  - On-Demand: Pay for Dedicated Hosts by the hour with no long-term commitments.
  - Reserved: Reserve Dedicated Hosts for a 1-year or 3-year term with significant cost savings.
- This is the most expensive option for running EC2 instances.
- Recommended for:
  - Workloads that require dedicated physical servers for compliance or licensing reasons.
  - Example: Regulatory compliance, software licensing requirements.

### EC2 Dedicated Instances

Dedicated Instances run in a VPC on hardware dedicated to a single customer.

- Instances run on hardware that is dedicated to you, but you do not have control over the physical host.
- You may share the underlying hardware with other instances from your account.
- No control over instance placement on the host.
- Recommended for:
  - Workloads that require dedicated hardware but do not need the control provided by Dedicated Hosts.
  - Example: Applications with specific compliance requirements.

### EC2 Capacity Reservations

Capacity Reservations enable you to reserve capacity for your EC2 instances in a specific Availability Zone for any duration.

- You reserve On-Demand instances capacity in a specific Availability Zone for as long as you need it.
- You always have access to the capacity when you need it.
- No time commitment is required and no billing discounts are applied.
- Combine with Regional Reserved Instances or Savings Plans to reduce costs.
- You are charged for the capacity you reserve, regardless of whether you use it.
- Recommended for:
  - Workloads that require guaranteed access to EC2 capacity in a specific Availability Zone.
  - Example: Applications with predictable traffic patterns that need to ensure capacity availability.

### Which Purchasing Option Is Right for You?

Here are some analogies to help you understand the different EC2 purchasing options:

- **On-Demand Instances**: Like renting a car for a day. You pay for what you use without any long-term commitment.
- **Reserved Instances**: Like leasing a car for a year. You commit to using it for a long period and get a discount.
- **Savings Plans**: Like subscribing to a car-sharing service. You commit to a certain amount of usage and get flexibility within that commitment.
- **Spot Instances**: Like booking a last-minute hotel room at a discount. You get a great deal but may have to leave if the room is needed by someone else.
- **Dedicated Hosts**: Like owning a car. You have full control and can use it as you see fit, but it comes with higher costs.
- **Dedicated Instances**: Like renting a private car. You get dedicated use without the full control of ownership.
- **Capacity Reservations**: Like reserving a parking spot. You ensure you have a place when you need it, regardless of whether you use it or not.
