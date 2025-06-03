# EC2 Instance Storage

## EBS Overview

Amazon Elastic Block Store (EBS) provides block-level storage volumes for use with Amazon EC2 instances. EBS volumes are highly available and reliable, designed for mission-critical applications. They can be attached to a single EC2 instance at a time, but can be detached and reattached to different instances as needed.

### What's an EBS Volume?

An EBS (Elastic Block Store) volume is a network drive you can attach to your instances while they run.

- Allow your instances to persist data beyond their lifecycle.
- They can only be mounted to one instance at a time (at the CCP level).
- CCP level - one EBS volume can only be attached to one instance at a time.
- Associate Level (Solutions Architect, Developer, SysOps) - one EBS volume can be attached to multiple instances at a time (multi-attach feature for some EBS volume types).
- EBS volumes are bound to a single Availability Zone (AZ) and cannot be moved across AZs without creating a snapshot.

Analogy: Think of EBS volumes like a "network USB drive" that you can attach to your EC2 instances. You can store data on it, and it remains available even if the instance is stopped or terminated.

For the free tier, you get 30 GB of EBS storage for free, which can be used for both EBS General Purpose SSD (gp2) and Magnetic volumes.

### EBS Volumes

EBS volumes are a network drive not a physical drive.

- It uses the network to communicate with the instance, meaning there is a slight latency compared to local storage.
- It can be detached from an EC2 instance and attached to another instance quickly.
- They are locked to a single Availability Zone (AZ).
  - An EBS volume in us-east-1a cannot be attached to an instance in us-east-1b.
  - To move an EBS volume across AZs, you must create a snapshot and then create a new volume from that snapshot in the desired AZ.
- It is a volume so you have to provision it before you can use it.
  - You get billed for the storage you provision, not the storage you use.
  - You can increase the size of an EBS volume at any time, but you cannot decrease it.

### EBS - Delete On Termination Attribute

When you launch an EC2 instance, you can specify whether the EBS volumes attached to it should be deleted when the instance is terminated. This is controlled by the "Delete on Termination" attribute.

- If set to true, the EBS volume will be deleted when the instance is terminated.
- If set to false, the EBS volume will persist even after the instance is terminated, allowing you to reattach it to another instance later.
- By default, the root EBS volume (the one that contains the operating system) is set to delete on termination, but you can change this setting when launching the instance or later through the AWS Management Console or CLI.

## EBS Snapshots

EBS snapshots are backups of EBS volumes that are stored in Amazon S3. They can be used to create new EBS volumes or restore existing ones.

- Are backups of your EBS volumes at a specific point in time.
- Not necessary to detach the EBS volume to create a snapshot, but recommended to ensure data consistency.
- Can copy snapshots across regions.
- Are incremental, meaning only the blocks that have changed since the last snapshot are saved, reducing storage costs.
- Can be used to create new EBS volumes in the same or different Availability Zones.
- Can be used to restore an EBS volume to a previous state.
- Can be shared with other AWS accounts or made public, allowing others to create volumes from your snapshots.
- Are stored in Amazon S3, but you cannot access them directly like regular S3 objects.
- Are automatically encrypted if the source EBS volume is encrypted, and can be used to create encrypted volumes in other regions.
- Can be created manually or automatically using Amazon Data Lifecycle Manager (DLM) to manage snapshot schedules and retention policies.
- Can be used to create AMIs (Amazon Machine Images) for launching new EC2 instances with the same configuration as the original instance.

### EBS Snapshot Features

EBS Snapshot Archive is a feature that allows you to move infrequently accessed snapshots to lower-cost storage, reducing costs while retaining the ability to restore them when needed.

- Move a snapshot to an "archive tier" that is up to 75% cheaper than standard snapshots.
- Takes within 24 to 72 hours to restore an archived snapshot.

Recycle Bin for EBS Snapshots is a feature that allows you to recover deleted snapshots within a specified retention period, providing an additional layer of data protection.

