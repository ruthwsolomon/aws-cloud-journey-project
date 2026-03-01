[← Back to Main Page](./README.md) | [Next: EC2 →](phase-main.md)
# Phase 1 – Static Website Hosting (Amazon S3)    

## Goal
Host a simple static website using Amazon S3 and make it publicly accessible on the internet.

## Architecture
- Amazon S3 bucket for storage
- Static website hosting enabled
- Bucket policy configured for public read access

## Steps Followed
1. Created an S3 bucket with a unique name
2. Disabled “Block all public access”
3. Enabled Static Website Hosting
4. Uploaded website files (index.html, etc.)
5. Added a bucket policy to allow public read access
6. Opened the website using the S3 website endpoint

## Screenshots
<img width="1914" height="818" alt="Screenshot 2026-02-23 193558" src="https://github.com/user-attachments/assets/96521bd7-5b37-41e6-918c-b4337d343f63" />
<img width="1914" height="853" alt="Screenshot 2026-02-23 193643" src="https://github.com/user-attachments/assets/230fae17-8a28-4fe1-afd3-36ed2c62ebe9" />
<img width="1914" height="857" alt="image" src="https://github.com/user-attachments/assets/8c3ae35e-9bdb-4283-9251-c78bec7b220a" />
<img width="1913" height="829" alt="Screenshot 2026-02-23 201124" src="https://github.com/user-attachments/assets/cfa56ed7-e37d-4d15-910d-4562ac6b634f" />
<img width="1919" height="951" alt="Screenshot 2026-02-23 193737" src="https://github.com/user-attachments/assets/da709b44-97dc-45d2-8907-ca3c118e4653" />

##  Lessons Learned
- S3 can host static websites without a server
- Public access must be configured carefully
- Bucket policies control who can view files
- Permissions errors (403 AccessDenied) usually mean policy or public access settings are wrong

## Outcome
Successfully hosted a live static website using Amazon S3.

[← Back to Main Page](./README.md) | [Next: EC2 →](phase-main.md)
