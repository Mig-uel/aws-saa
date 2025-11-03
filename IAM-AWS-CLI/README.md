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

## IAM: Permissions

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
