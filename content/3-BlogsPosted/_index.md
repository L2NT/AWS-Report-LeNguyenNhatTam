---
title: "Blogs Posted"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Here are 3 technical blog posts I wrote and posted on [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj), each based on an official AWS Blog article and directly connected to something I actually implemented/debugged while building the project.

### Blog 1 — [EventBridge Scheduler: when should you "upgrade" from EventBridge Rule?](3.1-Blog1/)
Amazon EventBridge Scheduler is far more powerful than the traditional EventBridge Rule (1 million schedules, 270+ targets, retry/DLQ, one-time schedules...). The post connects this to using an EventBridge Rule `rate(1 minute)` to clean up unconfirmed Cognito users in my project, and analyzes why Rule is still the sensible choice at the current scale instead of jumping straight to Scheduler.

### Blog 2 — [Amazon Bedrock Landing Zone Architecture](3.2-Blog2/)
*This post was written by teammate Phong, and counts toward the group's shared blog quota as required by the FCAJ program.* Analyzes the baseline architecture for deploying Amazon Bedrock within an AWS Landing Zone: network security via PrivateLink & VPC Lattice, centralized identity management under least-privilege principles, and centralized governance using Service Control Policies (SCPs) with CloudTrail audit trails.

### Blog 3 — [Lambda Tenant Isolation Mode: does this new feature solve multi-tenant data leak bugs?](3.3-Blog3/)
Analyzes the Lambda Tenant Isolation Mode feature (Nov 2025) in the context of a real cross-user data leak bug I debugged and manually fixed in my project — and why this new compute-level isolation feature cannot replace properly designing per-tenant data paths at the application layer.