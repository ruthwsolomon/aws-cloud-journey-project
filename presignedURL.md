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
