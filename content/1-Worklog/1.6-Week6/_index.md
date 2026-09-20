---
title: "Week 6: Chatpulse Project Kickoff, Architecture, and VPC"
date: 2026-06-29
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Weekly Topic:
Project kickoff for Chatpulse, technical requirements analysis, AWS Well-Architected system design, and dedicated multi-tier VPC provisioning

### Weekly Objectives:
- Officially initiate the internship project Chatpulse, a secure real-time enterprise internal communication and collaboration platform.
- Specify functional requirements including account management, real-time messaging, file sharing, and role-based access control, alongside non-functional requirements on low latency, high availability, and cost optimization.
- Construct the complete system architecture diagram using standardized AWS Architecture Icons adhering to the AWS Well-Architected Framework.
- Design and provision a dedicated multi-tier VPC infrastructure alongside an encrypted Amazon S3 bucket for media asset persistence.

### Daily Worklog Details (29/06/2026 - 03/07/2026):

| Date | Day | Tasks / Work Description | Hands-on Lab / Project Module |
| :--- | :--- | :--- | :--- |
| 29/06/2026 | Mon | - Analyzed core workflows: registration, authenticated sign-in, real-time WebSocket chat, and direct cloud media uploads.<br>- Developed phased milestone delivery roadmaps for subsequent sprints. | [Final Project](https://github.com/EricMai2112/chat-pulse) |
| 30/06/2026 | Tue | - Drafted system architecture in Draw.io using official AWS Architecture Icons.<br>- Designed 3-tier topology: Client to CloudFront, to ALB, to EC2 App instances running Node.js and Socket.io in Public Subnet, integrating with ElastiCache Redis in Private Subnet, S3, and SES.<br>- Refined architectural nuances ensuring valid service naming and decoupled data flows. | [Final Project](https://github.com/EricMai2112/chat-pulse) |
| 01/07/2026 | Wed | - Conducted Well-Architected evaluation across all 5 pillars:<br>+ Security: EC2 backend deployed in Public Subnet, ElastiCache isolated in Private Subnet, and S3 Pre-signed URL uploads.<br>+ Reliability & Performance: Multi-AZ resilience with Redis Pub/Sub horizontal scale.<br>+ Cost Optimization: Right-sized instances and optimized storage policies. | [Final Project](https://github.com/EricMai2112/chat-pulse) |
| 02/07/2026 | Thu | - Provisioned custom VPC for Chatpulse with CIDR 10.10.0.0/16.<br>- Implemented networking layout: 02 Public Subnets for ALB and EC2 Backend, 02 Private Data Subnets for ElastiCache Redis.<br>- Associated Internet Gateway and provisioned dedicated Route Tables. | [000003 - Multi-tier VPC Infrastructure Deployment](https://000003.awsstudygroup.com/) |
| 03/07/2026 | Fri | - Provisioned dedicated media storage S3 Bucket named chatpulse-bucket.<br>- Enforced Block Public Access.<br>- Configured CORS policy allowing direct client HTTP PUT and GET requests.<br>- Compiled Week 6 deliverable package and reviewed blueprint with Mentor. | [000057 - Provisioning Secure S3 Media Storage Bucket](https://000057.awsstudygroup.com/) |

### Knowledge Acquired and Key Deliverables:
- Knowledge Acquired:
  - Transforming business requirements into cloud architectural blueprints following AWS design standards.
  - Practical realization of AWS Well-Architected principles: defense-in-depth, clear network segregation between public and private tiers.
  - Leveraging in-memory caching and Pub/Sub engines in Redis to maintain high throughput without database bottlenecks.
- Key Deliverables:
  - Official AWS Architecture Diagram for Project Chatpulse ready for Proposal and Workshop chapters.
  - Live chatpulse-vpc network featuring Public Subnets for EC2 Backend and Private Subnets for ElastiCache Redis.
  - S3 Bucket chatpulse-bucket ready for secure media ingestion.

### Challenges Faced and Solutions:
- Challenge: The initial design routed media uploads through the EC2 backend server, which would cause severe network bandwidth bottlenecks when multiple concurrent users uploaded high-resolution media.
- Solution: Transitioned to Amazon S3 Pre-signed URLs. The backend server authenticates the user and dispenses a time-limited signed URL valid for 5 minutes, allowing the client to stream payloads directly into Amazon S3. This eliminated backend network overhead.
