[`← Home`](./README.md) **.** [`Next: Phase 2 →`](phase2-main.md)
# Phase 1 –  S3 Hands-On Project (trying out the console)

## Overview
This project documents my hands-on learning of Amazon S3 using the AWS Management Console. The goal was to understand core S3 concepts including storage, versioning, metadata, and static website hosting.

## 1. Bucket & Object Management

- Created an S3 bucket `s3-ruth-demo-bucket`   
- Created a folder `project-alpha` inside the bucket  
- Uploaded files into the folder:
  - `s3demo.txt` file  
  - `s3demo.png` image  

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
S3 does not overwrite files, it stores multiple versions, allowing recovery of deleted or modified objects.

## 3. Object Metadata

- Uploaded an HTML file `new.html`
- Added custom metadata before upload:

Key: `s3demo`

Value: `website`

### Takeaway
Metadata can be used to store additional information for filtering, automation, or analytics.

## 4. Static Website Hosting (Public Access Method)

- Uploaded an HTML file
- Temporarily allowed public access
- Enabled Static Website Hosting on the bucket  
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
- Did not enable WAF (currently using free-tier)
- Selected Origin access control settings (recommended) to ensure the S3 bucket remains private and only accessible via CloudFront
- Set default root object to: `new.html`
- Created the distribution  
- Verification: Copied the Distribution domain name `d1lzpm1e2bma0y.cloudfront.net` and confirmed the HTML site loaded securely over HTTP
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

### Screenshots (Drop down to see images)

<details>
<summary><b>1. Bucket overview and versioning enabled</b> </summary>
<img width="1890" height="749" alt="image" src="https://github.com/user-attachments/assets/038b1084-ec7d-498e-be68-46cc4ccecdc4" />
 />
<img width="1896" height="743" alt="image" src="https://github.com/user-attachments/assets/051951e6-e393-4c94-b248-b0fcb78beca9" />
</details>

<details>
<summary><b>2. Objects view</b> </summary>
<img width="1892" height="754" alt="image" src="https://github.com/user-attachments/assets/d1d86afb-cdfd-4e37-8deb-df008ea0a2db" />
<img width="1453" height="668" alt="Screenshot 2026-04-13 134943" src="https://github.com/user-attachments/assets/bbdfaed5-1b9a-4911-9105-af901de5cc82" />
</details>


<details>
<summary><b>3. Versioning demonstration</b> </summary>
<img width="1889" height="746" alt="image" src="https://github.com/user-attachments/assets/c2ff27b7-e16d-4ec4-a37e-76036927463b" />
</details>

<details>
<summary><b>4. Metadata on the html file</b> </summary>
<img width="1902" height="421" alt="image" src="https://github.com/user-attachments/assets/5e61b897-6ae1-404e-9b93-dd0399d3bb60" />
</details>

<details>
<summary><b>5. Public website</b> </summary>
<img width="1882" height="739" alt="image" src="https://github.com/user-attachments/assets/3f81219a-1677-4140-bc53-42fa840013da" />
<img width="1902" height="749" alt="image" src="https://github.com/user-attachments/assets/6e2d9bfe-c1d0-4c9b-973b-165d19ec5aea" />
<img width="1900" height="921" alt="image" src="https://github.com/user-attachments/assets/4577c211-7f76-463a-828d-c040f3eb58b1" />
</details>

<details>
<summary><b>5. problem encountered and how i solved it</b> </summary>
  
   - I hit a 404 error because my index file was stored inside a folder. After realizing S3 resolves requests based on the exact object path, I corrected the configuration and the site loaded properly.

<img width="1910" height="325" alt="Screenshot 2026-04-13 144441" src="https://github.com/user-attachments/assets/e8dfdada-ff86-40b1-aa66-40d18c5e7eff" />

<img width="1885" height="673" alt="Screenshot 2026-04-13 145008" src="https://github.com/user-attachments/assets/6374d76c-5b5f-4ff8-8850-73517bdc6abe" />
</details>

<details>
<summary><b>6. CloudFront website</b> </summary>
<img width="1815" height="931" alt="image" src="https://github.com/user-attachments/assets/bd331556-69ee-453e-9bb2-5b201d366219" />
</details>

<details>
<summary><b>5. problem encountered on cloud front and how i solved it</b> </summary>
  
   - I ran into an issue where opening the CloudFront domain on its own showed an error instead of loading my website. After checking the configuration, I realised the root URL wasn’t pointing to any file, so I set the default root object to new.html. Once updated and deployed, the site loaded correctly.

<img width="1901" height="238" alt="Screenshot 2026-04-14 120523" src="https://github.com/user-attachments/assets/b570856c-a289-4f38-a32c-ca2cda374db4" />
<img width="1894" height="315" alt="image" src="https://github.com/user-attachments/assets/be959cd8-bc1d-405a-bfca-42fdea100698" />
</details>

[`← Home`](./README.md) **.** [`Next: Phase 2 →`](phase2-main.md)
