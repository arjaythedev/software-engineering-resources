# AWS ECS

## Overview
Amazon Elastic Container Service (ECS) is a fully managed container orchestration service that allows users to deploy, manage, and scale containerized applications. ECS supports both AWS Fargate (serverless) and EC2-based deployment models.

### Key Features
- **Supports Docker containers** – Seamlessly run and manage Docker containers at scale.
- **Flexible launch types** – Choose between Fargate (serverless) or EC2-backed clusters.
- **Integration with AWS services** – Works with AWS Load Balancer, IAM, and CloudWatch.
- **Service Auto Scaling** – Automatically adjust the number of running tasks based on demand.
- **Networking and security** – Leverage VPC networking, IAM roles, and security groups.

## Example: Creating an ECS Cluster Using AWS CDK (TypeScript)
Below is an example of how to create an ECS cluster using AWS CDK in TypeScript:

```typescript
import * as cdk from 'aws-cdk-lib';
import * as ecs from 'aws-cdk-lib/aws-ecs';
import * as ec2 from 'aws-cdk-lib/aws-ec2';
import { Construct } from 'constructs';

export class ECSStack extends cdk.Stack {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    const vpc = new ec2.Vpc(this, 'MyVPC', { maxAzs: 2 });
    
    const cluster = new ecs.Cluster(this, 'MyECSCluster', {
      vpc,
    });

    cluster.addCapacity('DefaultAutoScalingGroup', {
      instanceType: new ec2.InstanceType('t3.micro'),
    });
  }
}
```

## Use Case Example: Hosting a School Project Website
Imagine you're a high school student working on a group project where you need to build a website to showcase your research. You have a web application that your team developed using **HTML, CSS, and JavaScript**. You want to make this website accessible online so anyone can visit it.

### How ECS Helps:
1. **Containerize Your Website**: Instead of setting up a full web server manually, you package your website into a Docker container.
2. **Deploy with ECS**: You upload this container to AWS ECS, where it runs in a managed environment.
3. **Scalability**: If more students start visiting your site, ECS can automatically create more containers to handle the extra traffic.
4. **Cost Efficiency**: With AWS Fargate, you only pay when someone accesses your website, saving money compared to running a server 24/7.

By using ECS, you don't need to worry about managing servers, and you can focus on your project instead of spending time on infrastructure setup!

## ECS Launch Types
ECS provides different deployment models based on workload requirements:

- **Fargate** – Serverless compute for containers without managing EC2 instances.
- **EC2** – Uses Amazon EC2 instances to run and manage container workloads.
- **External** – Run ECS tasks on on-premises or other cloud environments.

## ECS Task Definitions
Task definitions define how a container should run in ECS, including:
- **Container Image** – The Docker image used for the task.
- **CPU & Memory Limits** – Defines how much compute power and memory the container can use.
- **Networking Mode** – Specifies communication between containers and the outside world.
- **Logging Configuration** – Uses AWS CloudWatch for monitoring container logs.

## ECS Service Auto Scaling
ECS can automatically scale services to handle varying levels of demand:
- **Target Tracking Scaling** – Adjusts tasks based on CloudWatch metrics (e.g., CPU utilization).
- **Step Scaling** – Changes capacity incrementally in response to changes in demand.
- **Scheduled Scaling** – Defines scaling actions at specific times.

## ECS Networking and Security
- **IAM Roles and Policies** – Control access to AWS resources for ECS tasks and services.
- **Security Groups** – Restrict inbound and outbound traffic to ECS instances and tasks.
- **VPC and Subnets** – Deploy ECS services within a secure and isolated VPC network.
- **AWS App Mesh** – Manage service-to-service communication securely.

## Best Practices
- **Use Fargate for serverless workloads** – Reduce operational overhead by eliminating EC2 instance management.
- **Enable logging and monitoring** – Use AWS CloudWatch and AWS X-Ray for visibility.
- **Optimize container placement** – Use task placement strategies to spread workloads efficiently.
- **Implement Auto Scaling** – Adjust ECS tasks dynamically based on demand.
- **Secure with IAM and Security Groups** – Restrict access and permissions appropriately.

## Additional Resources
- [AWS ECS Documentation](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html)
- [AWS CDK Documentation](https://docs.aws.amazon.com/cdk/latest/guide/home.html)
- [ECS Best Practices](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/best-practices.html)
