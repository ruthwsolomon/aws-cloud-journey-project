[`← LifeCycle Policies`](lifecycle-policies.md) **.** [`Main Home`](./README.md) **.** [`Phase 1 Home `](phase1-main.md) **.** [`Next: Cross-Region Replication →`](cross-region-replication.md)

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

A Lambda function named `ruth-s3-trigger-fn` was created using Python 3.14 runtime.

The function was configured with a basic execution role to allow logging via CloudWatch.

### Lambda Logic
The function processes incoming S3 event data and extracts:

- Bucket name
- Object key

This information is then printed to CloudWatch logs for verification.

## S3 Event Configuration

The S3 bucket `s3-ruth-demo-bucket` was configured with an event notification rule:

- Event type: **Object Created (PUT)**
- Destination: **AWS Lambda function**
- Target: `ruth-s3-trigger-fn`

This configuration ensures that every new file upload automatically triggers the Lambda function.

## Testing and Validation

A test file `s3demo.txt` was uploaded to the S3 bucket to validate the integration.

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

## Skills Demonstrated

- Amazon S3 event configuration
- AWS Lambda function deployment
- Serverless architecture fundamentals
- IAM role configuration for Lambda execution
- CloudWatch log monitoring and validation

## Key Learning Outcome

This project demonstrated how AWS services can be loosely coupled using event-driven design. Instead of manually processing uploaded files, the system automatically triggers compute logic when events occur, enabling scalable and automated cloud workflows without managing infrastructure.

## Architecture Evidence (Each topic drops down to a screenshot)

<details>
<summary><b>1. Lambda Function Created</b></summary>
<img width="1893" height="742" alt="image" src="https://github.com/user-attachments/assets/cd8b8cae-c281-484d-ba01-031f661425c7" />
</details>

<details>
<summary><b>2. Lambda Code (Inside Function)</b></summary>
<img width="1890" height="738" alt="Screenshot 2026-05-04 192123" src="https://github.com/user-attachments/assets/0fceaaf3-252f-4353-b2f7-cf7aca5232f5" />
</details>

<details>
<summary><b>3. S3 Event Notification Setup</b></summary>
<img width="1913" height="328" alt="Screenshot 2026-05-04 193640" src="https://github.com/user-attachments/assets/4f17b135-abeb-4075-8330-abd11ec411ce" />
<img width="1898" height="313" alt="Screenshot 2026-05-04 193648" src="https://github.com/user-attachments/assets/828f5a34-03a5-4ba4-baa7-6eb00c84eb9a" />
<img width="1888" height="534" alt="Screenshot 2026-05-04 193701" src="https://github.com/user-attachments/assets/f30602cf-1ad6-4d58-85a5-624ad9788662" />
<img width="1879" height="719" alt="Screenshot 2026-05-04 192414" src="https://github.com/user-attachments/assets/b3f2efaa-ed2c-408c-8ca7-a4480d47348e" />
</details>

<details>
<summary><b>4. Test File Upload in S3</b></summary>
<img width="1878" height="531" alt="image" src="https://github.com/user-attachments/assets/daa0a5ee-c26d-4a31-b299-73309418698c" />
</details>

<details>
<summary><b>5. CloudWatch Logs (PROOF IT WORKED)</b></summary>
<img width="1896" height="732" alt="image" src="https://github.com/user-attachments/assets/f0a092ba-de84-47e4-9203-3f51b3ead36c" />
</details>


[`← LifeCycle Policies`](lifecycle-policies.md) **.** [`Main Home`](./README.md) **.** [`Phase 1 Home `](phase1-main.md) **.** [`Next: Cross-Region Replication →`](cross-region-replication.md)
