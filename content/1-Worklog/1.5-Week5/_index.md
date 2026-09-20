---
title: "Week 5: Docker Containers, ECR, CloudFront CDN, and Route 53"
date: 2026-06-22
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Weekly Topic:
Containerizing workloads with Docker and Amazon ECR, global content delivery via Amazon CloudFront CDN, and DNS management with Amazon Route 53

### Weekly Objectives:
- Master container packaging best practices using Docker: author multi-stage Dockerfile manifests to minimize image footprint and maximize runtime security.
- Provision an Amazon Elastic Container Registry repository, authenticate the Docker daemon via AWS CLI, and push production container images.
- Configure authoritative DNS resolution using Amazon Route 53: establish Public Hosted Zones and configure A, CNAME, and native Alias records.
- Accelerate static and dynamic content delivery with Amazon CloudFront CDN, configure Origin Access Control to secure S3 origins, and optimize edge caching behavior.

### Daily Worklog Details (22/06/2026 - 26/06/2026):

| Date | Day | Tasks / Work Description | Hands-on Lab / Project Module |
| :--- | :--- | :--- | :--- |
| 22/06/2026 | Mon | - Investigated Containerization paradigms and contrasted containers with virtual machines.<br>- Authored a multi-stage Dockerfile for a sample Node.js and React full-stack application.<br>- Optimized dockerignore rules, built local images, and verified execution via docker run. | [000015 - Containerization with Docker](https://000015.awsstudygroup.com/) |
| 23/06/2026 | Tue | - Studied Amazon Elastic Container Registry management features.<br>- Provisioned a Private Repository fcaj-sample-app on Amazon ECR with scan-on-push enabled.<br>- Acquired authentication tokens via aws ecr get-login-password, tagged image artifacts, and pushed images to ECR. | [000016 - Container Orchestration with Amazon ECS](https://000016.awsstudygroup.com/) |
| 24/06/2026 | Wed | - Explored Amazon Route 53 DNS resolution mechanisms, record categories, and routing policies.<br>- Created a Public Hosted Zone within Route 53.<br>- Configured standard A records pointing to compute IPs, CNAME records, and specialized AWS Alias records. | [000010 - DNS Management with Amazon Route 53](https://000010.awsstudygroup.com/) |
| 25/06/2026 | Thu | - Examined Amazon CloudFront content delivery network topology: Edge Locations, Regional Edge Caches, and Origins.<br>- Created a CloudFront Distribution pointing to an S3 Static Website Origin.<br>- Enforced Origin Access Control and updated S3 Bucket Policy to restrict access strictly to CloudFront. | [000094 - Content Delivery with Amazon CloudFront](https://000094.awsstudygroup.com/) |
| 26/06/2026 | Fri | - Fine-tuned CloudFront delivery: enabled automatic gzip and Brotli compression, configured Cache-Control TTL headers.<br>- Associated a Route 53 Alias Record mapping directly to the CloudFront distribution domain name.<br>- Profiled and benchmarked latency reduction before and after CDN acceleration. | [000094 - Optimizing Caching & Route 53 Routing](https://000094.awsstudygroup.com/) |

### Knowledge Acquired and Key Deliverables:
- Knowledge Acquired:
  - Multi-stage Docker builds: segregating build toolchains from lean runtime artifacts, drastically shrinking image size from 800MB down to 45MB.
  - Temporary, scoped Docker authentication against Amazon ECR leveraging AWS STS credentials.
  - Global DNS resolution workflows with Route 53 and the strategic value of AWS Alias records.
  - Origin protection using CloudFront Origin Access Control, ensuring raw S3 bucket endpoints remain sealed from direct public exposure.
- Key Deliverables:
  - 01 Compact, scanned Docker Image stored securely in an Amazon ECR Private Repository.
  - 01 Configured Amazon Route 53 Public Hosted Zone with functional record routing.
  - 01 Hardened Amazon CloudFront Distribution featuring Origin Access Control protection, yielding over 65% latency reduction.

### Challenges Faced and Solutions:
- Challenges Faced:
  - When provisioning an Amazon CloudFront Distribution for the first time on the newly created AWS account, the deployment was restricted by default service quota policies and automated security verification checks, temporarily preventing distribution activation.
  - Following CloudFront Distribution deployment against the S3 origin, browsing to the CloudFront domain returned an HTTP 403 Forbidden AccessDenied error.
- Solutions:
  - Proactively reached out to **AWS Support**, submitting an inquiry detailing the architecture and experimental CDN workloads intended for the **FCAJ** internship program. Following direct communication and validation, AWS Support verified the use case and enabled CloudFront Distribution provisioning on the account.
  - Discovered that although Origin Access Control had been assigned, the S3 Bucket Policy needed an explicit grant for s3:GetObject to the CloudFront Service Principal with an ArnLike condition matching the distribution ARN. Injected the generated policy into the S3 bucket configuration, resolving the 403 error.
