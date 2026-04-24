[`← Home` ](./README.md) **.** [`Next: Website Hosting and versioning →`](static-website-et.al.md)
# Phase 1  

## AWS S3: Storage, Security & Data Management

This phase documents my hands-on exploration of Amazon S3 using the AWS Management Console. The focus was on understanding how data is stored, secured, accessed, and managed in real-world cloud environments by implementing core features and practical access patterns.

## Accomplishments:

- [Static Website Hosting, Versioning & CloudFront Security](static-website-et.al.md) – I built a static website using S3, first by enabling public access and then by implementing a more secure architecture using CloudFront with Origin Access Control (OAC). I also worked with versioning and metadata to understand data protection and object-level configuration.
- [Pre-Signed URL System (Secure Access)](presignesURL.md) – I implemented a secure file access pattern by generating pre-signed URLs, allowing temporary access to private objects without making the bucket public. This demonstrated how controlled access is handled in real-world applications.
- [Lifecycle & Cost Optimisation](lifecycle-policies.md) – I configured lifecycle rules to automatically transition objects between storage classes (STANDARD → IA → GLACIER), demonstrating how S3 can be used to manage storage costs over time.
- [Event-Driven Architecture (S3 → Lambda)](s3-lambda.md)– I built a basic event-driven workflow where uploading a file to S3 triggers a Lambda function to process the object (e.g., logging, renaming, or moving files), introducing serverless automation.
- Cross-Region Replication (Disaster Recovery) – I configured replication between buckets in different regions to simulate a disaster recovery setup, ensuring data redundancy and availability in case of regional failure.
- Monitoring & Audit (CloudTrail & Logs) – I enabled CloudTrail and explored access logs to monitor activity within S3, gaining visibility into who accessed resources and when.

**Note:** Each section links to a detailed `.md` file containing step-by-step implementation, screenshots, and explanations.
