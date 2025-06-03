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

- 