[`← S3-Lambda Integration`](s3-lambda.md) **.** [`Main Home`](./README.md) **.** [`Phase 1 Home`](phase1-main.md) **.** [`Next: Monitoring & Audit (CloudTrail & Logs)`](monitoring-audit-s3.md) 

# Cross-Region Replication (Disaster Recovery Setup)

## Project Overview
I configured Amazon S3 Cross-Region Replication to demonstrate a basic disaster recovery and data redundancy strategy in AWS. The objective was to ensure that objects uploaded to a primary S3 bucket are automatically replicated to a secondary bucket located in a different AWS region.

This setup simulates a real-world high availability architecture where data remains accessible even if a primary region experiences failure. It demonstrates how AWS can be used to improve resilience, durability, and fault tolerance of cloud storage systems.

## Architecture Components

- **Amazon S3 (Source Bucket)** – primary storage location where objects are uploaded
- **Amazon S3 (Destination Bucket)** – replica bucket in a different AWS region
- **IAM Role (Replication Role)** – grants S3 permission to replicate objects between buckets
- **S3 Cross-Region Replication** – managed AWS feature used to automate replication

## Replication Flow

Source S3 Bucket → Object Upload → Replication Rule Trigger → Destination S3 Bucket (Different Region)

## Configuration Setup

### Source Bucket Configuration
The source bucket `s3-ruth-demo-bucket` was configured as the primary storage location for uploaded objects. Versioning was enabled to allow replication of object changes.

### Destination Bucket Configuration
A second S3 bucket `s3-ruth-demo-replica-bucket` was created in a different AWS region (`US West (Oregon) us-west-2`) to serve as the disaster recovery replica. This bucket receives automatically replicated objects from the source bucket.

### IAM Replication Role
An IAM role `s3-crr-replication-role` was created to allow Amazon S3 to replicate objects between buckets. The role included permissions for:

- Reading objects from the source bucket
- Writing objects to the destination bucket

## Replication Rule Configuration

A replication rule `crr-replication-rule` was configured on the source bucket with the following settings:

- Status: Enabled
- Scope: Entire bucket (all objects)
- Destination: Secondary S3 bucket `s3-ruth-demo-replica-bucket` in a different region `US West (Oregon) us-west-2`
- IAM Role: Assigned replication role `s3-crr-replication-role`

## Testing and Validation

A test file `s3replication-demo.txt` was uploaded to the source S3 bucket to validate the replication process.

### Expected Behaviour:
- File uploaded to source bucket
- S3 automatically triggers replication rule
- Object is copied to destination bucket in a different region

### Result:
The object was successfully replicated to the destination bucket, confirming that Cross-Region Replication was functioning correctly and that data redundancy had been achieved.

## Key Concepts Demonstrated

- Cross-Region Replication in Amazon S3
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

### Screenshots 
The following screenshots document the full Cross-Region Replication setup and validation process (drop down to see images):

<details>
<summary><b>1. Source and destination S3 buckets with versioning enabled </b> </summary>
<img width="1892" height="603" alt="Screenshot 2026-05-04 202111" src="https://github.com/user-attachments/assets/cf264b63-accb-4db1-8506-bf8e5604a661" />
<img width="1886" height="604" alt="Screenshot 2026-05-04 202051" src="https://github.com/user-attachments/assets/a8852559-a940-424a-8f87-938c3fbd06ad" />
</details>

<details>
<summary><b>2. IAM role created for S3 replication permissions</b> </summary>
<img width="1878" height="473" alt="Screenshot 2026-05-04 212219" src="https://github.com/user-attachments/assets/91675776-ff85-4f69-93f9-681e94f9b41f" />
<img width="1863" height="369" alt="Screenshot 2026-05-04 212230" src="https://github.com/user-attachments/assets/e0e5022f-fa91-40f4-9e66-77bf295ab913" />
</details>

<details>
<summary><b>3. Replication rule configuration on the source bucket</b> </summary>
<img width="1891" height="702" alt="Screenshot 2026-05-04 212543" src="https://github.com/user-attachments/assets/62d20808-caa8-4268-8baf-84728d4ac90e" />
<img width="1863" height="418" alt="Screenshot 2026-05-04 212632" src="https://github.com/user-attachments/assets/6d0e8145-b3e4-4b2b-bc6d-19cc48b08598" />
<img width="1865" height="556" alt="Screenshot 2026-05-04 212645" src="https://github.com/user-attachments/assets/8afa8325-4e04-494b-a843-c5f7e1b531c3" />
<img width="1885" height="391" alt="Screenshot 2026-05-04 213053" src="https://github.com/user-attachments/assets/6228106b-07e8-4a2a-9678-19cb956d209f" />
<img width="1861" height="332" alt="Screenshot 2026-05-04 213216" src="https://github.com/user-attachments/assets/8acd216c-0188-4588-872b-764ba7948e05" />
<img width="1865" height="614" alt="Screenshot 2026-05-04 213238" src="https://github.com/user-attachments/assets/067364c1-14d5-4be8-9533-1d0daa7ae148" />
</details>

<details>
<summary><b>4. Test file uploaded to the source bucket</b> </summary>
<img width="1887" height="578" alt="Screenshot 2026-05-04 213505" src="https://github.com/user-attachments/assets/f5ac77c8-3345-49d7-8103-a1ec4db2fe3a" />
</details>

<details>
<summary><b>5. Replicated file successfully appearing in the destination bucket</b> </summary>
<img width="1907" height="592" alt="Screenshot 2026-05-04 213523" src="https://github.com/user-attachments/assets/db568ded-b2ae-4555-9a56-850463ca4fa6" />
</details>

[`← S3-Lambda Integration`](s3-lambda.md) **.** [`Main Home`](./README.md) **.** [`Phase 1 Home`](phase1-main.md) **.** [`Next: Cross-Region Replication →`](cross-region-replication.md)
