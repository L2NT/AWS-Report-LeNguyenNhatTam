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

### Blog 2 — [Cold start in serverless: why my chatbot occasionally fails to respond](3.2-Blog2/)
Explains how AWS Lambda cold start/warm start works and why it stacks with API Gateway's hard 30-second limit to cause 503 errors. Includes real measured data from a Co-RAG bug in my project, and the reasoning for not immediately enabling Provisioned Concurrency despite it being AWS's standard recommendation.

### Blog 3 — [Lambda Tenant Isolation Mode: does this new feature solve multi-tenant data leak bugs?](3.3-Blog3/)
Analyzes the Lambda Tenant Isolation Mode feature (Nov 2025) in the context of a real cross-user data leak bug I debugged and manually fixed in my project — and why this new compute-level isolation feature cannot replace properly designing per-tenant data paths at the application layer.