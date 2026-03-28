# commands.md

## Bucket Name
BUCKET_NAME=metecan-2026

## Step 1: Create Bucket
### Command
aws s3api create-bucket --bucket metecan-2026 --region us-east-1

### Output
{
    "Location": "/metecan-2026",
    "BucketArn": "arn:aws:s3:::metecan-2026"
}

### Notes
Created an S3 bucket named metecan-2026 in the us-east-1 region.

## Step 2: Disable Block Public Access
### Command
aws s3api put-public-access-block --bucket metecan-2026 --public-access-block-configuration "BlockPublicAcls=false,IgnorePublicAcls=false,BlockPublicPolicy=false,RestrictPublicBuckets=false"

### Output
(No output)

### Notes
There was no output, so the command worked.

## Step 3: Apply Bucket Policy
### Command
aws s3api put-bucket-policy --bucket metecan-2026 --policy file://policy.json

### Output
(No output)

### Notes
Applied the bucket policy to allow public read access.
Only the s3:GetObject permission is allowed.

## Step 4: Enable Static Website Hosting
### Command
aws s3api put-bucket-website --bucket metecan-2026 --website-configuration "{\"IndexDocument\":{\"Suffix\":\"index.html\"},\"ErrorDocument\":{\"Key\":\"error.html\"}}"

### Output
(No output)

### Notes
Enabled static website hosting.
Set index.html as the main page and error.html as the error page.

## Step 5: Upload Files
### Command
aws s3 cp index.html s3://metecan-2026/index.html --content-type text/html
aws s3 cp error.html s3://metecan-2026/error.html --content-type text/html

### Output
upload: .\index.html to s3://metecan-2026/index.html
upload: .\error.html to s3://metecan-2026/error.html

### Notes
Both files were uploaded successfully.
I also set the correct content-type so the browser can render them properly.

## Verification 1: get-bucket-website
### Command
aws s3api get-bucket-website --bucket metecan-2026

### Output
{
    "IndexDocument": {
        "Suffix": "index.html"
    },
    "ErrorDocument": {
        "Key": "error.html"
    }
}

### Notes
This confirms that static website hosting is enabled and both index and error pages are set correctly.

## Verification 2: get-bucket-policy
### Command
aws s3api get-bucket-policy --bucket metecan-2026

### Output
{"Version":"2012-10-17","Statement":[{"Sid":"PublicReadGetObject","Effect":"Allow","Principal":"*","Action":"s3:GetObject","Resource":"arn:aws:s3:::metecan-2026/*"}]}

### Notes
The policy shows that only s3:GetObject is allowed.
No extra permissions are included, so it follows the least-privilege principle.

## Verification 3: get-public-access-block
### Command
aws s3api get-public-access-block --bucket metecan-2026

### Output
{
    "PublicAccessBlockConfiguration": {
        "BlockPublicAcls": false,
        "IgnorePublicAcls": false,
        "BlockPublicPolicy": false,
        "RestrictPublicBuckets": false
    }
}

### Notes
All Block Public Access settings are disabled, so the bucket can be accessed publicly.

## Verification 4: list-object-versions
### Command
aws s3api list-object-versions --bucket metecan-2026

### Output
{
    "Versions": [
        {
            "Key": "error.html",
            "IsLatest": true,
            "LastModified": "2026-03-24T16:35:58+00:00"
        },
        {
            "Key": "index.html",
            "IsLatest": true,
            "LastModified": "2026-03-24T16:35:50+00:00"
        }
    ]
}

### Notes
Both index.html and error.html are present in the bucket and marked as the latest versions.

## Website URL Validation
### URL
http://metecan-2026.s3-website-us-east-1.amazonaws.com

### Result
The website is live and accessible.
The main page loads correctly when opening the URL.