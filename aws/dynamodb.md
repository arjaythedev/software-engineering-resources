# DynamoDB

## Overview
Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. It is designed for applications that require single-digit millisecond latency at any scale.

### Key Features
- **Fully managed** – No need to worry about infrastructure management.
- **High availability** – Data is automatically replicated across multiple Availability Zones.
- **On-demand and provisioned capacity** – Scale your workload dynamically.
- **Strong and eventual consistency models** – Choose the best fit for your use case.
- **Integrated with AWS services** – Works seamlessly with Lambda, API Gateway, and more.

## Example: Creating a DynamoDB Table Using AWS CDK (TypeScript)
Below is an example of how to create a simple DynamoDB table using AWS CDK in TypeScript:

```typescript
import * as cdk from 'aws-cdk-lib';
import * as dynamodb from 'aws-cdk-lib/aws-dynamodb';
import { Construct } from 'constructs';

export class DynamoDBStack extends cdk.Stack {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    new dynamodb.Table(this, 'MyDynamoDBTable', {
      tableName: 'MyTable',
      partitionKey: { name: 'id', type: dynamodb.AttributeType.STRING },
      billingMode: dynamodb.BillingMode.PAY_PER_REQUEST,
      removalPolicy: cdk.RemovalPolicy.DESTROY,
    });
  }
}
```

## DynamoDB Use Case: Serverless User Profile Management
A **social networking application** needs a highly scalable and fast database to store and retrieve user profiles, including usernames, bios, and follower counts. **Amazon DynamoDB** provides an efficient NoSQL solution for managing dynamic user data.

## How DynamoDB Helps
1. **Low-Latency Reads & Writes** – Ensures instant profile updates and retrievals.
2. **Scalability** – Handles millions of user profiles without performance degradation.
3. **NoSQL Flexibility** – Supports semi-structured data, making it easy to add new attributes without schema changes.
4. **Global Tables** – Allows users from different regions to access their profiles with minimal latency.
5. **Pay-Per-Use Pricing** – Cost-effective scaling based on actual usage.

By using DynamoDB, the social networking app **achieves seamless user experience with low-latency access and effortless scalability**.

## Best Practices
- **Choose the right partition key** – A well-chosen partition key ensures even data distribution and prevents performance bottlenecks. Choose a high-cardinality attribute (one with many unique values) to distribute requests evenly across partitions. Avoid "hot partitions," which can cause throttling and increased latency.
- **Use secondary indexes wisely** – Global and local secondary indexes allow for efficient querying of non-primary key attributes. However, indexes consume additional read and write capacity, so only create them when necessary. Optimize queries to minimize index scans and maximize efficiency.
- **Monitor performance** – Use AWS CloudWatch metrics such as **ConsumedReadCapacityUnits**, **ConsumedWriteCapacityUnits**, **ThrottledRequests**, and **Latency** to track your table's performance. Enable AWS CloudTrail for auditing API calls and detect anomalies.
- **Enable point-in-time recovery** – This feature provides continuous backups, allowing you to restore your table to any point within the last 35 days. This is crucial for disaster recovery and accidental data deletion scenarios. Enable it in the table settings to ensure data resilience.

## Additional Resources
- [DynamoDB Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/)
- [AWS CDK Documentation](https://docs.aws.amazon.com/cdk/latest/guide/home.html)
- [Best Practices Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html)

