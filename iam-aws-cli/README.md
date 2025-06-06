# IAM and AWS CLI

## IAM (Identity and Access Management)

IAM is a web service that helps you securely control access to AWS resources. With IAM, you can create and manage AWS users and groups, and use permissions to allow or deny their access to AWS resources.

- IAM stands for Identity and Access Management.
- It is a global service, meaning it is not region-specific.
- When we created an AWS account, by default, we created a root account that has full access to all AWS services and resources in the account and should not be used or shared.
- The only reason to use the root account is to perform tasks that require root user access, such as changing your AWS support plan or closing your AWS account.
- We should instead create an IAM user with administrative privileges and use that user for day-to-day tasks.
- Users are people within your organization, and can be grouped together into IAM groups.
- Groups can only contain users, not other groups.
- Some users may not belong to any group, and that is fine.
- Users can be part of multiple groups, and groups can have different permissions.

### IAM: Permissions

IAM permissions are policies that define what actions are allowed or denied on specific resources. Permissions are assigned to IAM users, groups, or roles.

- Users or groups can be assigned JSON documents called policies that define their permissions.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "*"
    }
  ]
}
```

- The above policy allows the user to list all S3 buckets in the account.
- In AWS, you don't allow everyone to do everything. Instead, you start with no permissions and then add permissions as needed. This is known as the principle of least privilege and prevents accidental or malicious actions.

### Tags

- Tags can be used to add metadata to AWS resources.
- Tags are key-value pairs that can be attached to AWS resources.
- Tags can be used to organize and manage resources, and can also be used for cost allocation and billing.
- You can create and manage tags using the AWS Management Console, AWS CLI, or AWS SDKs.
- Tags can be used to filter resources in the AWS Management Console, and can also be used in IAM policies to control access to resources based on tags.

### IAM: Policies

- We can attach policies to users, groups, or roles levels.
- Policies can be inherited from groups to users.

### IAM: Policies Structure

IAM policies are JSON documents that define permissions. The structure of an IAM policy includes:

- **Version**: The version of the policy language. The current version is "2012-10-17".
- **Id**: An optional identifier for the policy.
- **Statement**: An array of statements that define the permissions. Each statement includes:
  - **Sid**: An optional identifier for the statement.
  - **Effect**: Either "Allow" or "Deny", indicating whether the action is allowed or denied.
  - **Action**: The specific actions that are allowed or denied (e.g., "s3:ListBucket").
  - **Resource**: The resources to which the actions apply (e.g., "\*", which means all resources).
  - **Principal**: The AWS account or user to which the policy applies (used in resource-based policies).
- **Condition**: Optional conditions that must be met for the policy to apply (e.g., based on tags or IP addresses).

### IAM: Password Policy

IAM allows you to set a password policy for your AWS account:

- You can setup a minimum password length.
- Require specific character types (uppercase, lowercase, numbers, symbols).
- Enforce password expiration and history.
- Allow all IAM users to change their own passwords.
- You can also enforce MFA (Multi-Factor Authentication) for added security.

### IAM: MFA (Multi-Factor Authentication)

MFA adds an extra layer of security to your AWS account by requiring a second form of authentication in addition to your password.

- MFA devices can be virtual (e.g., Google Authenticator) or hardware devices.
- You can enable MFA for the root user and IAM users.
- When MFA is enabled, users must provide a one-time code from their MFA device in addition to their password when signing in.
- MFA is highly recommended for the root user and any IAM users with administrative privileges.s

### IAM: Roles

IAM roles are a way to delegate access to AWS resources without sharing long-term credentials. Roles can be assumed by users, applications, or services.

- Roles are not associated with a specific user or group, but can be assumed by anyone who has permission to do so.
- Some AWS services will need to perform actions on your behalf, such as EC2 instances needing to access S3 buckets.
- You can create a role with specific permissions and then allow an AWS service to assume that role.
- Roles can be used to grant temporary access to AWS resources, which is useful for applications running on EC2 instances or Lambda functions.
- Roles can also be used to grant access to AWS resources across accounts, allowing for cross-account access.
- Common use cases for roles include:
  - Granting permissions to AWS services (e.g., EC2, Lambda) to access other AWS resources.
  - Allowing users from another AWS account to access resources in your account.
  - Providing temporary access to users or applications without sharing long-term credentials.
- Common roles include:
  - **EC2 Instance Role**: Allows EC2 instances to access AWS resources.
  - **Lambda Execution Role**: Allows Lambda functions to access AWS resources.
  - **Roles for CloudFormation**: Allows CloudFormation stacks to create and manage resources on your behalf.

### IAM: Security Tools

IAM provides several security tools to help you manage access to your AWS resources:

- **IAM Credentials Report**: A report that lists all IAM users in your account and their credentials, including access keys and MFA devices.
- **IAM Last Accessed**: A tool that shows the service permissions granted to IAM users and roles, along with the last accessed time for each service.
  - You can use this information to identify unused permissions and reduce the risk of over-permissioned users.

### IAM: Best Practices

- Do not use the root account for everyday tasks. Create an IAM user with administrative privileges instead.
- One physical user = one IAM user. Do not share IAM user accounts.
- Assign users to groups based on their job functions and grant permissions at the group level.
- Create a strong password policy and enforce MFA for all users, especially those with administrative privileges.
- Create and use Roles for giving permission to AWS services and applications, rather than using long-term credentials.
- Use Access Keys for programmatic access to AWS services, and rotate them regularly.
- Regularly review and audit IAM users, groups, roles, and policies to ensure they follow the principle of least privilege. You can use IAM Credentials Report and IAM Last Accessed to help with this.
- Use tags to organize and manage resources, and to control access based on tags.
- Enable logging and monitoring for IAM activities using AWS CloudTrail to track changes and access to your AWS resources.
- **NEVER SHARE IAM USERS AND ACCESS KEYS**.

### IAM: Summary

- IAM is a global service for managing access to AWS resources.
- It allows you to create and manage users, groups, roles, and policies.
- Users are mapped to a physical person; has a unique username and password.
- Groups are collections of users that share the same permissions.
- Policies are JSON documents that define permissions and can be attached to users, groups, or roles.
- Roles are used to delegate access to AWS resources without sharing long-term credentials.
- Security best practices include using the principle of least privilege, enforcing MFA, and regularly reviewing IAM configurations.
- AWS CLI is a command-line tool for managing AWS services.
- AWS SDKs provide programming language-specific APIs to interact with AWS services.
- Access keys are used to authenticate requests made through the AWS CLI and SDKs.
- Audit and monitor IAM activities using tools like IAM Credentials Report and IAM Last Accessed.

## AWS Access Keys, CLI, and SDKs

### How Can Users Access AWS?

Users can access AWS resources in several ways:

- **AWS Management Console**: A web-based interface for managing AWS resources.
  - Protected by passwords and MFA.
- **AWS Command Line Interface (CLI)**: A unified tool to manage AWS services from the command line.
  - Requires access keys (Access Key ID and Secret Access Key) for authentication.
- **AWS SDKs**: Software Development Kits that provide programming language-specific APIs to interact with AWS services.
  - Also requires access keys for authentication.

Access keys are generated through the AWS Management Console and consist of an Access Key ID and a Secret Access Key. These keys are used to sign programmatic requests to AWS services.

- Users manage their access keys through the IAM service.
- Access keys are secret and should not be shared or exposed in code repositories.
  - Access Key ID ~= username
  - Secret Access Key ~= password

### AWS CLI

**What is AWS CLI?**

The AWS Command Line Interface (CLI) is a unified tool that allows you to manage your AWS services from the command line. It provides a consistent interface for interacting with AWS services, making it easier to automate tasks and manage resources.

- A tool that enabled you to interact with AWS services using commands in your command-line shell.
- Direct access to the public APIs of AWS services.
- You can develop scripts to automate tasks and manage resources.
- It's open-source and available for Windows, macOS, and Linux.
- Alternative to using the AWS Management Console.

### AWS SDKs

AWS SDKs (Software Development Kits) are libraries that provide programming language-specific APIs to interact with AWS services. They simplify the process of integrating AWS services into your applications by providing pre-built functions and methods.

- AWS Software Development Kits (SDKs) are available for various programming languages, including Python (Boto3), Java, JavaScript, Ruby, and more.
- Also available for mobile and IoT devices.
- SDKs provide a higher-level abstraction over the AWS APIs, making it easier to work with AWS services in your code.
- Enables developers to access AWS services programmatically using their preferred programming language.
- Embedded in applications to interact with AWS services.
