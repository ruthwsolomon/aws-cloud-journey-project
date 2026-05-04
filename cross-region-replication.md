[`← S3-Lambda Integration`](s3-lambda.md) **.** [`Main Home`](./README.md) **.** [`Phase 1 Home`](phase1-main.md) **.** [`Next: Cross-Region Replication →`](cross-region-replication.md)

# Cross-Region Replication (Disaster Recovery Setup)

## Project Overview
I configured Amazon S3 Cross-Region Replication (CRR) to demonstrate a basic disaster recovery and data redundancy strategy in AWS. The objective was to ensure that objects uploaded to a primary S3 bucket are automatically replicated to a secondary bucket located in a different AWS region.

This setup simulates a real-world high availability architecture where data remains accessible even if a primary region experiences failure. It demonstrates how AWS can be used to improve resilience, durability, and fault tolerance of cloud storage systems.

## Architecture Components

- **Amazon S3 (Source Bucket)** – primary storage location where objects are uploaded
- **Amazon S3 (Destination Bucket)** – replica bucket in a different AWS region
- **IAM Role (Replication Role)** – grants S3 permission to replicate objects between buckets
- **S3 Cross-Region Replication (CRR)** – managed AWS feature used to automate replication

## Replication Flow

Source S3 Bucket → Object Upload → Replication Rule Trigger → Destination S3 Bucket (Different Region)

## Configuration Setup

### Source Bucket Configuration
The source bucket was configured as the primary storage location for uploaded objects. Versioning was enabled to allow replication of object changes.

### Destination Bucket Configuration
A second S3 bucket was created in a different AWS region to serve as the disaster recovery replica. This bucket receives automatically replicated objects from the source bucket.

### IAM Replication Role
An IAM role was created to allow Amazon S3 to replicate objects between buckets. The role included permissions for:

- Reading objects from the source bucket
- Writing objects to the destination bucket

## Replication Rule Configuration

A replication rule was configured on the source bucket with the following settings:

- Status: Enabled
- Scope: Entire bucket (all objects)
- Destination: Secondary S3 bucket in a different region
- IAM Role: Assigned replication role

## Testing and Validation

A test file `replication-test.txt` was uploaded to the source S3 bucket to validate the replication process.

### Expected Behaviour:
- File uploaded to source bucket
- S3 automatically triggers replication rule
- Object is copied to destination bucket in a different region

### Result:
The object was successfully replicated to the destination bucket, confirming that Cross-Region Replication was functioning correctly and that data redundancy had been achieved.

## Key Concepts Demonstrated

- Cross-Region Replication (CRR) in Amazon S3
- Disaster recovery and high availability design
- Data redundancy across AWS regions
- IAM role-based permissions for replication
- Versioning requirements for S3 replication
- Automated cloud data synchronization

## Skills Demonstrated

- Amazon S3 replication configuration
- Multi-region cloud architecture design
- IAM role creation and permission management
- Disaster recovery planning in AWS
- Cloud storage resilience strategies

## Key Learning Outcome

This project demonstrated how AWS S3 Cross-Region Replication can be used to build resilient storage architectures. By automatically copying data to a separate region, the system ensures business continuity and protects against regional outages or data loss scenarios.
