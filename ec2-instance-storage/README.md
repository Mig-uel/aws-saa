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
