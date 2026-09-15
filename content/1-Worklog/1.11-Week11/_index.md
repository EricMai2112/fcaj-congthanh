---
title: "Week 11: Cost Optimization, Benchmarking, and Technical Blog"
date: 2026-08-03
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Weekly Topic:
Cloud cost governance and optimization, Amazon S3 Lifecycle configurations, system performance benchmarking, and technical architecture blog publishing

### Weekly Objectives:
- Conduct cloud financial analysis adhering to the AWS Well-Architected Cost Optimization pillar: model monthly budgets with AWS Pricing Calculator and execute compute right-sizing.
- Establish automated Amazon S3 Lifecycle Rules on media buckets to automate archival transitions and minimize long-term storage expenditures.
- Benchmark full-stack performance indicators including WebSocket round-trip latency and CDN TTFB across production load scenarios.
- Author a technical architecture blog post on the Chatpulse system design and publish it within the AWS Study Group community.

### Daily Worklog Details (03/08/2026 - 07/08/2026):

| Date | Day | Tasks / Work Description | Hands-on Lab / Project Module | References |
| :--- | :--- | :--- | :--- | :--- |
| 03/08/2026 | Mon | - Utilized AWS Pricing Calculator to model operating expenditures for Chatpulse serving 1,000 Daily Active Users.<br>- Analyzed cost components: EC2 compute, ElastiCache Redis, S3 capacity, CloudFront data transfer, and NAT Gateway egress.<br>- Identified potential cost leaks and established regular audit routines. | Project Chatpulse: Cost estimation and financial modeling with AWS Pricing Calculator | [AWS Pricing Calculator](https://calculator.aws/#/) |
| 04/08/2026 | Tue | - Implemented an automated S3 Lifecycle configuration rule on chatpulse-media-assets-prod:<br>+ Transition objects after 30 days from S3 Standard to S3 Standard-IA, cutting storage fees by approximately 50%.<br>+ Transition objects after 90 days into S3 Glacier Flexible Retrieval for long-term archiving.<br>+ Enforced automated cleanup of incomplete multipart uploads after 7 days. | Project Chatpulse: Implementing automated S3 storage tiering via Lifecycle Rules | [S3 Lifecycle Management](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html) |
| 05/08/2026 | Wed | - Conducted compute right-sizing audits: scrutinized actual CPU and memory utilization across EC2 instances and ElastiCache nodes.<br>- Evaluated migration to cost-efficient AWS Graviton instances in the t4g family or optimized t3.micro instances under Free Tier parameters.<br>- Devised automated off-hours shutdown schedules for staging environments using AWS Instance Scheduler. | Project Chatpulse: Compute right-sizing and operational cost governance | [AWS Cost Optimization Pillar](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html) |
| 06/08/2026 | Thu | - Benchmarked core system latency metrics for Chatpulse:<br>+ Bidirectional WebSocket transmission latency: achieved average of 24ms.<br>+ Initial page load Time to First Byte over CloudFront: decreased from 380ms down to 65ms via edge caching.<br>+ Direct S3 Pre-signed uploads maximized client uplink throughput without computational strain on backend servers. | Project Chatpulse: Performance benchmarking and metric telemetry aggregation | [Web Performance Metrics](https://web.dev/explore/fast) |
| 07/08/2026 | Fri | - Authored a Technical Blog: Designing an Enterprise Real-time Communication Platform with Ultra-low Latency, Zero-trust Security and Cost Optimization on AWS.<br>- Elucidated architectural decisions: Redis Pub/Sub horizontal scale, S3 Pre-signed direct streaming, and AWS WAF perimeter defenses.<br>- Submitted draft for Mentor review and published article on the AWS Study Group community. | Technical Blog: Authoring and publishing deep-dive cloud architecture article | [AWS Study Group Community](https://www.facebook.com/groups/awsstudygroupfcj) |

### Knowledge Acquired and Key Deliverables:
- Knowledge Acquired:
  - Principles of proactive cost optimization: an effective architecture balances technical resilience with corporate cost efficiency.
  - Amazon S3 storage classes and lifecycle automation pipelines saving recurring operational expenditures.
  - Quantitative benchmarking methodologies for distributed WebSocket and CDN-accelerated architectures.
  - Professional engineering communication and knowledge sharing within the AWS cloud community.
- Key Deliverables:
  - Detailed cost breakdown demonstrating Chatpulse operational budgets of approximately 15 to 25 USD per month for SME deployments.
  - Active S3 Lifecycle configuration enforcing automated storage optimization.
  - Verified performance benchmark report certifying low message latencies.
  - 01 Technical Blog article published on the AWS Study Group platform.

### Challenges Faced and Solutions:
- Challenge: Unanticipated cost spikes were discovered on the NAT Gateway during heavy file transfer tests, attributable to AWS data processing charges through NAT.
- Solution: Confirmed that direct client-to-S3 uploads bypassed the NAT Gateway entirely. For internal VPC-to-S3 communication, provisioned a Gateway VPC Endpoint for Amazon S3 at no additional cost. This routed all internal VPC requests directly to S3 via private AWS backbones without traversing the NAT Gateway, eliminating data processing fees.
