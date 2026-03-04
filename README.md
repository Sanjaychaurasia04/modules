#  Deploy Static Website on AWS

> **Cloud DevOps Nanodegree — Udacity**
> A hands-on project demonstrating static website deployment using Amazon S3 and CloudFront.

---

##  Author

| Field | Details |
|-------|---------|
| **Name** | Sanjay Chaurasia |
| **Programme** | Cloud DevOps Nanodegree — Udacity |
| **AWS Region** | `eu-north-1` (Stockholm) |
| **Bucket Name** | `module-primer-s3-bucket` |

---

## 🔗 Live Website

| Service | URL |
|---------|-----|
| **S3 Endpoint** | https://module-primer-s3-bucket.s3.eu-north-1.amazonaws.com/index+(2).html |

---

##  Project Summary

This project walks through hosting a fully static website on **Amazon Web Services** without managing any servers. The site is stored as objects in an **S3 bucket** configured for website hosting, secured via an **IAM bucket policy**, and distributed globally through **AWS CloudFront** for fast, cached delivery over HTTPS.

The website itself — **MAISON** — is a furniture e-commerce landing page built with HTML5, CSS3, and JavaScript, featuring a live shopping cart, product grid, testimonials, and a custom animated cursor.

---

## 🛠️ Tech Stack

### Frontend
- HTML5
- CSS3
- JavaScript (Vanilla)
- Google Fonts — `Cormorant Garamond`, `DM Sans`

### AWS Services
- **Amazon S3** — Object storage + static website hosting
- **AWS CloudFront** — CDN with edge caching and HTTPS
- **AWS IAM** — Bucket policy for public read access

---

##  Deployment Steps

### 1. Create an S3 Bucket
- Open the **AWS Management Console**
- Navigate to **S3** → Click **Create bucket**
- Enter bucket name: `module-primer-s3-bucket`
- Select region: `eu-north-1`
- Leave all other settings as default and create

### 2. Disable Block Public Access
- Go to the bucket → **Permissions** tab
- Click **Edit** under *Block public access*
- Uncheck **Block all public access** → Save changes

### 3. Enable Static Website Hosting
- Go to the bucket → **Properties** tab
- Scroll to **Static website hosting** → Click **Edit**
- Set hosting type to: **Enable**
- Index document: `index.html`
- Error document: `error.html`
- Save changes

### 4. Apply IAM Bucket Policy
- Go to **Permissions** → **Bucket policy** → Click **Edit**
- Paste the policy below and save:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::module-primer-s3-bucket/*"
    }
  ]
}
```

### 5. Upload Website Files
- Go to the bucket → **Objects** tab → Click **Upload**
- Upload all files maintaining the folder structure:
  - `index.html`
  - `error.html`
  - `images/` folder with all assets

### 6. Verify the Website
- Go to **Properties** → **Static website hosting**
- Copy the **Bucket website endpoint** and open it in a browser
- Confirm the site loads correctly

### 7. Create a CloudFront Distribution
- Navigate to **CloudFront** → Click **Create distribution**
- Set **Origin domain** to the S3 static website endpoint
- Set **Viewer protocol policy** to: `Redirect HTTP to HTTPS`
- Leave all other settings as default → Click **Create distribution**
- Wait for status to change from `Deploying` → `Enabled`

---

##  IAM Bucket Policy Explained

```
Principal : "*"          → Accessible by anyone (public)
Action    : s3:GetObject → Read-only access to objects
Resource  : bucket/*     → Applies to all files in the bucket
Effect    : Allow        → Permission is granted
```

This policy grants **read-only** public access. No write, delete, or administrative permissions are exposed.

---

##  Screenshots

| # | File | Description |
|---|------|-------------|
| 1 | `01-aws-console.png` | AWS Console logged in with eu-north-1 region |
| 2 | `02-s3-bucket-created.png` | S3 bucket created and listed |
| 3 | `03-static-hosting-enabled.png` | Static website hosting enabled in bucket properties |
| 4 | `04-bucket-policy.png` | IAM bucket policy applied |
| 5 | `05-files-uploaded.png` | All website files uploaded to S3 |
| 6 | `06-s3-website-working.png` | Website live via S3 endpoint |
| 7 | `07-cloudfront-distribution.png` | CloudFront distribution configured |
| 8 | `08-cloudfront-working.png` | Website live via CloudFront URL |

---

## ✅ Rubric Checklist

- [x] S3 bucket created in a valid AWS region
- [x] Static website hosting enabled with correct index and error documents
- [x] Block public access disabled
- [x] IAM bucket policy applied for public read
- [x] All website files uploaded to S3
- [x] Website accessible via S3 endpoint URL
- [x] CloudFront distribution deployed and connected to S3 origin
- [x] All steps documented with screenshots
- [x] README includes S3 endpoint and project details

