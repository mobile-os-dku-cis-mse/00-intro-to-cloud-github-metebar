# report.md

## Summary
In this project, I set up a simple static website using Amazon S3 in the us-east-1 region.
I created a bucket called metecan-2026 and used it to host my HTML files so they can be accessed through a public URL.

## What I Built
- Configured an S3 bucket for static website hosting
- Added index.html as the main page
- Added error.html as a custom error page
- Enabled public read access using a bucket policy

### Region: us-east-1
I used us-east-1 mainly because it’s the default region and easier to work with during setup.

### Static Website Hosting vs REST Endpoint
I used the website endpoint instead of the REST endpoint because it behaves more like a normal website (loads index.html automatically and shows custom error pages).

### Block Public Access (BPA)
At first, I got an AccessDenied error when trying to apply the bucket policy.
Then I realized Block Public Access was still enabled, so I disabled it and tried again.

### Bucket Policy
I allowed only the necessary permission (s3) so users can view the files but cannot make any changes.

## Security Tradeoffs
- The bucket is public so the website can be accessed by anyone.
- Only read access is allowed.
- No permissions for uploading or deleting files.
- Access is limited to the objects inside the bucket.

## Website URL
http://metecan-2026.s3-website-us-east-1.amazonaws.com