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

## Best Practices
- **Choose the right partition key** – Ensures even data distribution.
- **Use secondary indexes wisely** – Optimize query performance.
- **Monitor performance** – Use AWS CloudWatch for insights.
- **Enable point-in-time recovery** – Protect against accidental data loss.

## Additional Resources
- [DynamoDB Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/)
- [AWS CDK Documentation](https://docs.aws.amazon.com/cdk/latest/guide/home.html)
- [Best Practices Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html)

