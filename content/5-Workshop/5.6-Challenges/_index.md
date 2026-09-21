---
title: "Challenges & Future Outlook"
date: 2026-06-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---


### 1. Challenges Encountered

During the architecture and deployment of **ChatPulse** on AWS, the project navigated several pivotal technical challenges:

- **Real-Time Latency & Concurrency Bottlenecks:** Handling bidirectional Socket.IO messaging alongside WebRTC audio and video streams on a single host risks network contention and EC2 resource exhaustion during peak traffic.
- **CloudFront Edge Cache Invalidation:** Deploying frontend updates to Amazon S3 frequently resulted in browsers loading stale cached bundles from CloudFront edge locations, causing API version discrepancies.
- **Multi-Tier Security & Data Protection:** Safeguarding user sessions, tightly regulating multimedia uploads to Amazon S3, and shielding perimeter endpoints against web exploits such as XSS, NoSQL Injection, and DDoS.
- **Cloud Cost Governance:** Monitoring and optimizing continuously running instances including EC2 and ElastiCache to avoid unexpected cloud expenditure throughout development and stress testing.

---

### 2. Technical Solutions

The system implemented standardized cloud architectural patterns to thoroughly address each hurdle:

- **Decoupled Workload Architecture:** The EC2 backend strictly manages authentication and signaling coordination, while heavy WebRTC audio and video streams are offloaded directly to a dedicated LiveKit SFU server, and Amazon ElastiCache Redis handles instant messaging and user presence tracking with sub-millisecond latency under 15ms.
- **Automated Cache Invalidation:** Embedded `aws cloudfront create-invalidation` into the `post_build` phase of AWS CodeBuild, automatically flushing global edge cache within 30 to 60 seconds of every code deployment.
- **Multi-Layer Defense:** Enforced JWT authentication with short-lived access tokens and database-backed refresh tokens, paired with SHA-256 password hashing, granted secure, direct S3 uploads via time-limited Pre-signed URLs, protected edge traffic with AWS WAF, and implemented end-to-end HTTPS and WSS encryption.
- **Cost Optimization & Lifecycle Pruning:** Fully leveraged AWS Free Tier allowances, configured AWS Budgets multi-tier threshold email alerts, and set S3 Lifecycle expiration rules to automatically prune ephemeral test artifacts after 14 days.

---

### 3. Future Development

To expand ChatPulse into a high-scale enterprise communication ecosystem, future roadmap priorities include:

- **Containerization & Autoscaling with Amazon EKS:** Decompose backend logic into independent microservices running in Docker containers orchestrated via Amazon EKS and AWS Fargate for elastic autoscaling.
- **Active-Active Multi-Region Deployment:** Expand across multiple AWS Regions using Route 53 Latency-Based Routing to minimize round-trip network latency for international users.
- **Autonomous AI Agent Integration:** Integrate Amazon Bedrock to automatically transcribe and summarize video meetings, extract action items into chat rooms, and offer semantic knowledge retrieval.
- **Database Modernization & Migration:** Transition from MongoDB to purpose-built distributed databases such as Amazon DynamoDB for serverless massive-scale throughput, Amazon DocumentDB for fully managed MongoDB compatibility, or ScyllaDB to handle millions of chat events per second with sub-millisecond persistence.
- **Enterprise Features & Payment Gateways:** Implement secure payment processing for tiered enterprise subscriptions, offering extended cloud storage and unlimited conference durations.
