# IAM & AWS CLI

## IAM Intro: Users, Groups, Policies

- IAM (Identity and Access Management) is a **global** service that helps you securely control access to AWS resources.
- When we created an AWS account, we created a **root user** or **root account** with full access to all AWS services and resources in that account.
- Best practice is to **not use the root user for everyday tasks**. Instead, create **IAM users** with specific permissions.
- An **IAM user** is an entity that represents a person or service that interacts with AWS resources.
- IAM users can be organized into **IAM groups**, which are collections of users that share the same permissions.
- Groups can only contain users, not other groups.
- Users do not have to belong to a group, but it is a best practice to assign users to groups to manage permissions more easily.
- A user can belong to multiple groups.

### IAM: Permissions

- Users or groups can be assigned JSON documents called **policies** that define their permissions.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::example_bucket"
    }
  ]
}
```

- In AWS, you do not allow everyone to do everything by default. Instead, you start with no permissions and then explicitly grant permissions as needed.
- In AWS, you apply the principle of **least privilege**, which means giving users only the permissions they need to perform their tasks and no more.

---

## IAM Policies

- Let's say we have a group called "Developers" with three users: Alice, Bob, and Charlie. If we assign a policy to the "Developers" group that allows access to Amazon S3, all three users will inherit that permission.
- If we have a user named Fred who is not part of any group, we can assign an inline policy directly to Fred that allows him to access Amazon EC2.
- If one of the developers, say Alice, is part of another group called "Admins" that has broader permissions, she will inherit permissions from both the "Developers" and "Admins" groups.

### IAM Policy Structure

- An IAM policy is a JSON document that consists of one or more statements.

```json
{
  "Version": "2012-10-17", // policy version
  "Id": "Policy1617181920", // optional policy ID
  "Statement": [
    // array of statements
    {
      // individual statement
      "Sid": "Stmt1617181921", // optional statement ID
      "Effect": "Allow", // or "Deny"
      "Action": "s3:ListBucket", // action or list of actions
      "Resource": "arn:aws:s3:::example_bucket" // resource or list of resources
    },
    {
      "Effect": "Deny",
      "Principal": "*", // wildcard principal
      "Action": ["s3:DeleteObject", "s3:PutObject"], // multiple actions
      "Resource": ["arn:aws:s3:::example_bucket/*"] // multiple resources
    }
  ]
}
```

- A policy consists of:
  - **Version**: The version of the policy language.
  - **Id**: An optional identifier for the policy.
  - **Statement**: An array of individual statements that define permissions.
- Each statement includes:
  - **Sid**: An optional identifier for the statement.
  - **Principal**: Specifies the user, account, service, or other entity that is allowed or denied access to a resource. (Only used in resource-based policies).
  - **Effect**: Specifies whether the statement allows or denies access ("Allow" or "Deny").
  - **Action**: Specifies the action or actions that are allowed or denied (e.g., "s3:ListBucket").
  - **Resource**: Specifies the resource or resources to which the action applies (e.g., "arn:aws:s3:::example_bucket").
  - **Condition**: (Optional) Specifies conditions under which the statement is in effect.

---

## IAM MFA Overview

### IAM — Password Policy

- In AWS, we have two defense mechanisms to protect our IAM users:

  - **Multi-Factor Authentication (MFA)**: An additional layer of security that requires users to provide two or more forms of authentication.
  - **Password Policy**: A set of rules that define the complexity and expiration of passwords for IAM users.

- A strong password policy can help prevent unauthorized access to your AWS resources by ensuring that users create secure passwords.
- A password policy can include requirements such as:

  - Minimum password length
  - Use of uppercase and lowercase letters
  - Inclusion of numbers and special characters
  - Password expiration period
  - Prevention of password reuse

- Multi-Factor Authentication (MFA) adds an extra layer of security by requiring users to provide a second form of authentication in addition to their password.
- Users have access to your AWS resources and can possibly change configurations or delete resources in your account.
- **You should want to protect your root account and all IAM users with MFA.**
- MFA can be implemented using various methods, such as:

  - Virtual MFA devices (e.g., smartphone apps like Google Authenticator or Authy)
  - Hardware MFA devices (e.g., physical tokens)
  - SMS-based MFA (text messages sent to a mobile phone)

- MFA = Something you know (password) + Something you have (MFA device)
- By enabling MFA, even if a user's password is compromised, an attacker would still need access to the MFA device to gain access to the account.

---

## AWS Access Keys, CLI, and SDK

### How Can Users Access AWS?

- Users can access AWS in several ways:

  - **AWS Management Console**: A web-based interface for managing AWS services (protected by password and MFA).
  - **AWS Command Line Interface (CLI)**: A tool that allows users to interact with AWS services using command-line commands (protected by access keys).
  - **AWS Software Development Kits (SDKs)**: Libraries that allow developers to interact with AWS services programmatically using various programming languages (e.g., Python, Java, JavaScript) (protected by access keys).

- Access Keys are generated through the AWS Management Console for IAM users.
- Users manage their access keys securely and avoid sharing them publicly.
- **Important**: Do not share your access keys with anyone or include them in publicly accessible code repositories.

- Access keys consist of two parts:

  - **Access Key ID**: A unique identifier for the access key (~= username).
  - **Secret Access Key**: A secret value used to sign requests to AWS services (~= password).

### What is AWS CLI?

- The AWS Command Line Interface (CLI) is a unified tool that allows users to manage AWS services from the command line.
- AWS CLI provides direct access to the public APIs of AWS services.
- Users can perform various tasks, such as creating and managing resources, deploying applications, and automating workflows.
- AWS CLI supports multiple operating systems, including Windows, macOS, and Linux.
- To use AWS CLI, users need to install it on their local machine and configure it with their access keys.
- Once configured, users can run AWS CLI commands to interact with AWS services.

### What is AWS SDK?

- AWS Software Development Kits (SDKs) are libraries that provide a convenient way for developers to interact with AWS services using various programming languages.
- AWS SDKs handle tasks such as authentication, request signing, and error handling, making it easier for developers to work with AWS services.
- AWS SDKs are available for multiple programming languages, including Python (Boto3), Java, JavaScript (Node.js), Ruby, PHP, and .NET.
- Developers can use AWS SDKs to build applications that leverage AWS services, such as storage, databases, machine learning, and more.
- AWS SDKs are regularly updated to support new features and services offered by AWS.
