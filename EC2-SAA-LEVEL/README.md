# EC2 - Solutions Architect Associate Level

## Private vs Public vs Elastic IPs

### Private vs Public IPs (IPv4)

- Networking has two sorts of IP addresses: IPv4 and IPv6.
  - IPv4 is the most common type of IP address.
    - IPv4: 192.168.1.1
    - It uses a 32-bit address scheme allowing for a total of 2^32 addresses (just over 4 billion addresses).
  - IPv6 is a newer type of IP address.
    - IPv6: 2001:0db8:85a3:0000:0000:8a2e:0370:7334
    - It uses a 128-bit address scheme allowing for a total of 2^128 addresses (approximately 3.4×10^38 addresses).

### Private vs Public IPs Example

- Public servers talk to one another over the internet using public IP addresses.
- Private IP addresses are used for communication within a private network.
- Let's say company A has a private network which has private IP ranges.
  - All the computers within that private network can communicate with each other using their private IP addresses.
  - An internet gateway is used to connect the private network to the internet.

### Private vs Public IPs - Fundamental Differences

- Public IP:

  - Public IP addresses are assigned to devices that need to be accessible over the internet.
  - The machine can be identified and reached from any other device on the internet using its public IP address.
  - Public IP addresses are globally unique.
  - Can be geo-located to a specific country or region.

- Private IP:
  - Private IP addresses are used within a private network and are not routable on the internet.
  - Devices with private IP addresses can communicate with each other within the same private network but cannot be accessed directly from the internet.
  - Private IP addresses are not globally unique; they can be reused in different private networks. However, within a single private network, each device must have a unique private IP address.
  - Cannot be geo-located as they are not visible on the public internet.
  - Machines connect to the world wide web using a NAT (Network Address Translation) gateway or similar device that translates private IP addresses to public IP addresses.
  - Only a specified range of IP addresses are reserved for private networks:
    - 10.0.0.0 - 10.255.255.255 (10.0.0.0/8)
    - 172.16.0.0 - 172.31.255.255 (172.16.0.0/12)
    - 192.168.0.0 - 192.168.255.255 (192.168.0.0/16)

### Elastic IPs

When you stop and start an EC2 instance, its public IP address changes. To maintain a consistent public IP address, you can use an Elastic IP address.

- An Elastic IP address is a static, public IPv4 address designed for dynamic cloud computing.
- You own the Elastic IP address until you choose to release it.
- You can associate an Elastic IP address with an EC2 instance or a network interface.
- If you stop and start the instance, the Elastic IP address remains associated with the instance.
- Note: AWS charges for Elastic IP addresses that are not associated with a running instance.

With an Elastic IP address, you can ensure that your application remains accessible via the same public IP address, even if the underlying EC2 instance is stopped and started.

Basically, you can mask the failure of an instance or software by rapidly remapping the Elastic IP address to another instance in your account.

- You can only have 5 Elastic IP addresses per AWS account by default. If you need more, you can request a limit increase through the AWS Support Center.

Overall, try to avoid using Elastic IPs unless absolutely necessary:

- They often reflect a poor architecture design.
- Instead, use a random public IP and use DNS to point to it.
- Or, better yet, use a Load Balancer with a static DNS name.