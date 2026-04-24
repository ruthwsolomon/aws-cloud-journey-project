[`←Presigned URL`](presignedURL.md) **.** [`Main Home`](./README.md) **.** [`Phase 1 Home `](phase1-main.md) **.** [`Next: LifeCycle Policies →`](lifecycle-policies.md)

# AWS LifeCycle Policies

## Overview
This project demonstrates how I optimized storage costs in S3 by first moving objects manually and then automating the process using lifecycle policies; these policies automatically transition objects between storage classes based on age, reducing costs without manual intervention.

## What I Did

### Manually
- Uploaded test files to `s3-ruth-demo-bucket`
- Manually changed object `s3demo.txt` storage class from STANDARD to STANDARD-IA to understand how storage tiers work

  **Result:** 

### Automatic
- Created a lifecycle rule `move-to-ia-rule` to automatically transition objects:
  - Day 30 → STANDARD-IA  
  - Day 66 → Glacier Flexible Retrieval

  **Result:** Objects are now automatically moved to cheaper storage classes over time without manual effort.

## Lessons Learned

- Storage class should match how often data is accessed  
- Manual changes don’t scale — lifecycle rules automate cost optimisation  
- Data doesn’t need to be deleted to reduce cost, it can be moved to cheaper storage  
- Lifecycle policies are essential for managing storage efficiently as data grows

[`←Presigned URL`](presignedURL.md) **.** [`Main Home`](./README.md) **.** [`Phase 1 Home `](phase1-main.md) **.** [`Next: LifeCycle Policies →`](lifecycle-policies.md)
