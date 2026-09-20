---
title: "Proposal"
date: 2026-06-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# ChatPulse – Real-Time Messaging & Video Calling Platform on AWS Cloud
### A Secure, AI-Augmented, and Automated CI/CD Real-Time Communication Solution on Amazon Web Services

---

### 1. Executive Summary

**ChatPulse** is a comprehensive real-time communication web platform that enables users to effortlessly connect with friends, create group chats, send instant messages, make high-quality voice and video calls, leverage smart voice accessibility, and rely on multi-tier security ranging from JWT authentication and SHA-256 password hashing to AWS WAF edge protection.

The entire system is architected, deployed, and managed directly on **Amazon Web Services** cloud infrastructure in the Singapore Region ap-southeast-1, strictly complying with the design principles of the **AWS Well-Architected Framework**. The project applies an automated Continuous Integration and Continuous Deployment CI/CD pipeline ensuring fast, secure, and reliable system releases and updates.

- **🌐 Live Demo:** [https://ericmai.io.vn](https://ericmai.io.vn)

---

### 2. Project Objectives

The ChatPulse project is engineered to achieve the following core objectives:

1. **Build a Real-Time Communication Platform:** Provide an intuitive experience for connecting friends, managing group discussions, sending instant messages with low latency, and hosting smooth, high-definition voice and video calls directly in the web browser.
2. **System Security & Data Integrity:** Implement multi-tier authentication and authorization via JWT, robust one-way SHA-256 password hashing, strict input validation against NoSQL Injection and XSS, end-to-end HTTPS and WSS encryption in transit, and AWS WAF edge firewall defense.
3. **Integrate AI Capabilities & Intelligent Accessibility:** Utilize AI models for smart conversational assistance and incorporate Amazon Polly to synthesize text messages into natural speech for enhanced user convenience.
4. **Deploy AWS Standard Cloud Infrastructure:** Design a multi-tier secured VPC architecture, optimize in-memory caching with Amazon ElastiCache Redis, enforce perimeter security via AWS WAF, and deliver content globally using Amazon CloudFront CDN.
5. **Automate the Deployment Lifecycle:** Establish an automated CI/CD pipeline to package and deploy updates to AWS, ensuring fast release iterations without service downtime.

---

### 3. Problem Statement & Value Proposition

- **Problem:** Growing demand for online communication contrasts with many existing chat platforms that still store data without strict controls or rely on simplistic authentication, creating significant data exposure risks. Furthermore, conventional applications frequently face network congestion during peak traffic, manual release routines cause service interruptions, and audio accessibility solutions remain scarce.
- **Solution:** ChatPulse delivers a modern communication solution backed by a robust multi-layer defense-in-depth architecture, including SHA-256 password hashing, strict JWT token validation, input sanitization with express-validator, and secure media access via S3 Pre-signed URLs. The platform leverages an Amazon ElastiCache Redis cluster for microsecond presence tracking and message routing, WebRTC SFU technology for smooth audio and video calling, Amazon Polly for intelligent voice synthesis, end-to-end HTTPS and WSS in-transit encryption, and perimeter protection via AWS WAF.
- **Value & Benefits:** Offers users a secure, private, and seamless environment for social connection and teamwork, optimizes operational resource utilization and infrastructure costs, and ensures high availability, stability, and future scalability.

---

### 4. System Architecture & Tech Stack

#### AWS Cloud Architecture Diagram

The entire ChatPulse system architecture is designed and deployed on Amazon Web Services cloud infrastructure in the Singapore Region ap-southeast-1, strictly adhering to a secure multi-tier VPC model comprising a Public Subnet for application servers and a Private Subnet for internal data services.

<div style="text-align: center; margin: 24px 0;">
  <img src="/images/2-Proposal/aws-architecture.jpg" alt="ChatPulse Platform Architecture on AWS Cloud" style="max-width: 100%; height: auto; border-radius: 10px; box-shadow: 0 4px 20px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.95rem; color: #64748b; margin-top: 10px; font-weight: 500; font-style: italic;">Figure 1: Comprehensive Infrastructure and Data Flow Architecture of ChatPulse on AWS Cloud in the Singapore Region ap-southeast-1</p>
</div>

#### Technology Stack Summary

| Layer | Technologies / Services | Role & Engineering Purpose |
| :--- | :--- | :--- |
| **Frontend Client** | React 19, Vite, TypeScript | High-performance SPA with optimized tree-shaking and modern bundle size. |
| | TailwindCSS v4, Radix UI | Sleek responsive styling, accessible UI components, and Dark/Light modes. |
| | Zustand, TanStack Query v5 | Client-side state synchronization and asynchronous cache management. |
| | Socket.io-client, LiveKit-client | Bidirectional WebSocket communication and WebRTC media streaming. |
| **Backend API** | Node.js, Express, TypeScript | High-throughput RESTful endpoints and real-time event orchestration. |
| | Socket.io Server, PM2 | Scalable concurrent socket connection management with process clustering. |
| | LiveKit Server SDK | Room access token dispensation and media SFU routing. |
| **Data Layer** | MongoDB Native Driver | Schema-flexible persistence for accounts, conversations, and chat history. |
| | **Amazon ElastiCache Redis** | In-memory presence detection, rate limiting, and real-time session caching. |
| **Security & Network**| **Amazon Route 53** | High-availability DNS routing for `ericmai.io.vn` and backend subdomains. |
| | **AWS Certificate Manager** | Automated SSL/TLS certificates enforcing end-to-end HTTPS and WSS encryption. |
| | **AWS WAF** | Web application firewall guarding against SQLi, XSS, and layer 7 DDoS. |
| | **Amazon CloudFront** | Edge CDN distribution delivering static assets with minimal international latency. |
| **Compute & Storage** | **Amazon EC2** | Dedicated application host running Node.js behind Nginx Reverse Proxy. |
| | **Amazon S3** | Durable object storage for production frontend artifacts and attachments. |
| **AI & Media Services**| **Amazon Polly** | Neural text-to-speech engine transforming text messages into lifelike voice. |
| | **Amazon SES** | High-deliverability transactional email service for verification codes. |
| | Gemini AI & Groq SDK | Real-time AI conversational assistance directly in chat threads. |
| **DevOps & Telemetry**| **AWS CodePipeline & CodeBuild** | Fully automated serverless CI/CD pipeline triggered on code commit. |
| | **Amazon CloudWatch** | Comprehensive metrics collection with automated alerts via CloudWatch Alarms. |

---

### 5. Technical Implementation

#### Execution Phases:
- **Research & Design:** Analyze requirements, architect AWS infrastructure according to the Well-Architected Framework, design database schema and API endpoints.
- **Backend Development:** Build RESTful API and WebSocket services using Node.js and Express, integrate JWT authentication, connect MongoDB, setup ElastiCache Redis, and LiveKit WebRTC.
- **Frontend Development:** Build Web UI with React 19 and Vite, design responsive interfaces with TailwindCSS, integrate AI conversational chatbot and Amazon Polly text-to-speech.
- **Deployment & Testing:** Deploy onto AWS, configure AWS WAF edge firewall, establish automated CI/CD pipelines, and execute comprehensive end-to-end testing.

#### Technical Requirements:
- **Backend:** Node.js, Express, TypeScript, Socket.io, LiveKit Server SDK.
- **Frontend:** React 19, Vite, TailwindCSS, Zustand, Socket.io-client.
- **Database & Cache:** MongoDB, Amazon ElastiCache Redis.
- **AWS Infrastructure:** VPC, EC2, S3, CloudFront, Route 53, CloudWatch, CodePipeline.
- **Security:** AWS WAF, SSL/TLS, JWT, SHA-256 password hashing, S3 Pre-signed URL.

---

### 6. Implementation Roadmap

- **Weeks 1–5: May 25 – Jun 26:** Master foundational AWS services including IAM, VPC, EC2, S3, RDS, DynamoDB, Serverless, Docker, CloudFront, and Route 53 via CloudJourney labs.
- **Week 6: Jun 29 – Jul 03:** Launch ChatPulse project, analyze requirements, architect system following Well-Architected principles, provision dedicated VPC and S3 Media Bucket.
- **Week 7: Jul 06 – Jul 10:** Initialize repository structure, develop Backend Auth with JWT, SHA-256 password hashing, Amazon SES email OTP integration, and deploy ElastiCache Redis.
- **Week 8: Jul 13 – Jul 17:** Build real-time chat with Socket.io, integrate LiveKit WebRTC, upload media to S3 via Pre-signed URLs, configure Route 53 and ACM SSL certificates.
- **Week 9: Jul 20 – Jul 24:** Enforce IAM Roles, configure AWS WAF firewall defense, setup CloudWatch Logs, and build automated CI/CD pipeline via CodePipeline.
- **Week 10: Jul 27 – Jul 31:** Polish React 19 and Vite web interface, integrate AI assistant and Amazon Polly, conduct comprehensive system testing, and record demo video.
- **Week 11: Aug 03 – Aug 07:** Optimize cloud expenses using S3 Lifecycle, measure system performance, and author 5 technical blog posts on AWS Study Group.
- **Week 12: Aug 10 – Aug 14:** Finalize all features, optimize codebase, complete bilingual internship report, and conclude the project acceptance.

---

### 7. Cost Estimation & Optimization Analysis

Monthly infrastructure costs are calculated using the official **[AWS Pricing Calculator](https://calculator.aws/)** for the Singapore Region ap-southeast-1, assuming continuous 730 hours/month operation:

| AWS Service | Technical Configuration Specification | Monthly Cost (USD) | Cost Optimization Strategy |
| :--- | :--- | :---: | :--- |
| **Amazon EC2** | 1 instance t3.small, 2 vCPU, 2GB RAM, 30GB EBS gp3 | **$15.20** | Hosts Backend Node.js, Socket.IO, and Nginx. Savings Plans applicable for long-term runs. |
| **Amazon ElastiCache** | 1 node cache.t3.micro Redis OSS Private Subnet | **$18.25** | High-performance in-memory presence detection and session caching. |
| **AWS WAF** | 1 Web ACL, 3 Core Managed Rule Groups, 10M requests/month | **$6.50** | Edge perimeter defense mitigating application-layer DDoS and malicious scanners. |
| **Amazon CloudFront** | Global edge distribution, approximately 50GB data transfer out | **$0.00** | Fully covered under AWS Free Tier with 1TB data transfer out per month. |
| **Amazon S3** | S3 Standard, approximately 10GB web bundle assets and user media | **$0.25** | Automated S3 Lifecycle policies transition stale files to Glacier. |
| **Amazon Route 53** | 1 Hosted Zone `ericmai.io.vn` and 1M DNS queries/month | **$0.90** | Baseline fixed fee for enterprise-grade authoritative DNS resolution. |
| **Amazon SES** | Approximately 2,000 verification emails and notifications/month | **$0.00** | Covered under EC2 free allowance of 62,000 outgoing emails per month. |
| **Amazon Polly** | Approximately 50,000 characters synthesized per month | **$0.00** | Covered under AWS Free Tier with 5M characters per month free. |
| **AWS CodePipeline** | 1 active pipeline connected to GitHub source | **$0.00** | Covered under AWS Free Tier with 1 active pipeline free per month. |
| **AWS CodeBuild** | Approximately 60 build minutes/month using general1.small | **$0.00** | Covered under AWS Free Tier with 100 build minutes free per month. |
| **Amazon CloudWatch** | 5 Custom Metrics, 3 Alarms, 2GB log retention | **$2.10** | Retention period restricted to 14 days to prevent storage bloat. |
| **ESTIMATED MONTHLY TOTAL** | *Full Production Environment* | **~$43.20 USD / month** | *~$518.40 USD / year* |

> [!TIP]
> **Budget Safeguards:**
> 1. Multi-tier **AWS Budgets** configured with automated SNS email notifications at **$15**, **$30**, and **$40** spending thresholds.
> 2. Daily tracking via **Amazon CloudWatch Billing Alarms** preventing unforeseen utilization spikes.
> 3. Maximum utilization of the **AWS Free Tier** across S3, CloudFront, CodeBuild, and Amazon Polly.

---

### 8. Risk Assessment & Mitigation Strategies

#### Risk Matrix:
- **High WebSocket Concurrency Load:** High impact, medium probability during traffic spikes.
- **Layer 7 DDoS or XSS Injections:** High impact, medium probability at application and edge tiers.
- **JWT Token Leakage or Theft:** High impact, low probability if revocation mechanisms are missing.
- **Unplanned AWS Budget Overrun:** Medium impact, low probability when idle resources are not pruned.
- **Stale Browser Caching Post-Deploy:** Medium impact, high probability due to CDN edge cache retention.

#### Mitigation Strategies:
- **Connection and Streaming Optimization:** Offload user presence tracking to Amazon ElastiCache Redis, route audio and video media through a dedicated LiveKit SFU server, configure Nginx with keep-alive connections.
- **Perimeter and Data Security:** Deploy AWS WAF to block malicious IPs, enforce Nginx rate limiting at 30 requests/second per IP, encrypt all transit data via HTTPS and WSS, secure media uploads using S3 Pre-signed URLs.
- **Secure Session Management:** Configure short-lived 15-minute Access Tokens, manage Refresh Tokens strictly in the database with immediate revocation upon logout.
- **Cost Controls:** Set up tiered AWS Budgets with SNS email notifications at $15, $30, and $40 spending levels, establish S3 Lifecycle rules transitioning older files to Glacier.

#### Contingency Plan:
- **Automated CDN Cache Invalidation:** Embed automatic CloudFront invalidation commands into the CodeBuild buildspec immediately after uploading static assets to S3.
- **Rapid Version Rollback:** Leverage the automated CI/CD pipeline to rollback to the last stable deployment upon encountering critical runtime issues.
- **Backup and Disaster Recovery:** Maintain automated database backups and version-controlled infrastructure configs to enable swift system restoration.

---

### 9. Expected Outcomes

#### Technical Enhancements:
- Deliver a production-grade communication platform hosted at [https://ericmai.io.vn](https://ericmai.io.vn) equipped with modern real-time communication capabilities:
  - **Friend Connection & Social Interactions:** Fast user discovery, sending and receiving friend requests, contact list management, and real-time online or offline presence tracking.
  - **Direct & Group Conversations:** Dynamic group chat creation, member permission controls, low-latency instant messaging, and secure file or photo sharing via Amazon S3.
  - **Real-Time Media & AI Accessibility:** High-definition voice and video calls powered by WebRTC SFU, neural text-to-speech accessibility via Amazon Polly, and conversational AI assistance.
- Architect a resilient multi-tier cloud infrastructure conforming to the 6 pillars of the AWS Well-Architected Framework, providing high availability, scalability, and minimal latency.
- Automate the end-to-end release lifecycle using serverless CI/CD pipelines via AWS CodePipeline and AWS CodeBuild.

#### Practical and Long-Term Value:
- Provide users with a secure and private workspace backed by robust JWT authentication, SHA-256 password hashing, and AWS WAF perimeter defense.
- Maintain cost-effective operations with an optimized cloud budget, maximizing AWS Free Tier benefits and creating an ideal foundation for future scaling.
- Establish a reliable foundation for future integrations of intelligent AI services and multimedia communication features.