- Setup rules to retain deleted snapshots so you can recover them after an accidental deletion.
- Retention period can be set from 1 day to 1 year.

Fast Snapshot Restore is a feature that allows you to pre-warm EBS snapshots, enabling faster volume creation from snapshots.

- Force full initialization of the snapshot to have no latency on the first use.
- Benefits:
  - Reduces the time it takes to create a new volume from a snapshot.
  - Ensures that the data is immediately available when the volume is created.
  - Can be enabled for specific snapshots, allowing you to optimize performance for critical workloads.
- Pre-warms the snapshot so that when you create a new volume from it, the data is immediately available.
  - Reduces the time it takes to create a new volume from a snapshot, especially for large volumes.
- Can be enabled for specific snapshots, allowing you to optimize performance for critical workloads.
- This feature is costly, so it is typically used for production workloads where performance is critical.

## AMI (Amazon Machine Image) Overview

An AMI (Amazon Machine Image) is a pre-configured template that contains the operating system, application server, and applications required to launch an EC2 instance. It serves as a blueprint for creating new instances.

- AMI stands for Amazon Machine Image.
- AMIs are a customization of an EC2 instance.
  - You add your own software, configuration, operating system, monitoring, etc.
  - Fast boot/configuration time because all your software is pre-packaged.
- AMI are built for a specific region (and can be copied across regions).
  - You can copy an AMI from one region to another, but it must be done explicitly.
- You can launch EC2 instances from:
  - A public AMI (AWS provided)
  - Your own AMI (customized; you make and maintain them)
  - An AWS Marketplace AMI (third-party provided)

### AMI Process (from an EC2 Instance)

1. Start an EC2 instance and customize it (install software, configure settings, etc.).
2. Stop the instance to ensure data consistency.
3. Build an AMI from the stopped instance.
   - This creates a snapshot of the root EBS volume and stores it as an AMI.
4. The AMI can now be used to launch new instances with the same configuration.

## EC2 Instance Store

An EC2 instance store is a type of storage that provides temporary block-level storage for EC2 instances. It is physically attached to the host machine and is ideal for high-performance workloads that require low-latency access to data.

- EBS volumes are network drives with good but limited performance.
- If you need high performance hardware disk, use an instance store.
- Instance store volumes are physically attached to the host machine.

Instance Stores:

- Provide better I/O performance than EBS volumes.
- EC2 instance stores are ephemeral, meaning they are temporary and data is lost when the instance is stopped or terminated.
- Good for buffer, cache, scratch data, or temporary data that does not need to persist beyond the instance lifecycle.
- Risk of data loss if the instance fails or is terminated.
- Cannot be detached and reattached to other instances like EBS volumes.
- It is you responsibility to manage data persistence and backups.

## EBS Volume Types

EBS volumes come in 6 different types, each optimized for different use cases. The main types are:

**gp2/gp3**: General Purpose SSD volumes that balances prices and performance for a wide range of workloads.

- Balanced price and performance.
- Suitable for a wide range of workloads, including boot volumes and small to medium-sized databases.
- gp3 offers higher performance at a lower cost compared to gp2.

**io1/io2 Block Express (SSD)**: Provisioned IOPS SSD volumes designed for I/O-intensive applications that require high performance and low latency.

- Designed for I/O-intensive applications that require high performance and low latency.
- Highest performance SSD volume for mission-critical low-latency or high-throughput workloads.

**st1 (HDD)**: Low-cost HDD volumes for frequently accessed, throughput-intensive workloads.

- Suitable for big data, data warehouses, and log processing.

**sc1 (HDD)**: Lowest-cost HDD volumes for less frequently accessed workloads.

- Suitable for infrequently accessed data, such as backups and archives.

EBS volumes are characterized in Size, Throughput, and IOPS (Input/Output Operations Per Second)

- When in doubt always consult the AWS documentation for the latest information on EBS volume types and their specifications.
- Only gp2/gp3 and io1/io2 Block Express volumes can be used as boot volumes (the root volume of an EC2 instance).

### EBS Volume Types Use Cases

