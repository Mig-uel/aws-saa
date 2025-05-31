# Getting Started with AWS

**AWS Cloud History:**

- AWS Cloud was internally launched in 2002.
- In 2004, SQS was launched, making it the first public AWS service.
- In 2006, S3 and EC2 were launched as well as SQS was relaunched.
- In 2007, AWS was expanded to Europe.
- As of today, there are many applications that run on AWS, including Netflix, Airbnb, and NASA.

**AWS Cloud Number Facts:**

- AWS is a leader in the cloud computing market.
- In 2023, AWS had $90 billion in revenue.
- AWS accounts for 31% of the market in Q1 2024 (Microsoft is 2nd with 25%)
- Pioneer and Leader of the AWS Cloud Market for the 13th consecutive year.
- Has over 1,000,000 active customers.

**AWS Cloud Use Cases:**

- AWS enabled you to build sophisticated, scalable applications.
- Applicable to a diverse set of industries and use cases.
- Use cases include:
  - Enterprise IT
  - Backup and Storage
  - Big Data and Analytics
  - Website hosting
  - Application Development
  - Mobile and IoT
  - Gaming
  - The use cases are endless.

**AWS Global Infrastructure:**

- AWS Regions
- AWS Availability Zones
- AWS Data Centers
- AWS Edge Locations/Points of Presence

All of these can be found on the [AWS Global Infrastructure page](https://aws.amazon.com/about-aws/global-infrastructure/).

The first important concept in AWS are regions. A region is a physical location in the world where AWS has multiple data centers. Each region is isolated from other regions to provide fault tolerance and stability.

- AWS has Regions all over the world.
- Each region has a name, such as us-east-1, eu-west-1, etc.
- You can see the mapping of the region to their code names on the [AWS Regions and Endpoints page](https://docs.aws.amazon.com/general/latest/gr/rande.html) as well on the console.
- A region is a cluster of data centers in a specific geographic area.
- When we use an AWS service, most services are going to be linked and scoped to a specific region. Meaning if we use a service in one region, and try to use it in another region, it will be like using that service for the first time.

**How to Choose an AWS Region:**

If you need to launch a new application, where should you do it?

Well, it depends on a few factors:

- **Compliance:** Some regions have specific compliance requirements, such as GDPR in Europe. Data must be stored in the region where it is processed.
- **Proximity:** Choose a region that is close to your users to reduce latency.
- **Availability of Services:** Not all AWS services are available in all regions. Check the [AWS Regional Services List](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) to see which services are available in each region.
- **Cost:** Some regions are more expensive than others. Check the [AWS Pricing Calculator](https://calculator.aws/#/) to see the cost of services in each region.

**AWS Availability Zones:**
Availability Zones (AZs) are actually what makes up a region.

- Each region has multiple AZs (usually 3, min is 3, max is 6).

Example:

- AWS Region: ap-southeast-2 (Sydney)
- AWS Availability Zone: ap-southeast-2a, ap-southeast-2b, ap-southeast-2c

Each of these AZs is one or more discrete data centers with redundant power, networking, and connectivity in an AWS Region.

- AZs are physically separated from each other, but they are connected through a high bandwidth, and ultra-low latency network.
- AZs are designed to be isolated from failures in other AZs, providing high availability and fault tolerance.
- When you launch an AWS service, you can choose which AZ to use, or let AWS choose for you.
- You can also deploy resources across multiple AZs to increase availability and fault tolerance.
- AZs are not the same as regions, they are a subset of regions.
- All together, AZs make up a region.

**AWS Points of Presence (Edge Locations):**

- Amazon has 400+ Points of Presence (PoPs) around the world (400+ Edge Locations and 10+ Regional Edge Caches) in 90+ cities across 40+ countries.
- Edge locations are helpful for content delivery to end users with low latency.
- They are used for services like Amazon CloudFront, AWS Global Accelerator, and AWS WAF.
- Edge locations are not the same as regions or AZs, they are a separate concept.

**Tour of the AWS Console:**

AWS Global Services:

- Identity and Access Management (IAM)
- Route 53 (DNS Service)
- CloudFront (Content Delivery Network)
- AWS WAF (Web Application Firewall)

AWS Regional Services:

- Amazon EC2 (Elastic Compute Cloud) (Infrastructure as a Service)
- Elastic Beanstalk (Platform as a Service)
- Lambda (Serverless Computing) (Function as a Service)
- Rekognition (Machine Learning) (Software as a Service)

To know if a service is global or regional, you can check the [AWS Regional Services List](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).
