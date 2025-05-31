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
