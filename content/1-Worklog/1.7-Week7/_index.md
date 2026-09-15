---
title: "Week 7: Codebase Setup, Backend Auth, SES, and ElastiCache Redis"
date: 2026-07-06
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Weekly Topic:
Project repository initialization, backend authentication engineering with Node.js and Express, Amazon SES integration, and Amazon ElastiCache Redis cluster provisioning

### Weekly Objectives:
- Establish version control structures on GitHub, standardizing branch governance for Project Chatpulse across React frontend and Node.js backend.
- Engineer robust authentication mechanisms: dual JSON Web Token flows and password hashing with bcrypt.
- Configure Amazon SES identity verification and program automated OTP dispatch services for account verification workflows.
- Deploy an Amazon EC2 application instance within a Private Subnet and provision an Amazon ElastiCache Redis cluster acting as a session store and Pub/Sub message broker.

### Daily Worklog Details (06/07/2026 - 10/07/2026):

| Date | Day | Tasks / Work Description | Hands-on Lab / Project Module | References |
| :--- | :--- | :--- | :--- | :--- |
| 06/07/2026 | Mon | - Initialized the Chatpulse GitHub Repository; enforced branch protection rules on main.<br>- Structured project boilerplates: React, Tailwind CSS, and Vite for frontend; Node.js, Express, and TypeScript for backend.<br>- Configured code quality standards with ESLint, Prettier, and established .env.example templates. | Project Chatpulse: Repository initialization, structure setup, and boilerplate | [Gitflow Workflow Guide](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) |
| 07/07/2026 | Tue | - Architected the Backend Authentication module: designed Users data schema and implemented bcrypt hashing with 10 salt rounds.<br>- Developed REST endpoints for register, login, and token refresh.<br>- Implemented dual-token architecture: short-lived Access Tokens valid for 15 minutes and Refresh Tokens valid for 7 days stored in HTTP-only cookies. | Project Chatpulse: Secure JWT authentication architecture implementation | [JWT Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/JSON_Web_Token_for_Java_Cheat_Sheet.html) |
| 08/07/2026 | Wed | - Set up Amazon SES in the Singapore region ap-southeast-1.<br>- Completed email address identity verification within the SES Sandbox environment.<br>- Integrated AWS SDK for JavaScript into backend: authored a secure OTP generator service storing 6-digit codes in Redis and transmitting HTML activation emails. | Project Chatpulse: Amazon SES integration for OTP dispatch and verification | [Amazon SES Developer Guide](https://docs.aws.amazon.com/ses/latest/dg/) |
| 09/07/2026 | Thu | - Created an ElastiCache Subnet Group across 2 Private Data Subnets.<br>- Provisioned an Amazon ElastiCache Redis cluster version 7.x with node type cache.t3.micro.<br>- Hardened Redis Security Group: restricted Inbound port 6379 strictly to the EC2 App Security Group.<br>- Configured Redis Time-to-Live parameters for transient OTP tokens and user session caches. | Project Chatpulse: Amazon ElastiCache Redis cluster provisioning | [Amazon ElastiCache Guide](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/) |
| 10/07/2026 | Fri | - Provisioned EC2 Backend Server Ubuntu 22.04 LTS inside the Private App Subnet.<br>- Installed Node.js runtime, PM2 process supervisor, and cloned application source code.<br>- Validated internal network connectivity to the ElastiCache Redis endpoint via redis-cli ping.<br>- Tested the registration and OTP verification flow. | Project Chatpulse: EC2 Private Backend deployment and Redis verification | [PM2 Production Process Manager](https://pm2.keymetrics.io/docs/usage/quick-start/) |

### Knowledge Acquired and Key Deliverables:
- Knowledge Acquired:
  - Stateless authentication models combining Access Tokens and Refresh Tokens for horizontal scalability without database session bloat.
  - SES operational mechanics: handling sandbox sending quotas, identity verification, and transactional email reliability.
  - Strategic utility of Amazon ElastiCache Redis: ultra-low latency in-memory data store supporting rapid OTP lookups, user presence states, and real-time Pub/Sub message distribution.
- Key Deliverables:
  - Fully functional Node.js and Express authentication microservice integrated with Amazon SES OTP mailing.
  - Operational, isolated Amazon ElastiCache Redis cluster in Private Data Subnets.
  - Provisioned EC2 backend instance communicating seamlessly with Redis over internal VPC pathways.

### Challenges Faced and Solutions:
- Challenge: The EC2 backend instance residing in the Private Subnet lacked outbound internet connectivity, causing npm install and git clone commands to hang.
- Solution: Inspected the routing table associated with the Private App Subnet and identified the absence of a default route pointing to the NAT Gateway. Added a 0.0.0.0/0 entry directing egress traffic to the NAT Gateway in the Public Subnet, enabling seamless package downloads while preserving inbound isolation.
