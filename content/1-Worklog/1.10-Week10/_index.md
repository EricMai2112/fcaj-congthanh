---
title: "Week 10: UI/UX Polish, Testing, Automated Alarms, and Demo Video"
date: 2026-07-27
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Weekly Topic:
User interface refinement, full-scale integration testing, automated alarms via SNS, and live project demo recording

### Weekly Objectives:
- Polish Chatpulse client frontend: optimize mobile and desktop responsiveness, implement fluid messaging dynamics.
- Execute full validation spanning user registration, OTP delivery, real-time messaging, file transfers, and network disconnection handling.
- Establish CloudWatch Alarms for compute and memory utilization linked to automated email notifications via Amazon SNS.
- Package Release v1.0.0 code artifacts and record an in-depth technical demo video showcasing live production architecture and cloud features on AWS.

### Daily Worklog Details (27/07/2026 - 31/07/2026):

| Date | Day | Tasks / Work Description | Hands-on Lab / Project Module | References |
| :--- | :--- | :--- | :--- | :--- |
| 27/07/2026 | Mon | - Refined Chatpulse frontend: optimized room navigation sidebar with real-time presence indicators.<br>- Integrated lightbox image preview modals and auditory notification cues for incoming messages.<br>- Validated responsive behaviors across desktop viewports and mobile screens. | Project Chatpulse: UI/UX polish and mobile responsive optimization | [React UI Best Practices](https://react.dev/learn) |
| 28/07/2026 | Tue | - Established end-to-end integration test suites:<br>+ Case 1: Account registration, SES OTP email dispatch, and account activation.<br>+ Case 2: JWT login, WebSocket handshake, and real-time bidirectional message distribution.<br>+ Case 3: S3 Pre-signed URL document and avatar uploads, with multi-client asset rendering.<br>+ Case 4: Exception handling for network dropouts and automatic socket reconnection. | Project Chatpulse: Full-spectrum integration testing and validation | [End-to-End Testing Strategies](https://martinfowler.com/articles/practical-test-pyramid.html) |
| 29/07/2026 | Wed | - Configured proactive CloudWatch Alarms for system reliability:<br>+ Alarm 1: EC2 CPU utilization exceeding 75% for 10 minutes.<br>+ Alarm 2: ElastiCache memory usage surpassing 80%.<br>- Linked alarms to an Amazon SNS Topic configured to dispatch operational alerts to the engineering inbox. | Project Chatpulse: Proactive monitoring with CloudWatch Alarms and SNS escalation | [Amazon CloudWatch Alarm Actions](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) |
| 30/07/2026 | Thu | - Packaged production release v1.0.0 and tagged git commits.<br>- Authored an operational runbook detailing configuration variables and disaster recovery procedures.<br>- Prepared presentation slide decks and aligned talking points for final architectural review. | Project Chatpulse: Release packaging v1.0.0 and technical presentation preparation | [AWS Project Presentation Guide](https://aws.amazon.com/architecture/) |
| 31/07/2026 | Fri | - Recorded a comprehensive video demonstration:<br>+ Part 1: Problem statement and AWS Well-Architected system design walkthrough.<br>+ Part 2: Live production demonstration covering messaging sync, S3 media uploads, CloudWatch log streams, and AWS WAF rate-limit blocks.<br>+ Part 3: Live verification of CloudWatch Alarms firing email notifications via SNS.<br>- Uploaded demo video artifacts. | Project Chatpulse: Demonstration video production and architectural evidence | [Screen Recording & Presentation Tools](https://obsproject.com/) |

### Knowledge Acquired and Key Deliverables:
- Knowledge Acquired:
  - Integration testing techniques: resolving asynchronous race conditions and client reconnection states over WebSocket protocols.
  - Operational Excellence pillar implementation: self-monitoring infrastructure that autonomously flags anomalies before service degradation occurs.
  - Technical communication proficiency: conveying cloud architectural decisions through structured demonstrations.
- Key Deliverables:
  - Responsive Chatpulse frontend user interface.
  - Test catalog achieving 100% pass rates across all functional user journeys.
  - 02 Active CloudWatch Alarms safeguarding EC2 compute and ElastiCache memory.
  - 01 Technical Demonstration Video validating the end-to-end cloud platform.

### Challenges Faced and Solutions:
- Challenge: When client devices experienced temporary network dropouts, the WebSocket connection severed, leaving client views desynchronized with messages dispatched during offline periods.
- Solution: Enhanced client architecture: used Socket.io reconnect lifecycle events to invoke a message synchronization API pulling all unread items into the application state upon reconnection. This prevented message loss across intermittent connections.
