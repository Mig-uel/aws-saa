# EC2- Solutions Architect Associate Level

## Private vs Public vs Elastic IP

### Private vs Public IP (IPv4)

- **Private IP**: Used for communication within a VPC. Not routable on the internet.
- **Public IP**: Assigned to instances that need to communicate with the internet. Routable on the internet.

Networking has two sorts of IP addresses:

IPv4:

- IPv4 are the most common type of IP address used in networking.
- 32-bit address, written as four decimal numbers separated by dots (e.g., 192.168.1.1)

  - [0-255]. [0-255]. [0-255]. [0-255]

- IPv4 allows for approximately 3.7 billion unique addresses in the public address space.
- Public IPs are routable on the internet, while private IPs are not.

IPv6:

- IPv6 is the newer version of IP addressing, designed to replace IPv4 due to the exhaustion of available IPv4 addresses.
- 128-bit address, written as eight groups of four hexadecimal digits separated by colons (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334)

- Public IPv6 addresses are routable on the internet, while private IPv6 addresses are not.

- IPv4 addresses are more common, but IPv6 is becoming increasingly important due to the exhaustion of IPv4 addresses.
- IPv6 addresses is newer and more complex, but it provides a larger address space and better support for modern networking needs.

Example (Public): Let's say you have a web server with a public IP address and another server with a public IP address. Using their public IP addresses, they can communicate with each other over the internet.

Example (Private): A company has a private network with private IP addresses assigned to its internal servers. These servers can communicate with each other using their private IP addresses, but they cannot be accessed directly from the internet.

Public IPs:

- Public IP means that the machine can be identified on the internet.
- Must be unique across the entire internet.
- Can be geo-located.

Private IPs:

- Private IP means that the machine can only be identified within a private network.
- Can be reused across different private networks but not within the same network.
- Cannot be geo-located.
- Machines connect to the internet using a NAT + internet gateway (proxy).
- Only a specific range of IPs can be used as private IPs, defined by RFC 1918.

### Elastic IP

Elastic IP is a static public IPv4 address designed for dynamic cloud computing.

- When you stop and start an EC2 instance, it gets a new public IP address.
- If you need to have a fixed public IP address for your instance, you can allocate an Elastic IP address.
- An Elastic IP address is a public IPv4 address that you own as long as you keep it allocated.
- You can associate an Elastic IP address with one instance at a time.
- With an Elastic IP address, you can mask the failure of an instance or software by quickly remapping the address to another instance in your account.
- You can only have a limited number(5 by default) of Elastic IP addresses per account in a region.

Overall, try to avoid using Elastic IPs unless absolutely necessary:

- They often reflect poor architecture.
- Instead, use a random public IP address and register a DNS name for it.
- If you need a fixed IP, consider using a load balancer or Route 53 for DNS management.

By default, an EC2 instance comes with:

- A private IP address for the internal AWS network.
- A public IP address for internet access (if configured).

When we are SSHing into an EC2 instance:

- We cannot SSH into the private IP address from outside the VPC because we are not within the VPC.
- We can only SSH into the public IP address from outside the VPC.

## Placement Groups

Placement groups are a way to control the placement of EC2 instances within a single Availability Zone (AZ) to meet specific needs.

We want to use placement groups when we want to:

- Have control over the EC2 Instance placement strategy.
- We do not get direct interaction with the hardware, but we can influence the placement of instances.
- When you create a placement group, you specify one of the following strategies:
  - **Cluster**: Place instances close together in a single AZ for low latency and high throughput (high performance, high risk).
  - **Spread**: Place instances across multiple hardware to reduce the risk of simultaneous failures (max 7 instances per AZ) (low performance, low risk) - for critical applications.
  - **Partition**: Similar to Spread, but spreads instances across many different partitions within the same AZ (which rely on different set of racks) within the same AZ. Scales to 100s of instances per group (Hadoop, Cassandra, Kafka, etc.) (medium performance, medium risk).

### Placement Groups: Cluster

In a cluster placement group, instances are placed close together in a single Availability Zone (AZ) to achieve low latency and high throughput.

Pros:

- Great network performance (10 Gbps bandwidth between instances with Enhanced Networking enabled).
- Low latency communication between instances.

Cons:

- If the AZ fails, all instances fails at the same time.
- Not suitable for high availability applications.
- Limited to a single AZ, so if you need high availability, you should use multiple AZs.

Use Cases:

- High-performance computing (HPC) applications.
- Big data applications that require low latency and high throughput.
- Applications that need extremely low network latency, such as financial applications or real-time analytics.

### Placement Groups: Spread

In a spread placement group, instances are placed across multiple hardware to reduce the risk of simultaneous failures. All the EC2 instances in a spread placement group are placed spread across different AZs and different hardware.

Pros:

- Can span multiple AZs.
- Reduces the risk of simultaneous failures.
- EC2 instances are placed on different hardware, so if one instance fails, the others are not affected.

Cons:

- Limited to a maximum of 7 instances per AZ per placement group.
- Not suitable for applications that require low latency and high throughput.

Use Cases:

- Critical applications that require high availability and fault tolerance.
- Applications that can tolerate some latency but require high availability.

### Placement Groups: Partition

In a partition placement group, instances are spread across many different partitions within the same AZ, which rely on different sets of racks. This allows for better fault tolerance and scalability.

Each partition represents a rack of hardware, and instances in different partitions do not share the same underlying hardware.

- You can have up to 7 partitions per AZ, and each partition can have multiple instances.
- Spans multiple AZs in the same region.
- Scales to 100s of instances per group.
- The instances in a partition do not share the same racks with the instances in other partitions.
- A partition failure can affect many EC2 instances, but won't affect other partitions.
- EC2 instances get access to the partition information as metadata.

Use Cases:

- Applications that require high availability and fault tolerance.
- Applications that can scale horizontally and require a large number of instances.
- Distributed applications like Hadoop, Cassandra, Kafka, etc.

## Elastic Network Interfaces (ENI)

An Elastic Network Interface (ENI) is a virtual network interface that you can attach to an EC2 instance in a VPC. It provides a way to manage network connectivity and IP addresses for your instances.

- Logical component in a VPC that represents a virtual network card (it is what gives instances access to the network).
- Each ENI can have the following attributes:
  - A primary private IPv4 address, one or more secondary private IPv4 addresses, and one or more IPv6 addresses.
  - One Elastic IP address (IPv4) per private IPv4 address.
  - One public IPv4 address (if the subnet is configured to assign public IPs).
  - One or more security groups.
  - A MAC address.
- You can create ENI independently of instances and attach them to instances later (very useful for failover).
- Bound to a specific Availability Zone (AZ).
