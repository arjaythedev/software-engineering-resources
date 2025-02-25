# AWS API Gateway

## Overview
AWS API Gateway is a fully managed service that makes it easy to create, publish, maintain, monitor, and secure APIs at any scale. It allows you to create RESTful and WebSocket APIs that integrate with AWS Lambda, DynamoDB, and other AWS services.

### Key Features
- **Supports REST and WebSocket APIs** – Build scalable APIs for various applications.
- **Integration with AWS services** – Easily connect APIs to Lambda, DynamoDB, and other AWS services.
- **Security and access control** – Supports IAM, Cognito, and API keys for authentication.
- **Throttling and rate limiting** – Protect APIs from excessive traffic and abuse.
- **Monitoring and logging** – Uses AWS CloudWatch for tracking metrics and debugging.

## Example: Creating an API Gateway with AWS CDK (TypeScript)
Below is an example of how to create an API Gateway using AWS CDK in TypeScript:

```typescript
import * as cdk from 'aws-cdk-lib';
import * as apigateway from 'aws-cdk-lib/aws-apigateway';
import * as lambda from 'aws-cdk-lib/aws-lambda';
import { Construct } from 'constructs';

export class ApiGatewayStack extends cdk.Stack {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    const myLambda = new lambda.Function(this, 'MyLambdaFunction', {
      functionName: 'MyFunction',
      runtime: lambda.Runtime.NODEJS_18_X,
      handler: 'index.handler',
      code: lambda.Code.fromAsset('lambda'),
    });

    const api = new apigateway.RestApi(this, 'MyApi', {
      restApiName: 'MyServiceApi',
      description: 'This API serves as an example.',
    });

    const lambdaIntegration = new apigateway.LambdaIntegration(myLambda);

    const resource = api.root.addResource('myresource');
    resource.addMethod('GET', lambdaIntegration);
  }
}
```

## Deployment Models
- **Edge-optimized APIs** – Best for APIs that serve global traffic; integrates with AWS CloudFront.
- **Regional APIs** – Ideal for applications within a specific AWS region.
- **Private APIs** – Accessible only within an Amazon VPC.

## Security and Access Control
- **IAM Policies** – Control access to API Gateway resources using AWS IAM roles.
- **Amazon Cognito** – Authenticate users with Cognito User Pools.
- **API Keys and Usage Plans** – Control access and rate limiting for different client applications.
- **Lambda Authorizers** – Use custom authentication logic before processing requests.

## Performance Optimization
- **Enable caching** – Reduce request latency by caching responses at the API Gateway level.
- **Use throttling and rate limiting** – Prevent abuse and ensure fair usage among clients.
- **Optimize payload sizes** – Reduce response time by minimizing data transfer.

## Monitoring and Logging
- **Enable AWS CloudWatch Logs** – Track API execution details and errors.
- **Use AWS X-Ray** – Debug and analyze API performance with request tracing.
- **Set up alarms** – Create CloudWatch alarms to notify on API latency and errors.

## Best Practices
- **Use separate stages (e.g., dev, test, prod)** – Manage API versions effectively.
- **Implement request validation** – Validate inputs before processing to prevent malformed requests.
- **Enable CORS (Cross-Origin Resource Sharing)** – Allow requests from different domains if needed.
- **Leverage API Gateway’s built-in authorization features** – Minimize security risks.

## Additional Resources
- [AWS API Gateway Documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)
- [AWS CDK Documentation](https://docs.aws.amazon.com/cdk/latest/guide/home.html)
- [Best Practices for API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/best-practices.html)

