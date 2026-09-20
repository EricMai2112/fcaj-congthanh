---
title: "Week 9: Security Hardening with WAF, IAM, CloudWatch, and CI/CD"
date: 2026-07-20
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Weekly Topic:
Perimeter and identity hardening via IAM Roles and AWS WAF, centralized CloudWatch logging, and automated CI/CD pipelines

### Weekly Objectives:
- Enforce the Principle of Least Privilege: bind IAM Roles directly to EC2 compute instances for S3 and SES operations, eradicating static hardcoded credentials.
- Deploy an AWS WAF Web ACL on CloudFront to neutralize common web application vulnerabilities, prevent spam bot floods, and configure rate-based limiting.
- Implement centralized log telemetry with CloudWatch Logs Agent and establish Metric Filters tracking HTTP 4xx and 5xx errors.
- Construct an automated CI/CD deployment pipeline delivering zero-downtime updates to EC2 instances, followed by load testing.

### Daily Worklog Details (20/07/2026 - 24/07/2026):

| Date | Day | Tasks / Work Description | Hands-on Lab / Project Module |
| :--- | :--- | :--- | :--- |
| 20/07/2026 | Mon | - Created IAM Role ChatpulseEC2AppRole with scoped Custom Policies: s3:PutObject and s3:GetObject on media bucket, and ses:SendEmail on verified identity.<br>- Associated IAM Role to the EC2 instance via an Instance Profile.<br>- Purged static access key environment variables, verified that AWS SDK fetched rotating credentials via IMDSv2. | [Final Project](https://github.com/EricMai2112/chat-pulse) |
| 21/07/2026 | Tue | - Provisioned an AWS WAF Web ACL associated with the CloudFront distribution.<br>- Enabled AWS Managed Rule Sets: AWSManagedRulesCommonRuleSet and AWSManagedRulesKnownBadInputsRuleSet.<br>- Authored a Custom Rate-based Rule: Cap requests at 300 queries per 5-minute window per IP to throttle spam and denial-of-service attempts. | [Final Project](https://github.com/EricMai2112/chat-pulse) |
| 22/07/2026 | Wed | - Configured the CloudWatch Agent on EC2 to ingest PM2 application log paths.<br>- Streamed telemetry to CloudWatch Log Group aws/ec2/chatpulse/backend.<br>- Configured Metric Filters parsing for error strings and HTTP status code 500 patterns. | [Final Project](https://github.com/EricMai2112/chat-pulse) |
| 23/07/2026 | Thu | - Developed an automated CI/CD pipeline leveraging GitHub Actions.<br>- Specified workflow configuration: lint checks, unit tests, asset compilation, and automated SSH deployment to EC2 with PM2 reload.<br>- Executed test commits and confirmed successful automated deployment. | [Final Project](https://github.com/EricMai2112/chat-pulse) |
| 24/07/2026 | Fri | - Conducted stress and load testing simulating 200 concurrent active users transmitting real-time messages and querying APIs.<br>- Observed defensive responses: AWS WAF blocked aggressive IPs violating rate thresholds with HTTP 429 Too Many Requests, EC2 CPU remained below 45%.<br>- Analyzed security logs and summarized performance data. | [Final Project](https://github.com/EricMai2112/chat-pulse) |

### Knowledge Acquired and Key Deliverables:
- Knowledge Acquired:
  - Avoiding static access credentials on computing instances, leveraging IAM Roles with IMDSv2 is the standard approach for cloud security.
  - Edge mitigation: filtering malicious requests at CloudFront Edge Locations prevents bad traffic from consuming backend compute cycles and bandwidth.
  - Automation principles: continuous automated testing and deployment eliminate operational errors on production servers.
- Key Deliverables:
  - Credential-free backend application secured via IAM Instance Profiles.
  - Functional AWS WAF Web ACL thwarting spam bots and abnormal request surges.
  - CI/CD automation pipeline with centralized CloudWatch Log Streams.

### Challenges Faced and Solutions:
- Challenge: During initial load testing, administrative calls from the developer workstation were temporarily blocked by AWS WAF with an HTTP 429 response after tripping the 300-request threshold.
- Solution: Created an IP Set in AWS WAF containing the developer IP address configured as an explicit allow rule with Priority 0 before the Rate-based rule. This allowed developers to conduct internal performance experiments without disruption.
