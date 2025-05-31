# EC2: Fundamentals

## EC2 Basics

Amazon EC2 (Elastic Compute Cloud) is a web service that provides resizable compute capacity in the cloud. It allows users to run virtual servers, known as instances, on-demand.

- EC2 is one of the most popular services in AWS.
- EC2 = Elastic Compute Cloud = Infrastructure as a Service (IaaS).
- It allows users to launch and manage virtual machines in the cloud.
- It provides a wide range of instance types optimized for different use cases.
- It mainly consists in the capability of:
  - Renting virtual machines (instances) in the cloud (EC2).
  - Storing data in the cloud (EBS).
  - Distributing loads across multiple instances (ELB).
  - Scaling the services using an auto-scaling group (ASG).

Knowing how to use EC2 is essential for anyone working with AWS, as it forms the backbone of many applications and services.

### EC2 Sizing and Configuration Options

EC2 instances come in various sizes and configurations to suit different workloads.

- Instance types are categorized into families based on their capabilities, such as compute-optimized, memory-optimized, storage-optimized, and GPU instances.
- Each instance type has different CPU, memory, storage, and networking capabilities.
- Users can choose the instance type that best fits their application's requirements.

EC2 instances can be launched with different configurations, including:

- Various operating systems, including Linux distributions, Windows, and macOS.
- How much compute power and cores you need (CPU).
- How much memory you need (RAM).
- How much storage you need (EBS volumes):
  - Network-attached storage (EBS and EFS).
  - Hardware-attached storage (EC2 Instance Store).
- How much network bandwidth you need:
  - Network card, speed of the network card, public IP, private IP, etc.
- Firewall rules (Security Groups).
- Bootstrapping scripts (User Data) to configure the instance at launch time.

### EC2 User Data

User Data is a feature that allows you to run scripts or commands on an EC2 instance at launch time. This is useful for automating the setup and configuration of instances.

- It is possible to bootstrap our instances using an EC2 User Data script.
- Bootstrapping means launching commands or scripts automatically when the instance is launched. The script is only executed once at the first boot of the instance.
- User Data scripts can be written in shell script, PowerShell, or cloud-init format.
- They can be used to install software, configure settings, or perform any other initialization tasks.
- EC2 User Data is used to automate boot tasks such as:
  - Installing updates
  - Installing software
  - Downloading files
  - Anything you can think of
  - The more complex the task, the more your instance will take to boot up
- The EC2 User Data script is executed as the root user, so it has full permissions to perform any actions on the instance.

### EC2 Instance Types

EC2 instances are categorized into different families based on their capabilities and use cases. Each family has various instance types optimized for specific workloads.

- **General Purpose**: Balanced compute, memory, and networking resources. Suitable for a wide range of applications.
  - Example: `t3`, `t3a`, `t4g`, `m5`, `m5a`, `m5n`, `m6g`, etc.
- **Compute Optimized**: High-performance processors for compute-intensive tasks. Ideal for high-performance web servers, batch processing, and gaming.
  - Example: `c5`, `c5a`, `c5n`, `c6g`, etc.
- **Memory Optimized**: High memory-to-CPU ratio for memory-intensive applications. Suitable for databases, in-memory caches, and real-time big data analytics.
  - Example: `r5`, `r5a`, `r5n`, `r6g`, etc.
- **Storage Optimized**: High disk throughput and IOPS for data-intensive applications. Ideal for NoSQL databases, data warehousing, and log processing.
- **Accelerated Computing**: Instances with hardware accelerators like GPUs for machine learning, graphics rendering, and high-performance computing.
  - Example: `p3`, `p4`, `g4`, `g5`, etc.
- **Bare Metal**: Provides direct access to the underlying hardware for applications that require low-level access or specific hardware configurations.
- **High Memory**: Instances with large amounts of memory for in-memory databases and high-performance computing applications.
  - Example: `u-6tb1.metal`, `u-9tb1.metal`, etc.
- **Mac Instances**: Designed for macOS workloads, allowing developers to run macOS applications in the cloud.
- **Graviton Instances**: Powered by AWS Graviton processors, these instances offer cost-effective performance for a variety of workloads.
  - Example: `t4g`, `m6g`, `c6g`, etc.

### EC2 Instance Types Examples

| Instance Type | vCPUs | Memory (GiB) | Storage Type | Network Performance | EBS Bandwidth | Use Case                                     |
| ------------- | ----- | ------------ | ------------ | ------------------- | ------------- | -------------------------------------------- |
| t2.micro      | 1     | 1            | EBS-Only     | Low to Moderate     | 100 Mbps      | Low traffic web servers, small databases     |
| t2.xlarge     | 4     | 16           | EBS-Only     | Moderate            | 300 Mbps      | Medium traffic web servers, small apps       |
| c5d.4xlarge   | 16    | 32           | EBS + NVMe   | Up to 10 Gbps       | 4,750 Mbps    | High-performance computing, batch processing |
| r5.16xlarge   | 64    | 512          | EBS-Only     | Up to 20 Gbps       | 13,600 Mbps   | In-memory databases, data analytics          |
| m5.8xlarge    | 32    | 128          | EBS-Only     | Up to 10 Gbps       | 6,800 Mbps    | General-purpose applications, web servers    |

The idea of this is that you can choose the instance type that best fits your application's requirements based on the CPU, memory, storage, and networking capabilities.

## EC2 Instance Types - Overview

You can use different types of EC2 instances that are optimized for different use cases.

