# AWS Resources

Welcome to the **AWS Directory** of the **Software Engineering Resources** repository! This section provides categorized documentation, code examples, and best practices for various AWS services.

## 📂 Categories & Services

### ☁️ Compute
- **[EC2](./ec2.md)** – Virtual machines in the cloud with different instance types, pricing models, and auto-scaling capabilities.
- **[Lambda](./lambda.md)** – Serverless computing service to run code without provisioning infrastructure.
- **[ECS](./ecs.md)** – Managed container orchestration service for running Docker workloads.

### 📦 Storage & Databases
- **[S3](./s3.md)** – Scalable object storage with lifecycle policies, versioning, and Glacier for archival.
- **[RDS](./rds.md)** – Managed relational database service supporting MySQL, PostgreSQL, and more.

### 🏗️ Infrastructure as Code
- **[CloudFormation](./cloudformation.md)** – Infrastructure as Code service using YAML or JSON templates.
- **[CDK](./cloudformation.md#how-cdk-and-terraform-use-cloudformation)** – High-level abstraction that generates CloudFormation templates using programming languages.
- **[Terraform](./cloudformation.md#how-cdk-and-terraform-use-cloudformation)** – Third-party IaC tool supporting multi-cloud deployments.

### 🔀 Networking & Traffic Management
- **[Route 53](./route53.md)** – Scalable domain name system (DNS) with traffic routing and health checks.

### 🔔 Messaging & Event-Driven Architecture
- **[SNS](./sns.md)** – Pub/Sub messaging service for notifications via email, SMS, SQS, and Lambda.
- **[SQS](./sqs.md)** – Message queue service for decoupling microservices and processing tasks asynchronously.

### 🔒 Security & Access Management
- **[IAM](./iam.md)** – Identity and Access Management for AWS users, roles, and permissions.

### 📊 Monitoring & Logging
- **[CloudWatch](./cloudwatch.md)** – Collect, monitor, and analyze AWS metrics, logs, and alarms.

## 📘 What’s Inside Each File?
Each file contains:
- **Overview** – A high-level explanation of the AWS service.
- **Key Features** – Notable functionalities and benefits.
- **CDK Example** – Infrastructure as Code examples using AWS CDK in TypeScript.
- **Use Case** – A real-world scenario demonstrating how the service is used.
- **Best Practices** – Recommendations for optimizing service usage.
- **Additional Resources** – Links to official AWS documentation and best practices.

## 🛠️ How to Use This Directory
1. Browse the service categories above to find the AWS service you're interested in.
2. Click on the service name to view detailed explanations and code examples.
3. Use the provided CDK templates to deploy AWS infrastructure efficiently.

For more details on AWS services, visit the **[official AWS documentation](https://aws.amazon.com/documentation/)**. 🚀

