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
