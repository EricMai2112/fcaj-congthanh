---
title: "Week 2: VPC Networking, EC2 Compute, and S3 Static Storage"
date: 2026-06-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Weekly Topic:
Architecting and provisioning Amazon VPC networking, Amazon EC2 compute instances, and Amazon S3 static storage

### Weekly Objectives:
- Master cloud virtual networking principles: design a Custom VPC with Public Subnets, Private Subnets, Internet Gateway, NAT Gateway, and routing via Route Tables.
- Launch Amazon EC2 compute instances and configure perimeter security with Security Groups and Network ACLs.
- Deploy and configure an Nginx web server on EC2 with secure Key Pair SSH access.
- Provision an Amazon S3 Bucket, implement object storage lifecycle basics, enable Bucket Versioning, and configure Static Website Hosting.

### Daily Worklog Details (01/06/2026 - 05/06/2026):

| Date | Day | Tasks / Work Description | Hands-on Lab / Project Module | References |
| :--- | :--- | :--- | :--- | :--- |
| 01/06/2026 | Mon | - Studied VPC fundamentals: IP addressing schemes, CIDR notation, and subnetting.<br>- Provisioned a Custom VPC with CIDR 10.0.0.0/16 in the Singapore Region ap-southeast-1.<br>- Created 2 Public Subnets and 2 Private Subnets spanning 2 Availability Zones ap-southeast-1a and ap-southeast-1b. | Building a Custom Amazon VPC with Multi-AZ Subnets | [Amazon VPC Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/) |
| 02/06/2026 | Tue | - Created an Internet Gateway and attached it to the Custom VPC.<br>- Configured Public Route Table routing 0.0.0.0/0 to the Internet Gateway and associated it with Public Subnets.<br>- Deployed a NAT Gateway inside the Public Subnet and updated the Private Route Table for outbound internet connectivity. | Configuring Internet Gateway, NAT Gateway, and Route Tables | [VPC Routing](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html) |
| 03/06/2026 | Wed | - Launched an Amazon EC2 instance Ubuntu 22.04 LTS instance type t3.micro inside the Public Subnet.<br>- Generated a new EC2 Key Pair stored securely on the local environment.<br>- Configured Security Group rules: Inbound port 22 for personal IP and port 80 HTTP for all traffic. | Launching and securing Amazon EC2 Linux instances | [Amazon EC2 User Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/) |
| 04/06/2026 | Thu | - Established secure SSH connectivity to the EC2 instance via terminal.<br>- Updated OS packages, installed and configured Nginx to serve a custom HTML test landing page.<br>- Analyzed Network ACLs: contrasted Security Groups with Network ACLs; implemented subnet-level traffic filtering rules. | Nginx web server deployment and Security Group vs Network ACL analysis | [VPC Security Groups & NACLs](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Security.html) |
| 05/06/2026 | Fri | - Investigated Amazon S3: bucket naming conventions and storage classes.<br>- Created an S3 Bucket and activated Bucket Versioning to guard against accidental deletions.<br>- Configured S3 Static Website Hosting, wrote an S3 Bucket Policy allowing public read access, and validated live endpoint delivery. | Hosting static website with Amazon S3 and Versioning protection | [Amazon S3 Documentation](https://docs.aws.amazon.com/s3/) |

### Knowledge Acquired and Key Deliverables:
- Knowledge Acquired:
  - Subnet allocation and multi-tier network isolation between Public Subnet for internet ingress and Private Subnet for application and database layers.
  - Strategic role of NAT Gateway in enabling private instances to download updates without exposing them to inbound attacks.
  - Practical comparison between Security Groups at the instance level and Network ACLs at the subnet level.
  - Cost-efficient static web hosting paradigms using Amazon S3.
- Key Deliverables:
  - 01 Multi-AZ Custom VPC equipped with Internet Gateway, NAT Gateway, and dedicated Route Tables.
  - 01 Hardened EC2 instance hosting Nginx web server, reachable via Public IP.
  - 01 S3 Bucket configured for Static Website Hosting with active Versioning protection.

### Challenges Faced and Solutions:
- Challenge: Initial SSH attempts to the EC2 instance timed out with a connection timeout error.
- Solution: Followed network troubleshooting diagnostics: verified Public IP allocation, confirmed that the Public Route Table routed 0.0.0.0/0 to the Internet Gateway, and checked port 22 in Security Group rules. Associated the Public Subnet with the Public Route Table, resolving the issue.
