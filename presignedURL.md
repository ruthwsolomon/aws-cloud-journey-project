[`←S3 website hosting and versioning`](static-website-et.al.md) **.** [`Phase 1 Home →`](phase1-main.md) **.** [`Next: LifeCycle Policies →`](lifecycle-policies.md)

# PRE-SIGNED URL SYSTEM (S3 Secure Access)
## Overview
This project demonstrates how to provide temporary, secure access to private S3 objects without ever making the bucket or the files public. This is a critical security pattern used in production environments to share sensitive data or allow time-limited uploads.

## Generating the Pre-Signed URL
- Created an S3 bucket `s3-ruth-demo-bucket`
- Enabled "Block all public access" so that the bucket has no public URL, and the objects cannot be reached via standard HTTP requests without authentication.   
- Uploaded file `s3demo.txt` into the bucket then attempted to access the file's direct S3 Object URL in a browser. I received an Access Denied error, confirming the file is private.
- Used the Object Actions > Share with a pre-signed URL feature in the AWS Console.
     - Settings: **Time Interval:** 2 Minutes (to test immediate expiry).

AWS created a special link that has a built-in timer. This link uses your own permissions to give someone temporary access to a private file, and once the time is up, the link stops working.

## Validation & Expiry Testing

**Test 1 (Active Link):**
- Opened the pre-signed URL immediately after generation.

   - **Result:** Successful access and file download.

**Test 2 (Expired Link):**
- Waited for the URL to expire and attempted to reuse the same link.

   - **Result:** Access denied due to expiration.

This confirmed that the URL is time-bound and automatically invalidated by AWS after the defined expiry period.

## Lessons Learned

Keep the bucket private and generate pre-signed URLs that grant temporary access to specific objects. This avoids making the bucket public while still allowing controlled access for users or applications.

### Screenshots (Drop down to see images)

<details>
<summary><b>1. Generating a Pre-Signed URL in S3</b> </summary>
<img width="1903" height="617" alt="image" src="https://github.com/user-attachments/assets/30a8b700-946c-41f4-a9a8-0d3147582d51" />
</details>

<details>
<summary><b>2. Successful Access Before Expiration</b> </summary>
<img width="1919" height="160" alt="image" src="https://github.com/user-attachments/assets/0cf82d52-ad43-48ad-b837-342bac457ece" />
</details>

<details>
<summary><b>3. Access Denied After URL Expiry</b> </summary>
<img width="1913" height="382" alt="image" src="https://github.com/user-attachments/assets/8923690b-c519-45f1-9f7c-34fdf195f33c" />
</details>

[`←S3 website hosting and versioning`](static-website-et.al.md) **.** [`Phase 1 Home →`](phase1-main.md) **.** [`Next: LifeCycle Policies →`](lifecycle-policies.md)
