# AWS EC2

## Overview
Amazon Elastic Compute Cloud (EC2) provides scalable compute capacity in the cloud, allowing users to run virtual machines with various configurations. It supports different instance types optimized for computing, memory, and storage workloads.

### Key Features
- **Flexible Instance Types** – Choose from general-purpose, compute-optimized, memory-optimized, and storage-optimized instances.
- **Auto Scaling** – Automatically scale EC2 instances based on demand.
- **Elastic Load Balancing (ELB)** – Distribute incoming traffic across multiple instances.
- **Secure Access** – Use IAM roles, security groups, and key pairs for access control.
- **Multiple Purchase Options** – On-Demand, Reserved, Spot, and Savings Plans to optimize costs.

## Example: Creating an EC2 Instance Using AWS CDK (TypeScript)
Below is an example of how to create an EC2 instance using AWS CDK in TypeScript:

```typescript
import * as cdk from 'aws-cdk-lib';
import * as ec2 from 'aws-cdk-lib/aws-ec2';
import { Construct } from 'constructs';

export class EC2Stack extends cdk.Stack {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    const vpc = new ec2.Vpc(this, 'MyVPC', {
      maxAzs: 2,
    });

    new ec2.Instance(this, 'MyEC2Instance', {
      instanceType: ec2.InstanceType.of(ec2.InstanceClass.T3, ec2.InstanceSize.MICRO),
      machineImage: ec2.MachineImage.latestAmazonLinux2(),
      vpc,
    });
  }
}
```

## EC2 Instance Types
EC2 provides multiple instance types suited for different workloads:
- **General Purpose (e.g., t3, m5)** – Balanced CPU, memory, and networking.
- **Compute Optimized (e.g., c5, c6g)** – Ideal for high-performance computing.
- **Memory Optimized (e.g., r5, x1e)** – Suitable for in-memory databases.
- **Storage Optimized (e.g., i3, d2)** – Designed for high disk throughput.
- **GPU Instances (e.g., p3, g4dn)** – Best for machine learning and graphics processing.

## Security and Access Control
- **Security Groups** – Control inbound and outbound traffic at the instance level.
- **IAM Roles** – Grant fine-grained access permissions to EC2 instances.
- **Key Pairs** – Secure SSH access using public/private key authentication.
- **VPC Isolation** – Run instances in private subnets for enhanced security.

## EC2 Auto Scaling
EC2 Auto Scaling ensures that instances dynamically adjust to traffic demands.
- **Scale-in and scale-out policies** – Automatically adjust instance count.
- **Scheduled scaling** – Define specific times to scale resources.
- **Spot Fleet Management** – Automatically replaces interrupted Spot Instances.

## EC2 Pricing Models
- **On-Demand** – Pay for compute capacity per hour/second with no long-term commitments.
- **Reserved Instances** – Commit to a term (1 or 3 years) for a significant discount.
- **Spot Instances** – Purchase unused EC2 capacity at a steep discount.
- **Savings Plans** – Flexible pricing model for long-term cost savings.

## Best Practices
- **Use Auto Scaling Groups** – Maintain high availability and scale efficiently.
- **Leverage Spot and Reserved Instances** – Optimize cost by mixing different pricing models.
- **Enable Monitoring and Logging** – Use AWS CloudWatch and CloudTrail for insights.
- **Harden Security** – Restrict access with IAM policies and security groups.
- **Automate with Infrastructure as Code (IaC)** – Use AWS CDK, Terraform, or CloudFormation.

## Additional Resources
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/index.html)
- [Instance Type Guide](https://aws.amazon.com/ec2/instance-types/)
- [Best Practices for EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-best-practices.html)
- [Auto Scaling Documentation](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)

