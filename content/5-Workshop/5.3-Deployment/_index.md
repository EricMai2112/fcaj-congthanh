---
title: "Deployment Steps"
date: 2026-06-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---


The end-to-end cloud deployment workflow for **ChatPulse** on **Amazon Web Services** is structured into 7 systematic technical steps:

---

### Step 1: VPC Network, Subnet & EC2 Backend Host Setup

Configure core networking and compute infrastructure running RESTful APIs and real-time Socket engines:

#### 1. VPC Network Configuration:
- Use the Default VPC in the Singapore ap-southeast-1 region with the CIDR block `172.31.0.0/16`.
- Identify the Public Subnet associated with a Route Table routing to an Internet Gateway for handling inbound internet traffic.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/vpc.jpg" alt="VPC Details and CIDR block" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.3: VPC details page displaying VPC ID and CIDR block 172.31.0.0/16</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/routetables.jpg" alt="Subnet Route Table associated with Internet Gateway" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.4: Subnet Route Table associated with Internet Gateway</p>
</div>

#### 2. EC2 Host Launch & Elastic IP Association:
- Launch an Amazon EC2 instance of size `t3.micro` running Ubuntu Server within the Public Subnet (`subnet-0f379510e7e053fd0`), named `ChatPulse-Backend-Server`.
- Allocate and associate an Elastic IP address (`54.254.6.80`) directly with the instance to prevent IP changes across reboots.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/ec2.jpg" alt="EC2 Instances management console running ChatPulse-Backend-Server" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.5: EC2 Instances console showing instance ChatPulse-Backend-Server in Running state</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/ec2details.jpg" alt="Instance Details tab showing Public IPv4 and Elastic IP" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.6: Instance Details tab showing Public IPv4 and associated Elastic IP 54.254.6.80</p>
</div>

#### 3. Security Group Configuration for EC2:
Configure Inbound Rules for the application server Security Group:
- **Port 22 (SSH):** Restrict administrative access to your development machine's IP.
- **Port 80 (HTTP) & Port 443 (HTTPS):** Open to all traffic (`0.0.0.0/0`) for REST API requests and WebSocket WSS handshakes.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/security_groups.jpg" alt="EC2 Security Group Inbound Rules" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.7: EC2 Security Group Details page showing Inbound Rules opening ports 22, 80, and 443</p>
</div>

#### 4. Node.js Runtime & Nginx Reverse Proxy Setup:
- Install Node.js LTS, PM2 process manager, and Nginx web server on the EC2 host.
- Configure Nginx as a Reverse Proxy receiving traffic on ports 80/443 and forwarding requests to the local Node.js application port. Enable `proxy_set_header Upgrade $http_upgrade` and `proxy_set_header Connection "upgrade"` directives to preserve continuous Socket.IO bidirectional streams.
- Manage persistent background process execution and automated recovery using PM2.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/pm2_status.jpg" alt="Backend Node.js operational status via PM2" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.8: Terminal console displaying pm2 status showing the backend Node.js process in online state</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/nginx_status.jpg" alt="Nginx Reverse Proxy service status" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.9: Terminal console displaying Nginx service status in active (running) state</p>
</div>

---

### Step 2: Amazon ElastiCache Redis & MongoDB Atlas Setup

Deploy in-memory session caching, real-time presence detection, and core persistent database storage:

#### 1. Amazon ElastiCache Redis Cluster Provisioning:
- Provision an ElastiCache Redis cluster using node type `cache.t3.micro` within the internal VPC boundary.
- Configure an ElastiCache Security Group accepting inbound TCP traffic exclusively on port `6379` originating from the EC2 Backend Security Group.
- Integrate the Redis client within Node.js to persist Socket IDs, govern chat rooms, and track real-time user presence (Online, Offline, Typing) with sub-millisecond responsiveness.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/elasticache.jpg" alt="Amazon ElastiCache Redis Cluster" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.10: ElastiCache management page showing Redis cluster in Available state</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/elasticache_details.jpg" alt="Redis Cluster Connectivity & Security Details" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.11: Redis Cluster Connectivity & Security tab showing internal connection Endpoint and Port 6379</p>
</div>

