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

| Date | Day | Tasks / Work Description | Hands-on Lab / Project Module | References |
| :--- | :--- | :--- | :--- | :--- |
| 22/06/2026 | Mon | - Investigated containerization theory and contrasted Containers against Virtual Machines.<br>- Authored a multi-stage Dockerfile for a sample Node.js and React application.<br>- Curated dockerignore file, executed local image compilation, and verified container health via docker run. | Building lightweight production containers with multi-stage Docker | [Docker Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) |
| 23/06/2026 | Tue | - Studied Amazon Elastic Container Registry managed container repository features.<br>- Created a Private Repository fcaj-sample-app on ECR and activated automated vulnerability scanning on push.<br>- Obtained an authenticated login token via AWS CLI command aws ecr get-login-password, tagged the local image, and pushed it to ECR. | Pushing secure Docker images to Amazon ECR private repositories | [Amazon ECR User Guide](https://docs.aws.amazon.com/AmazonECR/latest/userguide/) |
| 24/06/2026 | Wed | - Explored Amazon Route 53 DNS routing mechanisms including Simple, Failover, and Latency-based policies.<br>- Initialized a Public Hosted Zone within Route 53.<br>- Configured standard DNS records: Record A pointing to EC2 IP, CNAME, and AWS Alias records. | Domain management and intelligent DNS routing with Amazon Route 53 | [Amazon Route 53 Documentation](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/) |
| 25/06/2026 | Thu | - Examined Amazon CloudFront edge infrastructure including Edge Locations, Regional Edge Caches, and Origins.<br>- Created a CloudFront Distribution pointing to the S3 Static Website Bucket.<br>- Configured Origin Access Control and updated the S3 Bucket Policy to restrict read access strictly to CloudFront. | Global content acceleration with Amazon CloudFront and OAC hardening | [Amazon CloudFront Guide](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/) |
| 26/06/2026 | Fri | - Fine-tuned CloudFront delivery performance: enabled automated gzip and Brotli compression, configured TTL Cache-Control headers.<br>- Mapped an Alias Record from Route 53 directly to the CloudFront Distribution domain.<br>- Benchmarked network latency before and after CDN caching. | CDN performance optimization: Caching behaviors and Route 53 Alias | [CloudFront Optimization](https://aws.amazon.com/caching/cdn/) |

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
