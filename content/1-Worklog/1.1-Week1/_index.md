---
title: "Week 1: Internship Orientation and Security Foundation Setup"
date: 2026-05-25
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Weekly Topic:
Internship orientation, AWS culture, and cloud account security foundation setup

### Weekly Objectives:
- Understand workplace culture, regulations at Amazon Web Services Viet Nam, and the evaluation criteria of the FCAJ program.
- Establish a personal AWS Free Tier account, configure AWS Budgets and CloudWatch Billing Alerts for cost control throughout the internship.
- Implement administrative security baselines with AWS Identity and Access Management (IAM): Users, Groups, Roles, Policies, and activate Multi-Factor Authentication (MFA).
- Install, configure, and operate the AWS CLI on the local machine.

### Daily Worklog Details (25/05/2026 - 29/05/2026):

| Date | Day | Tasks / Work Description | Hands-on Lab / Project Module |
| :--- | :--- | :--- | :--- |
| 25/05/2026 | Mon | - Attended orientation session with company leadership and Mentor Nguyen Gia Hung.<br>- Learned corporate security guidelines, FCAJ internship standards, and communication channels. | [FCAJ Working Culture & Rules](https://hcm-rules.awsfcaj.com/) |
| 26/05/2026 | Tue | - Registered an individual AWS account for practical lab assignments.<br>- Enabled Multi-Factor Authentication (MFA) via Authenticator app on the Root Account.<br>- Locked down Root credentials and created a dedicated IAM Administrator user. | - [000001 - AWS Free Tier 2025 Guide](https://000001.awsstudygroup.com/)<br>- [000002 - Access Management with AWS IAM](https://000002.awsstudygroup.com/) |
| 27/05/2026 | Wed | - Studied AWS pricing models and Free Tier boundaries.<br>- Configured AWS Budgets with an initial threshold of 5 USD per month.<br>- Set up CloudWatch Billing Alarm connected to Amazon SNS to trigger email alerts at 80% budget consumption. | [000007 - Cost Management with AWS Budgets](https://000007.awsstudygroup.com/) |
| 28/05/2026 | Thu | - Installed AWS CLI v2 on local workstation.<br>- Generated IAM developer credentials and executed aws configure with default region ap-southeast-1 and JSON output.<br>- Verified CLI connectivity via aws sts get-caller-identity and aws ec2 describe-regions. | [000011 - Getting Started with AWS CLI](https://000011.awsstudygroup.com/) |
| 29/05/2026 | Fri | - Advanced IAM practice: created Groups for Developers and CloudAdmins, assigned Managed Policies.<br>- Authored Custom JSON IAM Policy adhering to the Principle of Least Privilege, allowing read-only access for EC2 and S3.<br>- Compiled Week 1 deliverables and conducted progress review with Mentor. | [000044 - Access Control with IAM Policies & Conditions](https://000044.awsstudygroup.com/) |

### Knowledge Acquired and Key Deliverables:
- Knowledge Acquired:
  - Clear understanding of the AWS Shared Responsibility Model.
  - Practical application of the Principle of Least Privilege in cloud identity governance.
  - Operational proficiency with AWS CLI command syntax, configuration profiles, and credentials management.
- Key Deliverables:
  - 01 Hardened personal AWS account with Root MFA active and operational tasks handled via IAM users.
  - 01 Active AWS Budget and CloudWatch Billing Alarm ready to detect unexpected charges.
  - Local development workstation fully provisioned with authenticated AWS CLI v2.

### Challenges Faced and Solutions:
- Challenges Faced:
  - During the registration of the personal AWS account, automated phone number verification and payment gateway validation encountered latency from the telecommunication provider, placing the account on a temporary verification hold and delaying immediate service access.
  - When configuring CloudWatch Billing Alarm, billing metrics were initially missing due to periodic billing metric aggregation delays.
- Solutions:
  - Proactively submitted an inquiry and worked directly with **AWS Support**, exchanging required identity details and clarifying the academic nature of the **FCAJ** internship program. AWS Support manually reviewed and verified the account, expediting complete activation.
  - Researched official AWS documentation, ensured Receive Billing Alerts was explicitly enabled under Root Billing Preferences, and simulated an SNS notification test to confirm alert delivery mechanisms.
