# AWS IAM

## Overview
AWS Identity and Access Management (IAM) is a service that helps you securely control access to AWS resources. It allows you to create and manage AWS users, groups, and roles, defining permissions using policies.

### Key Features
- **Granular Access Control** – Define fine-grained permissions for AWS resources.
- **IAM Roles and Policies** – Assign permissions dynamically to users, applications, and services.
- **Multi-Factor Authentication (MFA)** – Add an extra layer of security for user sign-ins.
- **Federated Access** – Enable single sign-on (SSO) with external identity providers.
- **Auditing and Compliance** – Track IAM changes and access logs with AWS CloudTrail.

## Example: Creating an IAM Role Using AWS CDK (TypeScript)
Below is an example of how to create an IAM role using AWS CDK in TypeScript:

```typescript
import * as cdk from 'aws-cdk-lib';
import * as iam from 'aws-cdk-lib/aws-iam';
import { Construct } from 'constructs';

export class IAMStack extends cdk.Stack {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    new iam.Role(this, 'MyIAMRole', {
      assumedBy: new iam.ServicePrincipal('ec2.amazonaws.com'),
      managedPolicies: [
        iam.ManagedPolicy.fromAwsManagedPolicyName('AmazonS3ReadOnlyAccess')
      ],
    });
  }
}
```

## Use Case Example: Securing an Application
Imagine you have an **online blogging platform** hosted on **EC2**, and you need to allow the application to read from an **S3 bucket** without giving full AWS account access.

### How IAM Helps:
1. **Create an IAM Role** – Assign an IAM role to the EC2 instance.
2. **Attach Permissions** – Use an AWS managed policy like `AmazonS3ReadOnlyAccess` to allow read access.
3. **Secure the Application** – The EC2 instance can now access S3 **without hardcoding credentials** in the application.
4. **Audit and Track Access** – Use AWS CloudTrail to monitor IAM access and changes.

By implementing IAM roles, you reduce security risks and improve access management.

## IAM Best Practices
- **Follow the Principle of Least Privilege** – Grant only the permissions necessary for a task.
- **Use IAM Roles Instead of Long-Term Access Keys** – Avoid storing credentials in applications.
- **Enable Multi-Factor Authentication (MFA)** – Add an extra security layer for users.
- **Rotate Credentials Regularly** – Update IAM user passwords and keys periodically.
- **Monitor with AWS CloudTrail** – Keep track of changes and access attempts.

## IAM Policy Structure
IAM policies define permissions in JSON format. Below is an example of a simple policy that allows read-only access to an S3 bucket:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-example-bucket/*"
    }
  ]
}
```

## Additional Resources
- [AWS IAM Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/)
- [AWS CDK Documentation](https://docs.aws.amazon.com/cdk/latest/guide/home.html)
- [Best Practices for IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)

