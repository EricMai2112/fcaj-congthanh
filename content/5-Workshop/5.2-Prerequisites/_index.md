---
title: "Prerequisites"
date: 2026-06-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---


Before beginning technical deployment for the ChatPulse project, completing prerequisite configurations across cloud accounts, local development workstations, source code repositories, and external data services ensures a smooth and secure workshop execution.

---

### 1. AWS Account & IAM User Provisioning

- **Active AWS Account:** An active AWS account in good standing, ideally eligible for AWS Free Tier benefits to optimize operational costs.
- **Dedicated IAM User:** Rather than using the Root account for daily activities, provision a dedicated administrative IAM user named `eric-thanh` with appropriate administrative permissions.
- **Active Access Keys:** Generate an active Access Key ID and Secret Access Key pair to enable remote tool connections and programmatic administration.
- **AWS CLI Configuration:** Install the AWS CLI on your local computer, authenticate using your IAM user access credentials, and set the default operational region to ap-southeast-1.

<div style="text-align: center; margin: 20px 0;">
  <img src="/images/5-Workshop/5.2-Prerequisite/iam-user-setup.jpg" alt="IAM User eric-thanh Configuration Evidence" style="max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,0.12); border: 1px solid #e2e8f0;" />
  <p style="font-size: 0.9rem; color: #64748b; margin-top: 8px; font-style: italic;">Figure 5.2: Configuration and security credentials proof of IAM User eric-thanh</p>
</div>

---

### 2. Local Development Workstation

- **Node.js Runtime:** Install a stable LTS release of Node.js to test dependencies and run local scripts.
- **Version Control System:** Install Git for managing codebase versions and remote repository operations.
- **Code Editor:** Prepare a modern development editor such as Visual Studio Code.
- **SSH Key Pair:** Generate and securely store an Amazon EC2 SSH Key Pair in `.pem` format from the AWS Console to enable remote terminal access.

---

### 3. GitHub Source Code Repository

Ensure the ChatPulse codebase is organized on GitHub under the primary `main` branch, comprising two essential architectural components:

- **Frontend Directory:** Contains the client web interface built with React 19, Vite, and TailwindCSS.
- **Backend Directory:** Contains the server application handling API routing and real-time events via Node.js, Express, Socket.io, and TypeScript.

---

### 4. External Data Services & API Credentials

- **MongoDB Atlas Database:** Provision a cloud database cluster on MongoDB Atlas, configure IP allowlists, and prepare a secure connection URI for user accounts and chat history.
- **LiveKit WebRTC Credentials:** Acquire LiveKit SFU connection parameters including Server URL, API Key, and Secret Key to power high-definition voice and video calling.
- **Conversational AI API Key:** Obtain an active API key from Google Gemini or Groq to support intelligent conversational chatbot features.

---

### 5. Custom Domain Registration

- **Domain Acquisition:** Register and acquire the custom domain `ericmai.io.vn` via accredited registrar Nhan Hoa to support real-world production deployment and SSL certificate binding.
- **DNS Administration Access:** Prepare administrative control panel credentials at Nhan Hoa to facilitate Name Server delegation to Amazon Route 53 during deployment.
