---
title: "Overview"
date: 2026-06-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---


### 1. Overview

This hands-on workshop thoroughly documents the process of building and testing the cloud infrastructure for the **ChatPulse** real-time messaging and video calling platform on **Amazon Web Services**.

The workshop focuses on:

- Establishing a secure and isolated VPC network architecture with public subnets for compute workloads and private subnets for backend data services.
- Configuring an EC2 application host running Node.js, Express, and Socket.io behind an Nginx Reverse Proxy for real-time WebSocket communication.
- Deploying an Amazon ElastiCache Redis cluster to track online presence states and route instant messages with microsecond latency.
- Configuring object storage on Amazon S3 with secure, time-limited Pre-signed URLs for media attachments.
- Accelerating global content delivery via CloudFront, configuring Route 53 DNS, issuing ACM SSL certificates, and deploying AWS WAF for edge perimeter defense.

Through this practical implementation, the system design adheres to the standards of the AWS Well-Architected Framework, placing special emphasis on two core pillars: Security and Cost Optimization.

---

### 2. Architecture Blueprint

The entire system is deployed within the AWS Singapore Region ap-southeast-1:

<div style="text-align: center; margin: 24px 0;">
  <img src="/images/2-Proposal/aws-architecture.jpg" alt="ChatPulse Architecture on AWS" style="max-width: 100%; height: auto; border-radius: 10px; box-shadow: 0 4px 16px rgba(0,0,0,0.1); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.95rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.1: End-to-End ChatPulse Infrastructure on AWS Cloud</p>
</div>

---

### 3. Operational Environment Specifications

- **Production Domain:** [https://ericmai.io.vn](https://ericmai.io.vn)
- **AWS Region:** Region Singapore ap-southeast-1
- **Quick Test Account:** `mait58674@gmail.com` / Password: `123123`
