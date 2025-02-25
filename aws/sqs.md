# AWS SQS

## Overview
Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables decoupling of microservices, distributed systems, and serverless applications. It allows reliable message delivery between components with **at-least-once delivery**, **message durability**, and **high scalability**.

### Key Features
- **Standard & FIFO Queues** – Choose between high-throughput or ordered message processing.
- **Message Durability** – Messages are stored across multiple AWS Availability Zones.
- **Scalability** – Supports an unlimited number of messages per second.
- **Dead-Letter Queues (DLQs)** – Capture messages that fail to be processed.
- **Long Polling & Delay Queues** – Optimize message retrieval to reduce costs.

## Example: Creating an SQS Queue Using AWS CDK (TypeScript)
Below is an example of how to create an SQS queue using AWS CDK in TypeScript:

```typescript
import * as cdk from 'aws-cdk-lib';
import * as sqs from 'aws-cdk-lib/aws-sqs';
import { Construct } from 'constructs';

export class SQSStack extends cdk.Stack {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    new sqs.Queue(this, 'MyQueue', {
      queueName: 'MyApplicationQueue',
      visibilityTimeout: cdk.Duration.seconds(30),
      retentionPeriod: cdk.Duration.days(4),
    });
  }
}
```

## Use Case Example: Order Processing System
Imagine an **e-commerce platform** where orders are placed and need to be processed asynchronously.

### How SQS Helps:
1. **Order Submission** – A user places an order, and the order details are sent to an SQS queue.
2. **Decoupling Services** – The **payment processing** and **inventory system** retrieve messages from the queue independently.
3. **Scalability** – Multiple workers consume messages in parallel, ensuring efficient processing during peak traffic.
4. **Fault Tolerance** – If a worker fails, the message remains in the queue for another worker to process.
5. **Dead-Letter Queue (DLQ)** – Unprocessed messages are moved to a DLQ for debugging and retry logic.

By using SQS, the order processing system remains **resilient, scalable, and decoupled**.

## Types of SQS Queues
- **Standard Queue** – High-throughput, at-least-once delivery, best-effort ordering.
- **FIFO Queue** – First-in-first-out processing with exactly-once message delivery.

## Best Practices
- **Enable Dead-Letter Queues (DLQs)** – Capture and analyze failed messages.
- **Use Long Polling** – Reduce empty responses and lower API costs.
- **Implement Message Deduplication** – Prevent duplicate processing in FIFO queues.
- **Monitor with CloudWatch** – Track message age, visibility timeout, and processing failures.
- **Secure with IAM Policies** – Restrict queue access to only necessary users and services.

## Additional Resources
- [AWS SQS Documentation](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html)
- [AWS CDK Documentation](https://docs.aws.amazon.com/cdk/latest/guide/home.html)
- [Best Practices for SQS](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-best-practices.html)
