[`← Home`](./README.md) **.** [`Next: Phase 2 →`](phase2-main.md)
# Phase 1 –  S3 Hands-On Project (trying out the console)

## Overview
This project documents my hands-on learning of Amazon S3 using the AWS Management Console. The goal was to understand core S3 concepts including storage, versioning, metadata, and static website hosting.

## 1. Bucket & Object Management

- Created an S3 bucket `s3-ruth-demo-bucket`  
- Uploaded files into the bucket:
  - `s3demo.txt` file  
  - `s3demo.png` image  
- Created a folder inside the bucket  
- Uploaded a file into the folder  

### Takeaway
Verified that the object key follows the structure: folder-name/file-name

## 2. Versioning

- Enabled versioning from the bucket settings  
- Uploaded a file, then modified it locally and uploaded it again  
- Enabled “Show Versions” to view:
  - Old version  
  - New version  
- Deleted the file and confirmed:
  - A delete marker was created  
  - Previous versions were still recoverable  

### Takeaway
S3 does not overwrite files—it stores multiple versions, allowing recovery of deleted or modified objects.

## 3. Object Metadata

- Uploaded an HTML file  
- Added custom metadata before upload:

Key: s3demo

Value: website

### Takeaway
Metadata can be used to store additional information for filtering, automation, or analytics.

## 4. Static Website Hosting (Public Access Method)

- Enabled Static Website Hosting on the bucket  
- Uploaded an HTML file  
- Added a bucket policy (JSON) to allow public access  
- Accessed the site using the bucket website endpoint URL  

### Result
Successfully hosted a static website directly from S3.

## 5. Secure Website Hosting (CloudFront Method)

Instead of making the bucket public:

- Kept “Block all public access” enabled
- Disabled Static Website Hosting on the bucket  
- Used CloudFront as a CDN in front of the bucket  

### Steps

- Created a CloudFront distribution:
  - Name: `ruth-website-dstr`
  - Description: My first secure S3 website
  - Distribution type: Single website or app
  - Origin Selection: Selected the S3 bucket `s3-ruth-demo-bucket` as the origin 
- Selected the S3 bucket as origin  
- Did not enable WAF (free-tier consideration)  
- Set default root object to: `new.html`
- Created the distribution  
- Verification: Copied the Distribution domain name `d2ucilamekaqxk.cloudfront.net` and confirmed the HTML site loaded securely over HTTP
- Infrastructure Cleanup: Successfully Disabled the distribution as the required first step before final deletion

### Result
Successfully served the website securely without exposing the S3 bucket publicly.

## Key Skills Demonstrated

- S3 bucket and object management  
- Folder structure and object keys  
- Versioning and recovery  
- Metadata usage  
- Static website hosting (public and secure methods)  
- Basic understanding of CDN integration with S3  

## What I Learned

- S3 versioning prevents permanent data loss  
- Public access must be carefully controlled  
- Metadata adds flexibility for managing objects  
- CloudFront allows secure content delivery without exposing S3 directly  

[`← Home`](./README.md) **.** [`Next: Phase 2 →`](phase2-main.md)
