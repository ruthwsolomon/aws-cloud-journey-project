[`← LifeCycle Policies`](lifecycle-policies.md) **.** [`Main Home`](./README.md) **.** [`Phase 1 Home `](phase1-main.md) **.** [`Next: S3-Lambda →`](s3-lambda.md)

# S3 Event-Driven Architecture (S3 → Lambda Integration)

## Project Overview
I designed and implemented a basic event-driven serverless workflow using Amazon S3 and AWS Lambda. The objective was to demonstrate how AWS services can communicate through events without manual intervention or server management.

In this architecture, Amazon S3 acts as the event source, triggering a Lambda function automatically whenever a new object is uploaded. The Lambda function processes the event and logs key metadata about the uploaded file. This setup demonstrates the foundation of serverless computing and event-driven design patterns in AWS.

## Architecture Components

- **Amazon S3** – object storage service used as the event source
- **AWS Lambda** – serverless compute service used to process S3 events
- **CloudWatch Logs** – monitoring service used to capture Lambda execution output
- **IAM Role (Lambda Execution Role)** – provides Lambda with permissions to write logs and access required AWS services

## Event Flow

S3 Bucket → Object Upload (PUT Event) → Lambda Trigger → CloudWatch Logs Output

## Lambda Function Configuration

A Lambda function named `ruth-s3-trigger-fn` was created using Python 3.x runtime.

The function was configured with a basic execution role to allow logging via CloudWatch.

### Lambda Logic
The function processes incoming S3 event data and extracts:

- Bucket name
- Object key (file name)

This information is then printed to CloudWatch logs for verification.

## S3 Event Configuration

The S3 bucket `s3-ruth-demo-bucket` was configured with an event notification rule:

- Event type: **Object Created (PUT)**
- Destination: **AWS Lambda function**
- Target: `ruth-s3-trigger-fn`

This configuration ensures that every new file upload automatically triggers the Lambda function.

## Testing and Validation

A test file `test-upload.txt` was uploaded to the S3 bucket to validate the integration.

### Expected Behaviour:
- S3 detects the object upload event
- Lambda function is invoked automatically
- CloudWatch logs capture the file name and bucket details

### Result:
The Lambda function executed successfully and logged the uploaded object details in CloudWatch, confirming that the event-driven workflow was functioning correctly.

## Key Concepts Demonstrated

- Event-driven architecture using AWS services
- Serverless compute execution using AWS Lambda
- S3 event notifications and integration patterns
- IAM role-based permissions for secure service interaction
- CloudWatch logging for monitoring and debugging
- 
## Skills Demonstrated

- Amazon S3 event configuration
- AWS Lambda function deployment
- Serverless architecture fundamentals
- IAM role configuration for Lambda execution
- CloudWatch log monitoring and validation

## Key Learning Outcome

This project demonstrated how AWS services can be loosely coupled using event-driven design. Instead of manually processing uploaded files, the system automatically triggers compute logic when events occur, enabling scalable and automated cloud workflows without managing infrastructure.

[`← LifeCycle Policies`](lifecycle-policies.md) **.** [`Main Home`](./README.md) **.** [`Phase 1 Home `](phase1-main.md) **.** [`Next: S3-Lambda →`](s3-lambda.md)
