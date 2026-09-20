---
title: "Week 3: Cloud Databases RDS, DynamoDB, and CloudWatch Monitoring"
date: 2026-06-08
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Weekly Topic:
Deploying managed cloud databases Amazon RDS, Amazon DynamoDB, and full-stack observability with Amazon CloudWatch

### Weekly Objectives:
- Provision a secure relational database cluster with Amazon RDS PostgreSQL isolated in Private Subnets following multi-AZ design patterns.
- Practice with NoSQL distributed storage on Amazon DynamoDB, implement high-performance schema patterns, and configure Point-in-Time Recovery.
- Install and configure the CloudWatch Unified Agent on EC2 Linux instances to ingest custom OS metrics and stream web server access and error logs.
- Build centralized CloudWatch Dashboards and establish automated CloudWatch Alarms dispatching proactive notifications via Amazon SNS.

### Daily Worklog Details (08/06/2026 - 12/06/2026):

| Date | Day | Tasks / Work Description | Hands-on Lab / Project Module |
| :--- | :--- | :--- | :--- |
| 08/06/2026 | Mon | - Researched Amazon RDS features.<br>- Created a DB Subnet Group across 2 Private Subnets in distinct Availability Zones.<br>- Provisioned an Amazon RDS PostgreSQL instance class db.t3.micro, enabled Storage Auto-scaling, and configured Automated Backups. | [000005 - Provisioning Amazon RDS PostgreSQL](https://000005.awsstudygroup.com/) |
| 09/06/2026 | Tue | - Established Security Group chaining: allowed Inbound port 5432 exclusively originating from the EC2 Application Security Group ID.<br>- Installed postgresql-client on the EC2 instance and executed connection tests via Private DNS endpoint.<br>- Created database schemas and validated CRUD operations. | [000005 - Securing and Connecting Amazon RDS](https://000005.awsstudygroup.com/) |
| 10/06/2026 | Wed | - Explored Amazon DynamoDB key-value store architecture.<br>- Created a DynamoDB Table with Partition Key userId and Sort Key timestamp.<br>- Executed operations via CLI and Console, configured Time-to-Live for automated data pruning, and enabled Point-in-time Recovery. | [000060 - Working with Amazon DynamoDB](https://000060.awsstudygroup.com/) |
| 11/06/2026 | Thu | - Deployed CloudWatch Unified Agent on Linux EC2 instance.<br>- Attached IAM Role with CloudWatchAgentServerPolicy to the EC2 instance.<br>- Configured config.json to collect Memory Utilization metrics and stream Nginx logs to CloudWatch Log Groups. | [000008 - CloudWatch Metrics and Logs Monitoring](https://000008.awsstudygroup.com/) |
| 12/06/2026 | Fri | - Constructed a centralized CloudWatch Dashboard tracking EC2 CPU utilization, RAM consumption, Disk IOPS, and RDS active connections.<br>- Configured 2 CloudWatch Alarms: EC2 CPU above 80% for 5 minutes and RDS FreeStorageSpace below 1GB.<br>- Integrated Amazon SNS Topic triggering instant email alerts upon state transition to Alarm. | [000008 - Creating CloudWatch Dashboards and Alarms](https://000008.awsstudygroup.com/) |

### Knowledge Acquired and Key Deliverables:
- Knowledge Acquired:
  - Architectural defense for cloud data stores: avoid Public IPs for databases, isolate within private network tiers, and enforce Security Group Chaining.
  - Operational distinction between transactional relational databases in RDS and horizontal scalability in DynamoDB.
  - Understanding hypervisor-level metrics versus operating system internal metrics requiring agent telemetry.
- Key Deliverables:
  - 01 RDS PostgreSQL database active in Private Subnets, connected securely from EC2.
  - 01 DynamoDB table with automated Time-to-Live expiration and Point-in-time Recovery protection.
  - 01 Centralized CloudWatch Dashboard and 2 automated Alarms linked to an Amazon SNS email topic.

### Challenges Faced and Solutions:
- Challenge: Memory utilization was missing from default EC2 CloudWatch metrics, preventing memory exhaustion alerts.
- Solution: Learned that the AWS hypervisor cannot inspect guest operating system memory for privacy boundaries. Solved this by deploying the CloudWatch Unified Agent with an associated IAM role, publishing the custom memory metric directly to CloudWatch.
