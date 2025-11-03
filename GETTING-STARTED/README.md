# Getting Started with AWS

## AWS Cloud Overview - Regions and Availability Zones

- AWS is a global cloud service provider with data centers located worldwide.
- AWS was launched internally in 2002 because they realized their IT infrastructure could be externalized and offered as a service.
- By 2003, Amazon's infrastructure is one of their core strengths and gave them the idea to offer it as a service to third parties.
- SQS (Simple Queue Service) was the first AWS service launched in 2004.
- In 2006, AWS re-launched publicly with S3 (Simple Storage Service), EC2 (Elastic Compute Cloud), and SQS.
- They realized that they do not have to service just America, so in 2007 they launched the first AWS region outside the US, in Europe (Ireland).
- Fast forward to today, so many applications and services run on AWS, from startups to large enterprises.

### AWS Cloud Facts

- In 2023, AWS had $90 billion in annual revenue.
- AWS accounted for 31% of the market in Q1 2024, making it the largest cloud service provider (Microsoft Azure is second with 25%).
- AWS has been a pioneer and leader of te cloud computing market for over a decade.
- It has over 1,000,000 active customers, including startups, enterprises, and public sector organizations.

### AWS Cloud Use Cases

- AWS enabled you to build sophisticated and scalable applications with increased flexibility, scalability, and reliability.
- It is applicable to a diverse set of industries, including:
  - Web and mobile applications
  - Data processing and warehousing
  - Storage, backup, and disaster recovery
  - Archiving
  - Enterprise IT
  - High-performance computing
  - Internet of Things (IoT)
  - Artificial Intelligence (AI) and Machine Learning (ML)

### AWS Global Infrastructure

AWS consists of:

- AWS Regions: Geographical areas that host AWS resources. Each region is isolated and independent.
- AWS Availability Zones (AZs): Data centers within a region that are designed for fault tolerance and high availability. Each region has multiple AZs.
- AWS Data Centers: Physical facilities that house the servers and networking equipment for AWS services.
- AWS Edge Locations/Points of Presence (PoPs): Locations that deliver content to end-users with low latency through services like Amazon CloudFront.

### AWS Regions

- AWS has multiple regions worldwide, each identified by a unique code (e.g., us-east-1 for Northern Virginia, eu-west-1 for Ireland).
- Each region is made up of a cluster of data centers known as Availability Zones (AZs).

> How do you choose a region?
> If you need to launch a new application, where should you do it?
> Choose a region based on these factors:
>
> - **Compliance with data governance and legal requirements**: data never leaves a region without explicit permission.
> - **Proximity to end-users to reduce latency**.
> - **Available services within a region**: new services and new features are not always available in all regions at launch.
> - **Pricing differences between regions**: pricing varies region to region and is transparent in the service pricing pages.

### AWS Availability Zones (AZs)

- An Availability Zone (AZ) is a data center or a group of data centers within a region that are isolated from failures in other AZs.
- Each region has many AZs (usually 3, min is 3, max is 6).

> Example:
> The Sydney region (ap-southeast-2) has 3 AZs:
>
> - ap-southeast-2a
> - ap-southeast-2b
> - ap-southeast-2c
>
> Each of these AZs is one or more discrete data centers with redundant power, networking, and connectivity in an AWS Region.
> Each AZ is separate from each other, so that even if one AZ goes down, the others remain unaffected.

- Each AZ is connected with high bandwidth, ultra-low latency networking.
- All together, these AZs form a region.

### AWS Edge Locations/Points of Presence (PoPs)

- Edge Locations or Points of Presence (PoPs) are data centers located in major cities around the world.
- Amazon has 400+ Points of Presence (400+ Edge Locations and 10+ Regional Caches) in 90+ cities across 40+ countries.
- They are used to deliver content to end-users with low latency through services like Amazon CloudFront (a Content Delivery Network or CDN).
- Edge Locations are separate from AWS Regions and AZs.

### More Information

- AWS has Global Services:

  - Identity and Access Management (IAM)
  - Amazon Route 53 (DNS service)
  - Amazon CloudFront (CDN service)
  - WAF (Web Application Firewall)

- Most AWS services are region-specific, meaning you need to select a region to use them.
- Region-specific services include:

  - Amazon EC2 (Elastic Compute Cloud)
  - Amazon S3 (Simple Storage Service)
  - Amazon RDS (Relational Database Service)
  - AWS Lambda
  - Amazon VPC (Virtual Private Cloud)

- Some services are global, meaning they are not tied to a specific region (e.g., IAM, Route 53, CloudFront).
- To know if a service is global or region-specific, check the AWS documentation for that service at [https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).