You can check the [AWS EC2 Instance Types documentation](https://aws.amazon.com/ec2/instance-types/) for the latest information on instance types and their specifications.

AWS has the following naming convention for EC2 instance types:

- The first letter indicates the instance family/instance class (e.g., `t` for General Purpose, `c` for Compute Optimized, `r` for Memory Optimized)
- The second letter indicates the generation of the instance type (e.g., `3` for the third generation, `4` for the fourth generation)
- The number indicates the size of the instance (e.g., `micro`, `small`, `medium`, `large`, `xlarge`, `2xlarge`, etc.). The larger the number, the more resources the instance has.

For example, `t3.micro` is a General Purpose instance of the third generation with a small size.

### EC2 Instance Types - General Purpose

General Purpose instances provide a balance of compute, memory, and networking resources, making them suitable for a variety of workloads. They are ideal for applications that require a moderate level of CPU and memory performance.

- Great for a diversity of workloads, such as web servers, small databases, and development environments.
- Good balance between:
  - Compute (CPU)
  - Memory (RAM)
  - Networking (Network Bandwidth)

Some examples of General Purpose instance types include:

- `t3.micro`
- `t3a.micro`
- `t4g.micro`
- `m5.large`
- `m5a.large`
- `m5n.large`
- `m6g.large`

### EC2 Instance Types - Compute Optimized

Compute Optimized instances are designed for compute-intensive workloads that require high-performance processors. They are ideal for applications that require high CPU performance, such as high-performance web servers, batch processing, and gaming.

- Great for compute-intensive tasks that require high-performance processors
- Tasks such as:
  - High-performance web servers
  - Batch processing workloads
  - Media transcoding
  - High-performance computing (HPC)
  - Scientific modeling and machine learning
  - Dedicated gaming servers

Some examples of Compute Optimized instance types include:

- `c5.large`
- `c5a.large`
- `c5n.large`
- `c6g.large`

### EC2 Instance Types - Memory Optimized

Memory Optimized instances are designed for memory-intensive applications that require high memory-to-CPU ratios. They are ideal for applications such as databases, in-memory caches, and real-time big data analytics.

- Fast performance for workloads that process large data sets in memory
- Tasks such as:
  - High-performance databases (e.g., MySQL, PostgreSQL, MongoDB)
  - In-memory caches (e.g., Redis, Memcached)
  - Real-time big data analytics
  - Data warehousing
  - High-performance computing (HPC)
  - Distributed web scale cache stores
  - Applications performing real-time processing of big unstructured data

Some examples of Memory Optimized instance types include:

- `r5.large`
- `r5a.large`
- `r5n.large`
- `r6g.large`

### EC2 Instance Types - Storage Optimized

Storage Optimized instances are designed for data-intensive applications that require high disk throughput and IOPS. They are ideal for applications such as NoSQL databases, data warehousing, and log processing.

- Great for storage-intensive tasks that require high, sequential disk read and write access to large data sets on local storage
- Tasks such as:
  - High frequency online transaction processing (OLTP) systems
  - Relational and NoSQL databases
  - Cache for in-memory databases
  - Data warehousing
  - Distributed file systems

Some examples of Storage Optimized instance types include:

- `i3.large`
- `i3en.large`
- `d2.large`

## Security Groups and Classic Ports

### Introduction to Security Groups

Security Groups are virtual firewalls that control inbound and outbound traffic to EC2 instances. They act as a security layer to protect instances from unauthorized access.

- Security Groups are the fundamental of network security in AWS.
- They are used to control inbound and outbound traffic to EC2 instances.
- Security Groups are stateful, meaning that if you allow inbound traffic on a specific port, the response traffic is automatically allowed.
- Security Groups only contain allow rules, meaning you can only specify what traffic is allowed, not what traffic is denied.
- Security Groups rules can references by IP address, CIDR blocks, or other Security Groups.

### Security Groups - Deeper Dive

Security Groups are associated with EC2 instances and control the traffic that can reach them. They can be configured to allow or deny traffic based on various criteria.

- Security Groups are acting as virtual firewalls for your instances.
- They regulate:
  - Access to ports
  - Authorized IP ranges - IPv4 and IPv6
  - Control of inbound network traffic (from the internet to your instance)
  - Control of outbound network traffic (from your instance to the internet)

### Security Groups - Good to Know

- Security Groups are associated with EC2 instances, not the VPC.
- You can associate multiple Security Groups with an instance.
- Locked down to a region, meaning you cannot use a Security Group from one region in another region.
- Does live "outside" the EC2 instance - if traffic is blocked by a Security Group, the instance will not see it.
- It's good to maintain one separate Security Group for SSH access, one for HTTP access, and one for HTTPS access.
- If your application is not accessible (timeout), check the Security Group rules first.
- If your application gives a "connection refused" error, then it is an application error or the application is not running.
- By default, all inbound traffic is blocked, and all outbound traffic is allowed.

### Classic Ports to Know

When configuring Security Groups, it's important to know the common ports used by various services. Here are some classic ports you should be aware of:

- **SSH**: Port 22 (for secure shell access to Linux instances)
- **FTP**: Port 21 (for file transfer protocol)
- **SFTP**: Port 22 (for secure file transfer protocol, often used with SSH)
- **HTTP**: Port 80 (for unsecured web traffic)
- **HTTPS**: Port 443 (for secured web traffic)
- **RDP**: Port 3389 (for remote desktop protocol access to Windows instances)

## SSH Overview

SSH (Secure Shell) is a protocol used to securely connect to remote servers and manage them over a network. It provides a secure channel over an unsecured network, allowing users to execute commands and transfer files securely.

- SSH is a secure way to connect to remote servers.
- It is a command-line tool that allows users to log in to remote machines securely.
- It uses encryption to protect the data transmitted between the client and the server.
- SSH is commonly used to manage Linux instances in AWS.
- It allows users to execute commands, transfer files, and perform administrative tasks on remote servers.
