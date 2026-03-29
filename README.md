# Develop and Deploy a Website using EC2, S3, and CloudFront

## Project Overview

In this project, I have developed and deployed a scalable web application using Amazon Web Services (AWS).
The architecture combines Amazon S3 for static content storage, Amazon EC2 for backend processing, and CloudFront for global content delivery.

This setup demonstrates how to build a modern web application by separating frontend and backend layers, ensuring better performance, scalability, and security.

---

## Project Objectives

* Host static website files using Amazon S3
* Deploy backend server using Amazon EC2
* Integrate S3 and EC2 using CloudFront
* Deliver content securely using HTTPS
* Improve performance using CDN

---

## Prerequisites

* AWS account (Free Tier recommended)
* Basic knowledge of:

  * EC2, S3, and CloudFront
  * HTML, CSS, JavaScript
  * Linux commands

---

## Step 1: Create Static Website using S3

1. Go to S3 service
2. Create a new bucket
3. Upload website files:

   * index.html
   * style.css
   * images
4. Enable Static Website Hosting
5. Set index document as:

   ```
   index.html
   ```

---

## Step 2: Launch EC2 Instance (Backend)

1. Go to EC2 service
2. Launch instance:

   * AMI: Amazon Linux
   * Instance type: t2.micro
3. Configure Security Group:

   * Allow HTTP (80)
   * Allow SSH (22)

---

## Step 3: Configure Web Server on EC2

Connect to EC2 via SSH and run:

```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

### Add Sample Backend File

```bash
echo "Backend running successfully" > /var/www/html/api.html
```

---

## Step 4: Connect Frontend with Backend

Modify your frontend code to call EC2 backend:

```html
<script>
fetch('http://<EC2-PUBLIC-IP>/api.html')
  .then(res => res.text())
  .then(data => console.log(data));
</script>
```

---

## Step 5: Create CloudFront Distribution

1. Go to CloudFront service
2. Click Create Distribution

### Configure Origins

* Origin 1: S3 bucket (frontend)
* Origin 2: EC2 instance (backend)

### Configure Behavior

* `/` → S3
* `/api/*` → EC2

### Settings

* Enable Redirect HTTP to HTTPS
* Set Default Root Object:

  ```
  index.html
  ```

---

## Step 6: Access Website

After deployment, access your website using:

```
https://your-cloudfront-domain.net
```

---

## Architecture Diagram

<p align="center">
  <img src="architecture.png" width="800">
</p>

---

## Architecture Explanation

* Amazon S3 stores static frontend files
* EC2 instance handles backend processing
* CloudFront distributes content globally
* Requests are routed based on path patterns
* HTTPS ensures secure communication

---

## Data Flow

1. User accesses CloudFront URL
2. CloudFront routes request to S3 (static content)
3. API requests are forwarded to EC2
4. EC2 processes request and returns response
5. CloudFront delivers response to user

---

## Summary

In this project, I:

* Hosted static content using S3
* Deployed backend on EC2
* Integrated services using CloudFront
* Enabled secure and fast content delivery

This project demonstrates a real-world scalable web architecture using AWS services.

---

## Conclusion

By combining S3, EC2, and CloudFront, this architecture provides high performance, scalability, and security. It follows best practices for modern web application deployment in the cloud.

---

## Note

This project was implemented using AWS Free Tier.
Resources were stopped or deleted after testing to avoid additional charges.
