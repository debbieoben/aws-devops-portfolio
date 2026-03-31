# Project 3: Production VPC with Auto-Scaling Web Application

## 🚀 Overview
Full-stack production application on AWS featuring VPC networking, load balancing, auto-scaling, and managed database.

**What was built:** Complete 3-tier architecture with VPC, ALB, Auto Scaling Group, EC2 instances, and RDS MySQL database.

## 🏗 Architecture
```
Internet → Application Load Balancer (Public Subnets)
         → Auto Scaling Group (2-4 EC2 instances in Private Subnets)
         → RDS MySQL Database (Private Subnets)
```

**Infrastructure:**
- 1 VPC (10.0.0.0/16) across 2 Availability Zones
- 4 Subnets (2 public, 2 private)
- 1 Internet Gateway + 1 NAT Gateway
- 1 Application Load Balancer
- 1 Auto Scaling Group (2-4 instances)
- 2 EC2 instances (t3.micro)
- 1 RDS MySQL database (db.t3.micro)
- 4 Security Groups

## 💻 What This Demonstrates

**Networking:**
- VPC design with public/private subnet separation
- Multi-AZ architecture for high availability
- NAT Gateway for private subnet internet access
- Route table configuration

**Compute & Scaling:**
- Auto Scaling Group with CPU-based scaling policy
- Launch Template with user data script
- Load balancing across multiple instances
- Self-healing infrastructure

**Database:**
- RDS MySQL in private subnet
- Security group allowing only web server access
- Automated backups configured

**Security:**
- 4-layer security group architecture
- Defense in depth
- Principle of least privilege
- No public database access

## 🎯 Key Features

✅ **Multi-AZ High Availability** - Distributed across us-east-1a and us-east-1b  
✅ **Auto Scaling** - Scales from 2 to 4 instances based on CPU  
✅ **Load Balancing** - ALB distributes traffic across healthy instances  
✅ **Private Subnets** - Web servers and database isolated from internet  
✅ **Managed Database** - RDS MySQL with automated backups  
✅ **Defense in Depth** - Layered security with 4 security groups

## 📊 Infrastructure Details

### VPC Configuration
- **CIDR Block:** 10.0.0.0/16
- **Public Subnets:** 10.0.1.0/24 (us-east-1a), 10.0.2.0/24 (us-east-1b)
- **Private Subnets:** 10.0.11.0/24 (us-east-1a), 10.0.12.0/24 (us-east-1b)

### Auto Scaling Group
- **Desired Capacity:** 2 instances
- **Minimum:** 2 instances
- **Maximum:** 4 instances
- **Scaling Policy:** Target CPU utilization 50%
- **Health Check:** ELB health checks (300s grace period)

### Application Load Balancer
- **Scheme:** Internet-facing
- **Subnets:** Both public subnets
- **Listener:** HTTP:80
- **Target Group:** production-web-tg
- **Health Check:** HTTP:80 on path `/`

### RDS Database
- **Engine:** MySQL 8.0
- **Instance:** db.t3.micro
- **Storage:** 20 GB
- **Deployment:** Single-AZ (cost optimized)
- **Backup:** 1-day retention

### Security Groups
1. **ALB-SG:** Allows HTTP/HTTPS from internet
2. **WebServer-SG:** Allows HTTP from ALB only
3. **Database-SG:** Allows MySQL from web servers only
4. **Bastion-SG:** Allows SSH from specific IP (reserved)

## 💰 Cost Analysis

**Actual Cost (2 hours):** ~$0.20

| Component | Cost |
|-----------|------|
| NAT Gateway | ~$0.09 |
| Application Load Balancer | ~$0.05 |
| RDS db.t3.micro | ~$0.03 |
| EC2 t3.micro (2x) | $0.00 (free tier) |

**If left running:** ~$66/month (mostly NAT Gateway + ALB)

