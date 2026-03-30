# Project 1: Secure Static Website (S3 + CloudFront)

## 🚀 Live Demo
**URL:** https://dpavaa9ircqaq.cloudfront.net

## 📋 Overview
Professional portfolio website hosted on AWS using S3 for storage and CloudFront CDN with enterprise-grade security. The website showcases my AWS DevOps skills and featured projects.

## 🏗 Architecture
```
Browser → CloudFront (HTTPS, 400+ edge locations) 
         → Origin Access Control 
         → S3 Bucket (Private, Block All Public Access)
```

**Key Components:**
- **S3 Bucket:** devops-portfolio-debbie-2026 (us-east-1)
- **CloudFront Distribution:** E33NY6R6S9NZNZ
- **Distribution Domain:** dpavaa9ircqaq.cloudfront.net
- **Security:** Origin Access Control (OAC) - S3 is completely private

## 🛠 Technologies Used

- **AWS S3:** Object storage for website files
- **AWS CloudFront:** Global CDN with 400+ edge locations
- **Origin Access Control (OAC):** Secure S3 access (CloudFront only)
- **HTTPS/TLS:** Automatic SSL certificate from CloudFront
- **HTML5 & CSS3:** Responsive design with gradient backgrounds
- **VS Code:** Development environment

## 🔒 Security Features

1. **Private S3 Bucket**
   - Block all public access enabled
   - No public bucket policies
   - No ACLs allowing public access

2. **Origin Access Control (OAC)**
   - Only CloudFront can access S3 bucket
   - S3 bucket policy restricts access to specific CloudFront distribution
   - No direct S3 access from internet

3. **HTTPS Enforced**
   - All HTTP requests redirect to HTTPS
   - CloudFront provides free SSL/TLS certificate
   - Secure connection with encryption in transit

4. **Custom Error Pages**
   - Custom 404 error page (user-friendly)
   - No information leakage from default error messages

## 🎨 Website Features

- **Responsive Design:** Works on desktop, tablet, and mobile
- **Modern UI:** Purple gradient background, card-based layout
- **Fast Loading:** Served from edge locations worldwide
- **Project Showcase:** Cards displaying 6 featured DevOps projects
- **Skills Section:** 8 technical skills with visual badges
- **Security Badges:** Visual indicators for HTTPS, Private S3, CDN, Edge Caching

## 💰 Cost Analysis

**Monthly Cost:** $0.00 (FREE)

**AWS Free Tier Coverage:**
- **S3:** 5 GB storage, 20,000 GET requests, 2,000 PUT requests
- **CloudFront:** 1 TB data transfer out, 10 million HTTP/HTTPS requests
- **Data Transfer:** First 100 GB free from CloudFront

**This project stays well within free tier limits for a portfolio website.**

## 📊 Performance

- **Global Edge Locations:** 400+ worldwide
- **Latency:** < 100ms for most users globally
- **Caching:** Automatic edge caching reduces origin requests
- **HTTP/2:** Enabled for faster page loads
- **Compression:** Automatic gzip compression enabled

## 🎯 Skills Demonstrated

1. **AWS S3 Configuration**
   - Bucket creation and configuration
   - Permissions and security settings
   - File upload and management

2. **AWS CloudFront Setup**
   - Distribution creation and configuration
   - Origin Access Control implementation
   - Custom error page configuration
   - Cache behavior settings

3. **Security Best Practices**
   - Principle of least privilege
   - Defense in depth (multiple security layers)
   - HTTPS enforcement
   - Private bucket architecture

4. **Web Development**
   - HTML5 semantic markup
   - CSS3 modern features (gradients, flexbox, grid)
   - Responsive design principles
   - User experience optimization

5. **DevOps Practices**
   - Infrastructure documentation
   - Cost optimization
   - Performance monitoring
   - Git version control

## 📸 Screenshots

website/Screenshots/live-website-homepage.png



## 🚀 Deployment Steps

1. **Create S3 Bucket**
   - Block all public access
   - Enable default encryption

2. **Upload Website Files**
   - index.html
   - error.html

3. **Create CloudFront Distribution**
   - Origin: S3 bucket
   - Origin Access Control: Create new OAC
   - Viewer protocol: Redirect HTTP to HTTPS
   - Default root object: index.html

4. **Update S3 Bucket Policy**
   - Allow CloudFront service principal
   - Restrict to specific distribution ARN

5. **Configure Custom Error Pages**
   - 404 → /error.html

6. **Test & Verify**
   - Homepage loads
   - HTTPS works
   - Custom error page displays


## 📸 Screenshots

### 🌐 Live Website Homepage
![Homepage](./Screenshots/homepage.png)
*Professional portfolio website with purple gradient design and project showcase*

### 🔴 Custom 404 Error Page
![404 Error Page](./Screenshots/404-error-page.png)
*User-friendly custom error page with "Back to Home" button*

### 🔒 HTTPS Security
![HTTPS Secure](./Screenshots/https-secure.png)
*Browser showing secure HTTPS connection with lock icon*

### ☁️ CloudFront Distribution
![CloudFront Distribution](./Screenshots/cloudfront-distribution.png)
*AWS CloudFront console showing deployed distribution*

### 🪣 S3 Bucket Configuration
![S3 Bucket Files](./Screenshots/s3-bucket-files.png)
*Private S3 bucket with index.html and error.html files*

### 🏗️ Architecture Diagram
[View Full Architecture Diagram (PDF)](./architecture-diagram.pdf)  

## 🎤 Interview Talking Points

*"I built a secure static website using AWS S3 and CloudFront. The S3 bucket is completely private with all public access blocked. Only CloudFront can access the files using Origin Access Control, which is AWS's recommended approach over legacy Origin Access Identity.*

*All traffic is served over HTTPS using CloudFront's free SSL certificate, with HTTP requests automatically redirecting to HTTPS. The content is distributed globally through 400+ edge locations, providing sub-100ms latency for users worldwide.*

*The architecture demonstrates security best practices: defense in depth with multiple layers, principle of least privilege with minimal permissions, and encryption in transit. The entire setup stays within AWS free tier, costing $0 per month.*

*This project shows I understand cloud storage, CDN configuration, origin security, and how to build production-grade infrastructure while staying cost-effective."*

## 🔄 Future Enhancements

- [ ] Add custom domain name (e.g., www.debbieoben.com)
- [ ] Implement AWS WAF for DDoS protection
- [ ] Add CloudWatch logging and monitoring
- [ ] Create multiple environments (dev, staging, prod)
- [ ] Implement CI/CD pipeline with GitHub Actions
- [ ] Add Lambda@Edge for dynamic content
- [ ] Implement versioning and rollback capability

## 📚 What I Learned

1. **S3 vs CloudFront:** When to use each and how they work together
2. **Origin Access Control:** New recommended approach vs legacy OAI
3. **Cache Behavior:** How CloudFront caching works and TTL settings
4. **Security Layers:** Multiple security controls working together
5. **Cost Optimization:** Leveraging free tier effectively
6. **Global Distribution:** How CDNs reduce latency worldwide

## 🧹 Cleanup Instructions

**To avoid any charges after free tier expires:**

1. **Delete CloudFront Distribution:**
   - Disable distribution
   - Wait for "Disabled" status
   - Delete distribution

2. **Empty and Delete S3 Bucket:**
   - Empty bucket (delete all objects)
   - Delete bucket

**Note:** Keep local files and this documentation!

---

**Built:** March 30, 2026  
**Time to Complete:** 1 hour  
**Total Cost:** $0.00  
**Status:** ✅ Live and deployed