#### 2. MongoDB Atlas Database Integration:
- Configure Network Access on MongoDB Atlas whitelisting the EC2 Elastic IP (`54.254.6.80`) accessed via a dedicated database user.
- Maintain core collections: Users, Conversations, and Messages for long-term chat persistence and account profiles.

---

### Step 3: Amazon S3 Static Storage, Route 53 DNS & ACM SSL Certificates

Prepare frontend artifact distribution and transit encryption infrastructure:

#### 1. Amazon S3 Bucket Creation:
- Create a dedicated S3 Bucket to host compiled frontend static bundles (`dist/`).
- Enforce strict private bucket access with Origin Access Control (OAC), restricting asset delivery exclusively through Amazon CloudFront.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/s3.jpg" alt="Amazon S3 Bucket hosting frontend static distribution" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.12: Amazon S3 console displaying the storage bucket for frontend static build artifacts</p>
</div>

#### 2. Domain Configuration with Amazon Route 53:
- Verify domain registration status for `ericmai.io.vn` on Nhan Hoa domain registrar:

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/domain.jpg" alt="Active status of domain ericmai.io.vn at Nhan Hoa" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.13: Nhan Hoa domain management dashboard displaying active status for ericmai.io.vn</p>
</div>

- Configure Name Server delegation at Nhan Hoa pointing to Amazon Route 53 DNS servers:

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/name_server_dns.jpg" alt="Name Server configuration on Nhan Hoa dashboard" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.14: Name Server configuration at Nhan Hoa delegating DNS management to Route 53 servers</p>
</div>

- Create a Public Hosted Zone for the primary domain `ericmai.io.vn` and configure core DNS records:
  - **Record A (Alias):** Route root domain `ericmai.io.vn` to the CloudFront CDN distribution endpoint.
  - **Record A (Subdomain Backend):** Route backend subdomain `api.ericmai.io.vn` to the EC2 Elastic IP (`54.254.6.80`).

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/route53.jpg" alt="Route 53 DNS records configuration" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.15: Route 53 Hosted Zone details page showing active DNS records</p>
</div>

#### 3. SSL/TLS Certificate Issuance with AWS Certificate Manager (ACM):
- Request a free public wildcard certificate covering `*.ericmai.io.vn` and `ericmai.io.vn` in the US East N. Virginia (`us-east-1`) region for CloudFront compatibility.
- Complete domain ownership verification via automated Route 53 DNS CNAME record validation.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/acm.jpg" alt="AWS Certificate Manager SSL Certificate" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.16: AWS Certificate Manager console displaying SSL certificate in Issued status</p>
</div>

---

### Step 4: CloudFront CDN Distribution & AWS WAF Firewall Setup

Establish global edge distribution combined with edge security defenses:

#### 1. Amazon CloudFront Distribution Setup:
- Provision a new CloudFront distribution with its primary origin pointing to the frontend S3 Bucket.
- Attach the ACM SSL certificate to enforce HTTPS encryption across all global edge locations.
- Configure Alternate Domain Names (CNAMEs) matching the Route 53 domain configuration (`ericmai.io.vn`).
- Configure Custom Error Responses (redirecting HTTP 403 and 404 error codes to `/index.html` with response code `200 OK`) to support Single Page Application (SPA / React Router) client-side routing.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/cloudfront.jpg" alt="Amazon CloudFront Distribution Configuration" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.17: Amazon CloudFront console displaying the CDN distribution in Enabled status</p>
</div>

#### 2. AWS WAF Web Application Firewall Activation:
- Provision a Web ACL in AWS WAF and attach it directly to the CloudFront distribution.
- Activate AWS Managed Rules: `AWSManagedRulesCommonRuleSet` and `AWSManagedRulesKnownBadInputsRuleSet` to mitigate Layer-7 DDoS, Cross-Site Scripting (XSS), SQLi, and automated vulnerability scanners.

---

### Step 5: Amazon Polly Voice Accessibility & Amazon SES Setup

Integrate dedicated cloud services powering core chat ecosystem workflows:

