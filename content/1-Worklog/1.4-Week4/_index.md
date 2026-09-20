---
title: "Week 4: Serverless, Infrastructure as Code, and Well-Architected"
date: 2026-06-15
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Weekly Topic:
Serverless architecture with AWS Lambda and API Gateway, Infrastructure as Code, and AWS Well-Architected Framework

### Weekly Objectives:
- Master Serverless computing models: implement event-driven serverless functions with AWS Lambda and expose RESTful endpoints via Amazon API Gateway.
- Adopt Infrastructure as Code engineering practices using declarative AWS CloudFormation templates and programmatic modeling with AWS CDK.
- Analyze the 5 core pillars of the AWS Well-Architected Framework and incorporate proactive cloud cost optimization principles into architectural blueprints.

### Daily Worklog Details (15/06/2026 - 19/06/2026):

| Date | Day | Tasks / Work Description | Hands-on Lab / Project Module |
| :--- | :--- | :--- | :--- |
| 15/06/2026 | Mon | - Investigated Serverless architecture paradigms: event-driven execution, on-demand pricing, and cold starts.<br>- Created first AWS Lambda function utilizing the Node.js runtime for computational workloads.<br>- Configured IAM Execution Role granting CloudWatch Logs write privileges under Least Privilege. | [000022 - Serverless Automation with AWS Lambda](https://000022.awsstudygroup.com/) |
| 16/06/2026 | Tue | - Created a REST API in Amazon API Gateway.<br>- Defined Resource /calculate with POST method, enabling Lambda Proxy Integration for request payload passthrough.<br>- Configured CORS and verified endpoints using Postman and curl. | [000066 - Serverless API with API Gateway](https://000066.awsstudygroup.com/) |
| 17/06/2026 | Wed | - Explored Infrastructure as Code principles and YAML syntax for AWS CloudFormation.<br>- Authored a CloudFormation template defining core baseline assets: an S3 Bucket with Lifecycle policies and an associated IAM Role.<br>- Deployed the stack through CloudFormation Console and tracked resource state transitions to completion. | [000037 - Infrastructure as Code with AWS CloudFormation](https://000037.awsstudygroup.com/) |
| 18/06/2026 | Thu | - Enhanced CloudFormation capabilities: implemented Parameters, Conditions, and Outputs for dynamic stack deployments.<br>- Simulated automated Rollback mechanisms by introducing a resource configuration defect.<br>- Explored programmatic cloud modeling using the AWS Cloud Development Kit with TypeScript. | - [000037 - CloudFormation Parameters & Rollback](https://000037.awsstudygroup.com/)<br>- [000038 - Cloud Development with AWS CDK](https://000038.awsstudygroup.com/) |
| 19/06/2026 | Fri | - Conducted a study of the 5 pillars of the AWS Well-Architected Framework: Operational Excellence, Security, Reliability, Performance Efficiency, and Cost Optimization.<br>- Utilized the AWS Well-Architected Tool to run a preliminary assessment on established lab workloads.<br>- Compiled a concrete Cost Optimization checklist. | - [000042 - Cost Optimization with Savings Plans](https://000042.awsstudygroup.com/)<br>- [AWS Well-Architected Framework Assessment](https://aws.amazon.com/architecture/well-architected/) |

### Knowledge Acquired and Key Deliverables:
- Knowledge Acquired:
  - Event-driven Lambda execution lifecycles, execution contexts, and cold start mitigation techniques.
  - Essential role of Amazon API Gateway handling request routing, rate limiting, and CORS headers.
  - Benefits of Infrastructure as Code: version-controlled, auditable, and repeatable cloud infrastructure without configuration drift.
  - Practical adoption of AWS Well-Architected pillars as engineering guideposts for internship technical projects.
- Key Deliverables:
  - 01 Functioning Serverless Microservice API delivering sub-100ms response latencies.
  - 01 Reusable, modular CloudFormation template for automated resource provisioning.
  - Preliminary Well-Architected Review scorecard evaluating lab environments.

### Challenges Faced and Solutions:
- Challenge: Requests dispatched from local frontend code to API Gateway failed with a browser CORS error due to missing headers.
- Solution: Discovered that when using Lambda Proxy Integration, enabling CORS in API Gateway Console only handles the OPTIONS preflight request, the Lambda function itself must explicitly return CORS response headers with Access-Control-Allow-Origin and Access-Control-Allow-Methods. Added these headers to the response payload, resolving the issue.
