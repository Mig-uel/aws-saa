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

## EC2 Instances Purchasing Options

When launching EC2 instances, you have several purchasing options to choose from based on your workload requirements and budget. The main purchasing options are:

- **On-Demand Instances**: Pay for compute capacity by the hour or second, with no long-term commitments. Ideal for short-term workloads or unpredictable traffic.
- **Reserved Instances**: Commit to using EC2 instances for a one-year or three-year term in exchange for a significant discount compared to On-Demand pricing. Suitable for steady-state workloads.
- **Spot Instances**: Bid on unused EC2 capacity at potentially lower prices. Spot Instances can be interrupted by AWS with little notice, making them suitable for flexible workloads that can tolerate interruptions.
- **Savings Plans**: Flexible pricing model that provides significant savings on EC2 usage in exchange for a commitment to a consistent amount of usage (measured in $/hour) for a one- or three-year term. It applies to any EC2 instance regardless of region, instance family, operating system, or tenancy.
- **Dedicated Hosts**: Physical servers dedicated to your use, allowing you to run your instances on hardware that is not shared with other AWS customers. Useful for compliance and licensing requirements.
- **Dedicated Instances**: Instances that run on hardware dedicated to a single customer, but share the underlying hardware with other instances. They provide additional isolation compared to standard instances.
- **Capacity Reservations**: Reserve capacity for your EC2 instances in a specific Availability Zone, ensuring that you have the compute capacity available when you need it. This is useful for applications with predictable workloads.

### EC2 On-Demand Instances

On-Demand Instances allow you to pay for compute capacity by the hour or second, with no long-term commitments. This flexibility makes them ideal for short-term workloads or unpredictable traffic.

- You can launch and terminate instances as needed, paying only for the time they are running.
- On-Demand Instances are suitable for applications with variable workloads, development and testing environments, and applications that cannot be interrupted.
- They provide the highest level of flexibility and scalability, allowing you to quickly adapt to changing requirements.
- On-Demand Instances are charged based on the instance type, region, and operating system.
- They are billed by the second, with a minimum of 60 seconds for Linux instances and 1 hour for Windows instances.
- Has the highest cost compared to other purchasing options.

### EC2 Reserved Instances

Reserved Instances provide a significant discount compared to On-Demand pricing in exchange for a commitment to use EC2 instances for a one-year or three-year term. They are ideal for steady-state workloads.

- Reserved Instances are not physical instances but rather a billing discount applied to the use of On-Demand Instances.
- They provide a capacity reservation in the specified Availability Zone, ensuring that you have the compute capacity available when you need it.
- Reserved Instances are suitable for applications with predictable workloads, such as web servers, databases, and enterprise applications.
- They can be purchased in three payment options:
  - All Upfront: Pay the entire reservation fee upfront for the term.
  - Partial Upfront: Pay a portion of the reservation fee upfront and the rest in monthly installments.
  - No Upfront: Pay for the reservation in monthly installments over the term.
- You can reserve a specific instance attributes, such as instance type, region, and Availability Zone.
- Reserved Instance's Scope can be set to either regional or zonal, depending on your needs.
- Recommended for steady-state workloads that require consistent compute capacity.
- You can buy and sell Reserved Instances in the AWS Marketplace, allowing you to adjust your capacity as needed.

There is a special type of Reserved Instances called **Convertible Reserved Instances** that allow you to change the instance type, operating system, or tenancy during the term, providing additional flexibility.

### EC2 Savings Plans

Savings Plans are a flexible pricing model that provides significant savings on EC2 usage in exchange for a commitment to a consistent amount of usage (measured in $/hour) for a one- or three-year term. It applies to any EC2 instance regardless of region, instance family, operating system, or tenancy.

- Savings Plans offer a flexible alternative to Reserved Instances, allowing you to save on your EC2 costs while maintaining the flexibility to change instance types and configurations.
- Get a discount based on long-term usage commitment, similar to Reserved Instances.
- Commit to a specific amount of usage (measured in $/hour) for a one- or three-year term.
- Usage beyond the committed amount is charged at the On-Demand rate.
- Locked to a specific instance family and AWS Region, but allows you to change instance types and configurations within that family.
- Flexible across instance sizes, operating systems, and tenancies.

### EC2 Spot Instances

Spot Instances allow you to bid on unused EC2 capacity at potentially lower prices. They can be interrupted by AWS with little notice, making them suitable for flexible workloads that can tolerate interruptions.

- Spot Instances are ideal for workloads that are flexible and can be interrupted, such as batch processing, data analysis, and machine learning training.
- Can get significant cost savings compared to On-Demand Instances, often up to 90% off the On-Demand price.
- Instances that you can 'lose' at any point of time if your max price is lower than the current Spot price.
- The MOST cost-effective way to run workloads in AWS.
- Not suitable for production workloads or applications that require high availability.

### EC2 Dedicated Hosts

Dedicated Hosts are physical servers dedicated to your use. They provide you with complete control over the physical server and are ideal for applications that require compliance with specific licensing or regulatory requirements.

- A physical server with EC2 instance capacity fully dedicated to your use.
- Allows you to address compliance and regulatory requirements that require physical isolation.
- Purchasing options:
  - On-demand: pay per second for active Dedicated Hosts.
  - Reserved: 1-year or 3-year term with a significant discount.
- The most expensive purchasing option.
- Useful for software that have complicated licensing model (BYOL, etc.) or for applications that require physical isolation.

