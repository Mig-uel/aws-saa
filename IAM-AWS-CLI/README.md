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
