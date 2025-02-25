# AWS RDS

## Overview
Amazon Relational Database Service (RDS) is a managed database service that makes it easy to set up, operate, and scale relational databases in the cloud. It supports multiple database engines, including **MySQL, PostgreSQL, MariaDB, Oracle, and Microsoft SQL Server**.

### Key Features
- **Fully managed** – Automated backups, patching, and scaling.
- **Multi-AZ Deployment** – Provides high availability and failover support.
- **Read Replicas** – Improves performance by offloading read queries.
- **Encryption** – Supports encryption at rest and in transit.
- **Performance Insights** – Helps monitor and optimize database performance.

## Example: Creating an RDS Instance Using AWS CDK (TypeScript)
Below is an example of how to create an RDS instance using AWS CDK in TypeScript:

```typescript
import * as cdk from 'aws-cdk-lib';
import * as rds from 'aws-cdk-lib/aws-rds';
import * as ec2 from 'aws-cdk-lib/aws-ec2';
import { Construct } from 'constructs';

export class RDSStack extends cdk.Stack {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    const vpc = new ec2.Vpc(this, 'MyVPC', { maxAzs: 2 });

    new rds.DatabaseInstance(this, 'MyRDSInstance', {
      engine: rds.DatabaseInstanceEngine.postgres({ version: rds.PostgresEngineVersion.V14 }),
      instanceType: ec2.InstanceType.of(ec2.InstanceClass.BURSTABLE3, ec2.InstanceSize.MICRO),
      vpc,
      allocatedStorage: 20,
      multiAz: true,
      publiclyAccessible: false,
      deletionProtection: false,
    });
  }
}
```

## Use Case Example: Setting Up a Student Management System
Imagine you're a high school administrator looking to **manage student records, grades, and attendance** efficiently. Instead of maintaining physical records, you want to use a **relational database** to store and retrieve student information securely.

### How RDS Helps:
1. **Structured Data Storage**: Store student details, grades, and attendance in a structured format using **MySQL or PostgreSQL**.
2. **High Availability**: Multi-AZ deployment ensures that the database remains accessible even if one server fails.
3. **Automated Backups**: Helps recover lost data in case of accidental deletion.
4. **Scalability**: Can handle thousands of student records and grow as needed.
5. **Security**: Access can be restricted to school staff with **IAM and security groups**.

By using AWS RDS, the school can focus on managing students instead of dealing with database maintenance.

## RDS Storage Types
AWS RDS provides different storage types optimized for various use cases:
- **General Purpose SSD (gp2/gp3)** – Balanced price-performance for everyday workloads.
- **Provisioned IOPS (io1/io2)** – Designed for high-performance applications with low-latency.
- **Magnetic Storage** – Legacy option, generally not recommended for new applications.

## Security Best Practices
- **Enable encryption** – Protect sensitive data with AWS Key Management Service (KMS).
- **Use IAM roles** – Restrict database access to authorized users and services.
- **Implement VPC isolation** – Deploy RDS within a private subnet.
- **Enable automated backups** – Retain backups for disaster recovery.

## Additional Resources
- [AWS RDS Documentation](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- [AWS CDK Documentation](https://docs.aws.amazon.com/cdk/latest/guide/home.html)
- [Best Practices for RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_BestPractices.html)

