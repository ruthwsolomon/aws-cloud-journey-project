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

### Screenshots (Drop down to see images)

<details>
<summary><b>1. Manual transition of S3 objects</b> </summary>
<img width="1435" height="244" alt="Screenshot 2026-04-24 091636" src="https://github.com/user-attachments/assets/c20aaa97-29fc-42d5-be25-bb144f129f31" />
<img width="1881" height="137" alt="Screenshot 2026-04-24 091754" src="https://github.com/user-attachments/assets/30b42c63-d671-4f5a-b224-43c80d0c62d7" />
<img width="1862" height="236" alt="Screenshot 2026-04-24 091806" src="https://github.com/user-attachments/assets/81924ae1-6e0b-4df4-bf4a-6d65cb981505" />
</details>

<details>
<summary><b>2. Implementating automated lifecycle rules</b> </summary>
<img width="1895" height="494" alt="Screenshot 2026-04-24 092651" src="https://github.com/user-attachments/assets/31283a37-e1f1-49ea-a57d-7ec3753155e8" />
<img width="1886" height="724" alt="Screenshot 2026-04-24 092704" src="https://github.com/user-attachments/assets/cd34048e-09f4-4c15-837e-6612b6b8f788" />
</details>


[`←Presigned URL`](presignedURL.md) **.** [`Main Home`](./README.md) **.** [`Phase 1 Home `](phase1-main.md) **.** [`Next: LifeCycle Policies →`](lifecycle-policies.md)
