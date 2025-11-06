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