**General Purpose SSD**

- Cost effective storage with low latency.
- Used for boot volumes, virtual desktops, development and test environments, and small to medium-sized databases.
- Size can be between 1 GB and 16 TB.
- gp3
  - Is a newer generation of volumes
  - Baseline of 3,000 IOPS and 125 MiB/s throughput.
  - Can increase IOPS up to 16,000 and throughput up to 1,000 MiB/s independently.
- gp2
  - Is the older generation of volumes
  - Small gp2 volumes can burst IOPS up to 3,000.
  - Size of the volume and IOPS are linked (max IOPS is 16,000).
  - 3 IOPS per GB, means at 5,334 GB you get the max IOPS of 16,000.

**Provisioned IOPS (PIOPS) SSD**

- Used for critical business applications with sustained I/O performance, applications that need more than 16,000 IOPS, and large databases.
- Great for databases workloads (sensitive to storage performance and consistency).
- io1 (4 GiB - 1 TiB)
  - Max PIOPS of 64,000 for Nitro EC2 instances and 32,000 for non-Nitro instances.
  - Can increase PIOPS independently of volume size.
- io2 (4 GiB - 64 TiB)
  - Sub-millisecond latency.
  - Max PIOPS of 256,000 with an IOPS:GiB ration of 1,000:1.
- Support EBS multi-attach (attach the same volume to multiple instances).

**Hard Disk Drive (HDD)**

- Cannot be used as boot volumes.
- Size from 125 GiB to 16 TiB.
- Throughput optimized HDD (st1)
  - Used for big data, data warehouses, and log processing.
  - Cost-effective storage for frequently accessed workloads.
  - Max throughput of 500 MiB/s, max IOPS of 500.
- Cold HDD (sc1)
  - Lowest cost storage for less frequently accessed workloads.
  - Used for infrequently accessed data, such as backups and archives.
  - Max throughput of 250 MiB/s, max IOPS of 250.

## EBS Multi-Attach - io1/io2 Family

EBS Multi-Attach is a feature that allows you to attach an EBS volume to multiple EC2 instances simultaneously. This feature is available for io1 and io2 EBS volume types.

- Attach the sane EBS volume to multiple EC2 instances in the same Availability Zone.
- Each instance has full read/write permissions to the high-performance EBS volume.

Use Cases:

- Achieve higher application availability in clustered Linux applications (ex. Teradata)
- Applications must manage concurrent write operations.

Remember, this multi-attach feature is only available for within a specified Availability Zone and is not supported for all EBS volume types.

An EBS volume can only be attached up to 16 instances at a time and must use a file system that supports concurrent access.

## EBS Encryption

EBS encryption is a feature that allows you to encrypt EBS volumes and snapshots to protect your data at rest. It uses AWS Key Management Service (KMS) to manage the encryption keys.

When you create an encrypted EBS volume, you get the following benefits:

- Data at rest is encrypted using AES-256 encryption.
- All the data in flight between the instance and the volume is encrypted.
- All snapshots created from the encrypted volume are also encrypted.
- All volumes created from the encrypted snapshot are also encrypted.
- Encryption and decryption are handled transparently by AWS, so you don't need to manage the encryption keys yourself.
- Encryption has a minimal impact on performance.
- EBS encryption leverages keys from AWS Key Management Service (KMS) to encrypt the data.

### Encryption: Encrypt an Unencrypted Volume

To encrypt an unencrypted EBS volume, you can create a snapshot of the volume and then create a new encrypted volume from that snapshot. Here are the steps:

1. Create an EBS snapshot of the unencrypted volume.
   - This creates a point-in-time backup of the volume.
2. Encrypt the EBS snapshot.
   - Use the AWS Management Console, CLI, or SDK to create an encrypted copy of the snapshot.
3. Create a new EBS volume from the encrypted snapshot (the volume wil also be encrypted).
   - Specify the desired size and Availability Zone for the new volume.
4. Now you can attach the new encrypted volume to the original EC2 instance or any other instance in the same Availability Zone.
