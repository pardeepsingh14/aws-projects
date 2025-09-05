# Static Website — S3 Deployment Guide

This README documents how I deployed a static website to Amazon S3.  
It contains step-by-step deployment instructions, the bucket policy I used, verification commands, and troubleshooting steps.

---

## Project overview
A simple static website (HTML, CSS, images) was deployed to an S3 bucket to serve as a static website hosting origin.  
Example bucket used in this project: `nextwork-website-project-staticwebsite-hosting` (replace with your own bucket name).

---

## Prerequisites
- AWS account with required permissions (S3 create, put object, put bucket policy, put public access block, s3 website config)
- AWS CLI installed and configured (`aws configure`) with appropriate profile
- Local site files ready (e.g., `index.html`, `404.html`, `assets/`)

---

## Repo structure (example)
static-website/
├─ index.html
├─ 404.html
├─ assets/
│ ├─ css/
│ │ └─ styles.css
│ └─ img/
└─ README.md # this file


---

## UI (Console) step-by-step

> All steps performed in the AWS Management Console (https://console.aws.amazon.com).

### 1) Create the S3 bucket
1. Open **S3** in the AWS Console.  
2. Click **Create bucket**.  
3. Enter **Bucket name**: `nextwork-website-project-staticwebsite-hosting`.  
4. Choose Region (e.g., **Asia Pacific (Mumbai) ap-south-1**).  
5. For **Block Public Access settings**, if you plan a public website, uncheck the blocks that prevent public policies or public ACLs **only if** you understand the exposure. (Warning below).  
6. Click **Create bucket**.

---

### 2) Upload website files
1. Open your bucket in the Console → **Objects** tab.  
2. Click **Upload** → **Add files** / **Add folder** and select your `index.html`, `404.html`, and `assets/` folder.  
3. Click **Upload** (use default storage class unless you need different one).

---

### 3) Configure Object Ownership (recommended)
1. In bucket → **Permissions** → **Object Ownership**, set to **Bucket owner preferred** or **ACLs disabled** based on your team policy.  
2. Save (this avoids ownership/ACL conflicts if objects were uploaded from different accounts).

---

### 4) Add bucket policy (Permissions → Bucket policy)
Paste the following policy JSON (this grants public read access to all objects):

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::nextwork-website-project-staticwebsite-hosting/*"
        }
    ]
}

Important: Make sure bucket public access block settings allow this policy to take effect. If Block public policy is enabled, this policy will be ignored.

**### 5) Enable static website hosting (Properties → Static website hosting)**

Open bucket → Properties.

Scroll to Static website hosting → Edit.

Choose Enable → Provide Index document: index.html. Error document: 404.html.

Save.

Note the Endpoint displayed (the website URL), for example:
http://nextwork-website-project-staticwebsite-hosting.s3-website.ap-south-1.amazonaws.com

**### 6) Verify the site**

Open the Endpoint URL in a browser.

If the page loads, site is live.

If you get an AccessDenied XML page, capture the RequestId and HostId values shown in the response body (these help AWS Support trace the issue).

