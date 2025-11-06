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
