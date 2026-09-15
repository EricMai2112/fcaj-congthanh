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

| Date | Day | Tasks / Work Description | Hands-on Lab / Project Module | References |
| :--- | :--- | :--- | :--- | :--- |
| 29/06/2026 | Mon | - Alignment session with Mentor Nguyen Gia Hung finalizing project scope: Enterprise Internal Communication Platform Chatpulse.<br>- Outlined core user journeys: secure authentication, real-time WebSocket messaging, direct cloud document and image upload.<br>- Established an execution timeline and delivery milestones over the subsequent weeks. | Project Chatpulse: Scope definition and requirements specification | [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/) |
| 30/06/2026 | Tue | - Drafted comprehensive architectural blueprints on Draw.io utilizing official AWS Architecture Icons.<br>- Mapped 3-tier data flows: Client to CloudFront, to ALB, to EC2 App Instances running Node.js and Socket.io, connecting to ElastiCache Redis, S3, and SES.<br>- Verified every connecting line to eliminate overlaps and ensure correct AWS service terminology. | Project Chatpulse: System architecture modeling with AWS Architecture Icons | [AWS Architecture Icons](https://aws.amazon.com/architecture/icons/) |
| 01/07/2026 | Wed | - Evaluated architectural choices against Well-Architected Pillars:<br>+ Security: Backend and database tiers isolated in Private Subnets; S3 interactions handled via Pre-signed URLs.<br>+ Reliability and Performance: Multi-AZ redundancy; Redis Pub/Sub cluster ensuring cross-node message distribution.<br>+ Cost Optimization: Maximizing resource efficiency with lean instance families and intelligent storage classes. | Project Chatpulse: Well-Architected Framework design verification | [Well-Architected Pillars](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html) |
| 02/07/2026 | Thu | - Provisioned the project dedicated VPC chatpulse-vpc with CIDR 10.10.0.0/16.<br>- Structured 3 isolated network tiers across 2 AZs: 2 Public Subnets for ALB and NAT Gateway, 2 Private App Subnets for EC2 instances, and 2 Private Data Subnets for ElastiCache Redis and Database.<br>- Attached Internet Gateway and updated routing tables. | Project Chatpulse: Multi-tier dedicated VPC infrastructure deployment | [VPC Subnet Sizing](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html) |
| 03/07/2026 | Fri | - Created a dedicated media storage bucket named chatpulse-media-assets-prod.<br>- Configured complete Block Public Access settings and enabled SSE-S3 AES-256 server-side encryption.<br>- Implemented CORS policies permitting HTTP PUT and GET actions directly from client origins.<br>- Submitted architecture diagram to Mentor for review. | Project Chatpulse: S3 media bucket provisioning and security hardening | [S3 Security Best Practices](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html) |

### Knowledge Acquired and Key Deliverables:
- Knowledge Acquired:
  - Transforming business requirements into cloud architectural blueprints following AWS design standards.
  - Practical realization of AWS Well-Architected principles: defense-in-depth, strict network segregation between Web, Application, and Data tiers.
  - Leveraging in-memory caching and Pub/Sub engines in Redis to maintain high throughput without database bottlenecks.
- Key Deliverables:
  - Official AWS Architecture Diagram for Project Chatpulse ready for Proposal and Workshop chapters.
  - Live chatpulse-vpc network spanning 6 isolated subnets across 2 Availability Zones.
  - Hardened, encrypted S3 Bucket chatpulse-media-assets-prod ready for secure media ingestion.

### Challenges Faced and Solutions:
- Challenge: The initial design routed media uploads through the EC2 backend server, which would cause severe network bandwidth bottlenecks when multiple concurrent users uploaded high-resolution media.
- Solution: Transitioned to Amazon S3 Pre-signed URLs. The backend server authenticates the user and dispenses a time-limited signed URL valid for 5 minutes, allowing the client to stream payloads directly into Amazon S3. This eliminated backend network overhead.
