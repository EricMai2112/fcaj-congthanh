---
title: "Week 8: Real-Time Chat, S3 Uploads, and SSL Setup"
date: 2026-07-13
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Weekly Topic:
Building real-time WebSocket messaging with Redis Pub/Sub, direct S3 uploads via Pre-signed URLs, and global HTTPS deployment with ACM and CloudFront

### Weekly Objectives:
- Implement real-time messaging using WebSocket and Socket.io backed by an ElastiCache Redis Pub/Sub adapter to support horizontal multi-server scaling.
- Program direct client-to-cloud media upload flows utilizing short-lived Amazon S3 Pre-signed URLs.
- Manage project domain zones with Amazon Route 53, request and validate SSL/TLS certificates via AWS Certificate Manager.
- Deploy the React Frontend bundle onto an S3-backed Amazon CloudFront Distribution, enforcing HTTPS encryption and edge delivery.

### Daily Worklog Details (13/07/2026 - 17/07/2026):

| Date | Day | Tasks / Work Description | Hands-on Lab / Project Module | References |
| :--- | :--- | :--- | :--- | :--- |
| 13/07/2026 | Mon | - Integrated Socket.io into the Node.js backend; wrote JWT validation middleware for WebSocket connection handshakes.<br>- Connected socket.io redis-adapter directly to the ElastiCache Redis cluster.<br>- Validated bidirectional text message exchanges across browser sessions with sub-30ms latencies. | Project Chatpulse: WebSocket server implementation with Redis Pub/Sub adapter | [Socket.io Redis Adapter](https://socket.io/docs/v4/redis-adapter/) |
| 14/07/2026 | Tue | - Developed messaging features: direct messaging and department channel chat.<br>- Implemented real-time user presence detection persisted within Redis.<br>- Added typing indicator events and message delivery confirmation acknowledgments. | Project Chatpulse: Advanced room messaging and real-time presence engine | [WebSocket Security Best Practices](https://cheatsheetseries.owasp.org/cheatsheets/HTML5_Security_Cheat_Sheet.html#websockets) |
| 15/07/2026 | Wed | - Developed Backend API for media upload-url utilizing AWS SDK to issue S3 Pre-signed PUT URLs valid for 300 seconds.<br>- Constructed React client file uploader component: fetches signed URL, performs direct binary HTTP PUT to S3, and commits object URL to database.<br>- Verified uploads for profile avatars and attachments in PDF, DOCX, PNG, and JPG formats. | Project Chatpulse: Direct S3 media ingestion pipeline via Pre-signed URLs | [S3 Pre-signed URLs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html) |
| 16/07/2026 | Thu | - Mapped project subdomains on Amazon Route 53.<br>- Requested a public SSL/TLS certificate via AWS Certificate Manager in us-east-1.<br>- Created automated CNAME validation records in Route 53, completing DNS validation. | Project Chatpulse: Route 53 DNS management and SSL/TLS provisioning via ACM | [AWS Certificate Manager Guide](https://docs.aws.amazon.com/acm/latest/userguide/) |
| 17/07/2026 | Fri | - Compiled production React frontend bundle.<br>- Synchronized static assets to S3 web hosting bucket and provisioned CloudFront Distribution attached to the ACM SSL certificate.<br>- Enforced HTTP to HTTPS redirect policy and created a Route 53 Alias record pointing to CloudFront. | Project Chatpulse: CloudFront CDN HTTPS deployment and Route 53 Alias routing | [CloudFront HTTPS Configuration](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-alternate-domain-names.html) |

### Knowledge Acquired and Key Deliverables:
- Knowledge Acquired:
  - Solving horizontal scaling bottlenecks in WebSocket applications: Redis Pub/Sub abstracts connection locality, broadcasting messages across multiple EC2 instances.
  - Architectural mechanics of Pre-signed URLs: delegating upload capability directly to clients with strict temporal scopes, isolating backend memory and network pipes.
  - Cryptographic HTTPS termination and DNS Alias mapping using ACM, CloudFront, and Route 53.
- Key Deliverables:
  - Real-time WebSocket messaging service with sub-30ms latency backed by ElastiCache Redis.
  - Direct-to-S3 media upload pipeline for avatars and documents with minimal server overhead.
  - HTTPS-secured Frontend production web application globally accelerated by CloudFront CDN.

### Challenges Faced and Solutions:
- Challenge: Client browsers threw a network and authorization error when executing direct HTTP PUT payload uploads against the S3 Pre-signed URL.
- Solution: Investigated S3 Bucket CORS configurations. Discovered the bucket policy only permitted GET requests and lacked Content-Type header declarations. Updated CORS configuration on the S3 bucket to allow PUT verbs and whitelisted the CloudFront distribution domain, resolving upload issues.
