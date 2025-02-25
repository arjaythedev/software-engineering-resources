# AWS SNS

## Overview
Amazon Simple Notification Service (SNS) is a fully managed messaging service that enables applications, users, and services to communicate using **publish/subscribe (pub/sub) messaging**. It allows for sending messages to multiple subscribers, including **email, SMS, Lambda functions, and SQS queues**.

### Key Features
- **Pub/Sub Messaging Model** – Supports one-to-many message broadcasting.
- **Multiple Protocols** – Deliver messages via Email, SMS, HTTP, SQS, and Lambda.
- **Message Filtering** – Enable subscribers to receive only relevant messages.
- **Event-Driven Architecture** – Trigger notifications based on AWS events.
- **Encryption & Security** – Supports message encryption and IAM policies.

## Example: Creating an SNS Topic Using AWS CDK (TypeScript)
Below is an example of how to create an SNS topic and subscribe an email endpoint using AWS CDK in TypeScript:

```typescript
import * as cdk from 'aws-cdk-lib';
import * as sns from 'aws-cdk-lib/aws-sns';
import * as sns_subscriptions from 'aws-cdk-lib/aws-sns-subscriptions';
import { Construct } from 'constructs';

export class SNSStack extends cdk.Stack {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    const topic = new sns.Topic(this, 'MySNSTopic', {
      displayName: 'My Application Notifications',
    });

    topic.addSubscription(new sns_subscriptions.EmailSubscription('example@example.com'));
  }
}
```

## Use Case Example: Alerting System for Application Failures
Imagine you run an **e-commerce website** and want to be notified whenever an order fails due to a **payment processing issue**.

### How SNS Helps:
1. **Create an SNS Topic** – `OrderFailureTopic` to send failure notifications.
2. **Publish Failure Events** – The payment system sends failure messages to the topic.
3. **Subscribe Multiple Endpoints** – Notify developers via **Email**, log failures in **SQS**, and trigger **AWS Lambda** to retry failed payments.
4. **Filter Messages** – Only send critical failure alerts to on-call engineers.

With SNS, you ensure that failure notifications are **timely, reliable, and scalable**.

## SNS Message Filtering
SNS allows **message filtering** so that subscribers receive only relevant notifications.

### Example: Filter Orders Based on Payment Status
```json
{
  "orders": {
    "payment_status": ["FAILED"]
  }
}
```
With this filter policy, a subscriber will only receive messages where `payment_status` is `FAILED`, reducing unnecessary notifications.

## SNS Security Best Practices
- **Use IAM Policies** – Restrict SNS topic access to authorized users/services.
- **Enable Encryption** – Use **AWS KMS** for message encryption.
- **Apply Message Filtering** – Reduce unwanted notifications for subscribers.
- **Monitor with CloudWatch** – Track message delivery status and failures.
- **Enable Dead Letter Queues (DLQs)** – Capture undelivered messages for debugging.

## Additional Resources
- [AWS SNS Documentation](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)
- [AWS CDK Documentation](https://docs.aws.amazon.com/cdk/latest/guide/home.html)
- [Best Practices for SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-best-practices.html)