#### 1. Amazon Simple Email Service (SES) Setup:
- Add and verify domain identity or sender email on Amazon SES.
- Configure SPF and DKIM authentication records on Route 53 to elevate sender reputation and prevent spam classification.
- Integrate AWS SDK in the backend to automatically dispatch registration confirmation emails and password recovery OTP codes.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/ses_gmail.jpg" alt="Verified domain identity on Amazon SES" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.18: Amazon SES console showing sender identity in Verified status</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/received_gmail.jpg" alt="Transactional password reset OTP email in Gmail" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.19: Gmail inbox receiving automated password reset OTP email dispatched via Amazon SES</p>
</div>

#### 2. Text-to-Speech Integration with Amazon Polly:
- Configure backend IAM roles and AWS SDK authorization to invoke Amazon Polly APIs.
- Deploy an API endpoint converting text message payloads into natural audio speech (MP3 format) for in-chat audio accessibility.

---

### Step 6: Automated CI/CD Pipeline with AWS CodePipeline & AWS CodeBuild

Automate the complete release lifecycle from code commit to CDN distribution deployment:

#### 1. AWS CodeBuild Project Setup:
- Create a new CodeBuild project using a standard Linux Ubuntu container with Node.js runtime.
- Maintain a `buildspec.yml` file in the frontend repository root defining the build lifecycle:
  - **install:** Install dependency packages (`npm install`).
  - **build:** Inject environment variables and compile the React/Vite app (`npm run build`).
  - **post_build:** Synchronize static assets to S3 and invalidate the CloudFront edge cache:
    ```bash
    aws s3 sync dist/ s3://<bucket-name> --delete
    aws cloudfront create-invalidation --distribution-id <DISTRIBUTION_ID> --paths "/*"
    ```
- Assign an IAM Service Role to CodeBuild with permissions for S3 bucket writes and CloudFront cache invalidations.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/codebuild.jpg" alt="AWS CodeBuild project configuration" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.20: AWS CodeBuild project management interface displaying build environment and execution history</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/buildspec.jpg" alt="buildspec.yml file configuration" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.21: Structure of buildspec.yml defining build phases, S3 sync, and CloudFront invalidation</p>
</div>

#### 2. Automated Pipeline with AWS CodePipeline:
- Create a CodePipeline linked to the GitHub repository via GitHub Webhooks, automatically triggered upon merging commits into the `main` branch.
- Connect Source Stage (GitHub) with Build Stage (AWS CodeBuild).
- When developers push code (`git push`), the entire workflow—compilation, S3 upload, and CloudFront cache invalidation—executes automatically without manual intervention.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/pipeline.jpg" alt="AWS CodePipeline automated release flow" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.22: AWS CodePipeline CI/CD pipeline showing Source and Build stages successfully executed</p>
</div>

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/pipeline_details.jpg" alt="CodePipeline execution details and stages" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.23: Detailed execution logs and automated deployment steps in AWS CodePipeline</p>
</div>

---

### Step 7: Telemetry, Monitoring & Alerting with Amazon CloudWatch

Implement hardware telemetry and real-time application health monitoring:

#### 1. CloudWatch Agent Setup on EC2:
- Attach IAM Role `EC2-CloudWatchAgent-Role` to the EC2 host granting permissions to stream metrics and system logs to CloudWatch.
- Stream continuous hardware metrics: CPU Utilization, available RAM memory, and Inbound/Outbound network throughput.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/ec2_cloudwatch.jpg" alt="Amazon CloudWatch Metrics monitoring EC2" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.24: CloudWatch Metrics graphs tracking EC2 hardware telemetry (CPU Utilization, Network)</p>
</div>

#### 2. Automated CloudWatch Alarms:
- Create an operational alarm: Transition to ALARM state whenever EC2 CPU Utilization exceeds 80% continuously for 5 minutes.
- Connect the alarm action to Amazon SNS to dispatch immediate email notifications to system administrators upon high system load.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.3-Deployment/cloudwatch_alarm.jpg" alt="Amazon CloudWatch Alarms management" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.25: Amazon CloudWatch Alarms console displaying configured threshold alarms</p>
</div>
