# AWS Lambda

## Overview
AWS Lambda is a serverless compute service that allows you to run code without provisioning or managing servers. It automatically scales based on the number of incoming requests and charges only for the compute time consumed.

### Key Features
- **Event-driven execution** – Triggered by AWS services such as S3, DynamoDB, API Gateway, and more.
- **Automatic scaling** – Instantly scales based on workload demand.
- **Pay-per-use pricing** – Billed based on the number of requests and execution time.
- **Supports multiple languages** – Runs code in Python, Node.js, Java, Go, Ruby, and .NET.
- **Integrated monitoring** – Works with AWS CloudWatch to log and monitor execution.

## Example: Creating an AWS Lambda Function Using AWS CDK (TypeScript)
Below is an example of how to create a simple Lambda function using AWS CDK in TypeScript:

```typescript
import * as cdk from 'aws-cdk-lib';
import * as lambda from 'aws-cdk-lib/aws-lambda';
import { Construct } from 'constructs';

export class LambdaStack extends cdk.Stack {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    new lambda.Function(this, 'MyLambdaFunction', {
      functionName: 'MyFunction',
      runtime: lambda.Runtime.NODEJS_18_X,
      handler: 'index.handler',
      code: lambda.Code.fromAsset('lambda'),
      memorySize: 128,
      timeout: cdk.Duration.seconds(5),
    });
  }
}
```

## Concurrency in AWS Lambda
Concurrency in AWS Lambda refers to the number of function instances that can be running at the same time.

### Types of Concurrency
1. **Unreserved Concurrency** – By default, Lambda scales automatically to handle incoming requests, sharing resources across functions in an account.
2. **Reserved Concurrency** – A specific number of instances are allocated to a function, ensuring availability but limiting scalability.
3. **Provisioned Concurrency** – Keeps a specified number of instances initialized and ready to handle requests immediately, reducing cold starts.

### Managing Concurrency
- Use **Provisioned Concurrency** to minimize cold start latency for critical applications.
- Configure **Reserved Concurrency** to ensure a function has dedicated capacity and prevent other functions from exhausting account-wide concurrency.
- Monitor **ConcurrentExecutions** and **Throttles** metrics in AWS CloudWatch to track function performance.

## Best Practices
- **Optimize function duration** – Reduce execution time by choosing efficient code and minimizing external API calls.
- **Set appropriate memory allocation** – More memory means more CPU power, leading to faster execution.
- **Use provisioned concurrency for high-traffic applications** – Ensures functions are warm and ready for execution.
- **Leverage environment variables** – Store configuration settings without modifying code.
- **Enable AWS X-Ray for tracing** – Helps debug and optimize function performance.

## Additional Resources
- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [AWS CDK Documentation](https://docs.aws.amazon.com/cdk/latest/guide/home.html)
- [AWS Lambda Best Practices](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)

