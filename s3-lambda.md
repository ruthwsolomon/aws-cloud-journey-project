# S3 Event-Driven System (S3 → Lambda)

## Overview
This project demonstrates how I connected Amazon S3 with AWS Lambda to build a simple event-driven workflow. The goal was to understand how AWS services can automatically react to events without manual intervention.

## What I Did

- Created a Lambda function `ruth-s3-trigger-fn`
- Configured my S3 bucket `s3-ruth-demo-bucket` to trigger the Lambda function on file upload 
- Uploaded a test file to the bucket to trigger the workflow
- Verified execution by checking logs in CloudWatch

## Result
Each time a file is uploaded to the S3 bucket, the Lambda function is automatically triggered and processes the event. In this case, it logs the file name and bucket details.

## Lessons Learned

- S3 can trigger other AWS services based on events (like file uploads)  
- Lambda allows you to run code without managing servers (serverless)  
- Event-driven architecture removes the need for manual processes  
- CloudWatch logs are useful for verifying and debugging workflows  

## Real-World Use Case

This pattern is commonly used in:

- File processing systems (e.g. image resizing after upload)  
- Data pipelines  
- Automated workflows triggered by user uploads  

## Key Takeaway

Instead of manually handling files after upload, S3 can automatically trigger Lambda to perform actions. This demonstrates how AWS enables scalable, event-driven architectures.