**Cost saved by:** Using free tier instances, single NAT Gateway, and tearing down after demo

## 🎤 Interview Talking Points

**Architecture Overview:**
*"I built a production-grade web application using AWS with a 3-tier architecture. The VPC spans two availability zones with public/private subnet separation. Traffic flows through an Application Load Balancer to an Auto Scaling Group of EC2 instances in private subnets, which connect to an RDS MySQL database also in private subnets."*

**High Availability:**
*"The architecture is designed for fault tolerance through multi-AZ deployment. The ALB distributes traffic across instances in different availability zones. If one AZ fails, the other continues serving traffic. The Auto Scaling Group maintains a minimum of 2 instances and automatically replaces unhealthy instances."*

**Security:**
*"I implemented defense-in-depth security with four security groups. The ALB accepts internet traffic, web servers only accept traffic from the ALB, and the database only accepts connections from web servers. This creates multiple security layers following the principle of least privilege."*

**Auto Scaling:**
*"The Auto Scaling Group uses a target tracking policy monitoring CPU utilization. When average CPU exceeds 50%, it launches additional instances up to a maximum of 4. This provides both high availability and cost efficiency by scaling resources based on actual demand."*

## 🛠 Skills Demonstrated

- VPC design and CIDR planning
- Multi-AZ architecture
- Application Load Balancer configuration
- Auto Scaling Group setup with scaling policies
- Launch Template creation with user data
- RDS database deployment
- Security group layering
- Private/public subnet separation
- NAT Gateway configuration
- Route table management
- Health check configuration
- Cost optimization strategies
- Infrastructure documentation

## 📸 Screenshots

All screenshots showing the complete infrastructure are available in the `screenshots/` folder, including:

- VPC and subnets configuration
- NAT Gateway and route tables
- Security groups (all 4)
- RDS database setup
- Application Load Balancer
- Target Group with healthy instances
- Auto Scaling Group configuration
- EC2 instances running
- Working application in browser

## 🧹 Teardown

All infrastructure was deleted after completion to avoid ongoing charges:

1. Auto Scaling Group (terminates instances automatically)
2. Application Load Balancer
3. Target Group
4. RDS Database
5. NAT Gateway (critical for cost savings)
6. VPC (deletes all subnets, route tables, IGW)
7. Launch Template
8. DB Subnet Group

**Result:** $0.00 ongoing charges ✅

## 📚 Lessons Learned

**Networking:**
- NAT Gateway is expensive (~$32/month) - biggest cost driver
- Route table configuration is critical for public/private separation
- CIDR planning must account for future growth

**Auto Scaling:**
- Health check grace period prevents premature terminations
- Target tracking is easier than step scaling for most use cases
- Minimum capacity ensures availability during scaling events

**Load Balancing:**
- ALB health checks must match application configuration
- Target deregistration delay affects deployment speed
- Connection draining prevents dropped requests

**Security:**
- Security group chaining provides effective defense in depth
- Always use least privilege - only open necessary ports
- Private subnets significantly reduce attack surface

**Troubleshooting:**
- Security group misconfigurations are the most common issue
- User data script errors can prevent instances from becoming healthy
- Always verify security group sources reference correct groups

## 🔄 Future Enhancements

- [ ] Enable Multi-AZ for RDS (automatic failover)
- [ ] Add HTTPS with AWS Certificate Manager
- [ ] Implement CloudWatch alarms and dashboards
- [ ] Add bastion host for secure SSH access
- [ ] Deploy across 3 availability zones
- [ ] Add AWS WAF for web application firewall
- [ ] Implement ElastiCache for session management
- [ ] Configure VPC Flow Logs
- [ ] Use AWS Secrets Manager for credentials
- [ ] Add CI/CD pipeline for automated deployments

---

**Project Completed:** March 30, 2026  
**Duration:** 2 hours  
**Total Cost:** $0.20  
**Status:** Infrastructure torn down, documentation complete
