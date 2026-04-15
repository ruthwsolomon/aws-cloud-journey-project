# PRE-SIGNED URL SYSTEM (S3 Secure Access)
## Overview
This project demonstrates how to provide temporary, secure access to private S3 objects without ever making the bucket or the files public. This is a critical security pattern used in production environments to share sensitive data or allow time-limited uploads.

### Generating the Pre-Signed URL
- Created an S3 bucket `s3-ruth-demo-bucket`
- Enabled "Block all public access" (ON) so that the bucket has no public URL, and the objects cannot be reached via standard HTTP requests without authentication.   
- Uploaded file `s3demo.txt` into the bucket then attempted to access the file's direct S3 Object URL in an incognito browser. I received an Access Denied error, confirming the file is private.
- Used the Object Actions > Share with a pre-signed URL feature in the AWS Console.
    -Settings: * Time Interval: 1 Minute (to test immediate expiry).
AWS generates a unique URL that includes a temporary authentication token (Signature) tied to my IAM permissions.

### Validation & Expiry Testing
- Test 1 (Active): Opened the link immediately.

Result: Success. The file downloaded/opened perfectly.

- Test 2 (Expired): Waited 2 minutes and refreshed the same link.

Result: AccessDenied (Expired). The URL was automatically invalidated by AWS.