### EC2 Dedicated Instances

Dedicated Instances are instances that run on hardware dedicated to a single customer. They provide additional isolation compared to standard instances, but share the underlying hardware with other instances.

- Dedicated Instances run on hardware that is dedicated to a single customer, providing additional isolation compared to standard instances.
- May share the underlying hardware with other instances, but are isolated at the hypervisor level.
- No control over instance placement, meaning you cannot choose which physical server your instances run on.

### EC2 Capacity Reservations

Capacity Reservations allow you to reserve capacity for your EC2 instances in a specific Availability Zone, ensuring that you have the compute capacity available when you need it. This is useful for applications with predictable workloads.

- Reserve On-Demand instances capacity in a specific Availability Zone for any duration.
- You always have access to the reserved capacity, even during peak demand periods.
- No time commitment is required, and you can cancel the reservation at any time.
- No billing discount is applied, and you pay the On-Demand rate for the reserved capacity.
- You are charged for the reserved capacity regardless of whether you use it or not.
- Suitable for short-term workloads that require guaranteed capacity, such as batch processing, data analysis, and machine learning training.

### Which Purchasing Option to Choose?

- **On-Demand Instances:** coming and stating in resort whenever we like, we pay for the time we use them.
- **Reserved Instances:** like planning ahead and if we plan to stay for a long time, we may get a good discount.
- **Savings Plans:** pay a certain amount per hour for a certain period of time, and stay in any room type we want.
- **Spot Instances:** the hotel allows people to bid on unused rooms and the highest bidder gets the room, but the hotel can kick us out at any time if they need the room back.
- **Dedicated Hosts:** like renting a whole hotel for ourselves, we have complete control over the rooms and can customize them as we like.
- **Dedicated Instances:** like renting a room in a hotel that is dedicated to us, but we share the underlying infrastructure with other guests.
- **Capacity Reservations:** booking a room for a period of time, ensuring that we have a room available when we need it, but we pay the full price for the room regardless of whether we use it or not.

## IP Address Charges in AWS

In AWS, there are charges associated with the use of IP addresses, particularly Elastic IP addresses (EIPs) and public IP addresses.

Starting from February 2024, there are charges for all public IPv4 addresses created in your account.

## Spot Instances and Spot Fleet

Spot Instances are a cost-effective way to run workloads in AWS by bidding on unused EC2 capacity. They can be interrupted by AWS with little notice, making them suitable for flexible workloads that can tolerate interruptions.

- Can get a discount of up to 90% compared to On-Demand Instances.
- We define a maximum price we are willing to pay for the Spot Instances.
- If the Spot price goes above our maximum price, our Spot Instances can be terminated with little notice.
  - The hourly spot price varies based on supply and demand.
- If the current spot price is greater than our maximum price, you can choose to either:
  - Terminate the Spot Instances.
  - Stop the Spot Instances (if they are configured to do so).
- Spot blocks were a feature that allowed you to run Spot Instances for a fixed duration without interruption, but they have been deprecated.
- Spot Instances are ideal for workloads that can tolerate interruptions, such as batch jobs, data analysis, or workloads that are resilient to interruptions.

### How to Terminate Spot Instances

A Spot Request is a request to launch Spot Instances. It consists of the following components:

- Maximum price: The maximum price you are willing to pay for the Spot Instances.
- Desired capacity: The number of Spot Instances you want to launch.
- Launch specifications: The configuration of the Spot Instances, such as instance type, AMI, security groups, and user data.
- Request type: The type of Spot Request, which can be either one-time or persistent.
- Validation period: The time period during which the Spot Request is valid.

To terminate Spot Instances, the Spot Instance requests must be:

- In the `open` state.
- In the `active` state.
- In the `disabled` state.

Cancelling a Spot Request does not terminate the Spot Instances. If you want to terminate the Spot Instances, you first need to cancel the Spot Request, and then terminate the Spot Instances manually.

### Spot Fleets

Spot Fleets are a collection of Spot Instances that can be launched together to meet a specific capacity requirement. They allow you to manage multiple Spot Instances as a single entity, making it easier to scale your workloads.

- A Spot Fleet is a collection of Spot Instances + optionally On-Demand Instances.
- The Spot Fleet will try to fulfill the target capacity with price constraints and instance types that you specify.
  - Define possible launch pools: instance types, availability zones, OS, etc.
  - Can have multiple launch pools so that the Spot Fleet can choose the best option based on availability and price.
  - Spot Fleet stops launching instances when the target capacity is reached or when the maximum price is reached.

We define strategies for how the Spot Fleet should fulfill the target capacity:

- **Lowest Price**: The Spot Fleet will launch instances from the lowest-priced available Spot Instances (cost optimization, short workloads).
- **Diversified**: The Spot Fleet will launch instances from multiple Spot Instance pools to reduce the risk of interruption (availability optimization, long workloads).
- **Capacity Optimized**: The Spot Fleet will launch instances from the most available Spot Instance pools to reduce the risk of interruption (availability optimization, long workloads).
- **Price Capacity Optimized**: The Spot Fleet will launch instances from the most available Spot Instance pools that are below the maximum price (availability optimization, cost optimization, long workloads).

The idea of Spot Fleets is that it can be complicated but using the Spot Fleet you are able to define multiple launch pools, multiple instance types, and multiple strategies to fulfill the target capacity.
Spot Fleets allow us to automatically request Spot Instances with the lowest price, or with the most available capacity, or with a combination of both.
