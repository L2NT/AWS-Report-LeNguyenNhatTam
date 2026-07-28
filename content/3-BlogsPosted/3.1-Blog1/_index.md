---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# EVENTBRIDGE SCHEDULER: WHEN SHOULD YOU "UPGRADE" FROM EVENTBRIDGE RULE?

## Introduction

Hi everyone, our team is building a document Q&A chatbot project (RAG): users upload a PDF/DOCX file and then chat directly with an AI based on that document's content. The whole system runs serverless on AWS — API Gateway + Lambda (packaged as Docker) for the backend, Cognito for authentication, DynamoDB + S3 for storage, and Amazon Bedrock for the LLM/Embeddings part.

While deploying, I needed a mechanism to automatically clean up Cognito accounts that registered but never confirmed their email (`UNCONFIRMED`) — if left alone, they're just "trash" in the User Pool. The solution I chose was an **EventBridge Rule** running `rate(1 minute)` to trigger a Lambda that checks and deletes expired users.

While digging deeper to write this post, I found out AWS actually has a dedicated scheduling service — **Amazon EventBridge Scheduler** — far more powerful than the traditional EventBridge Rule. This post walks through the differences between the two options, and more importantly: **why I still chose Rule for the current use case**, instead of jumping straight to Scheduler just because it's "newer".

## What is EventBridge Scheduler?

> Amazon EventBridge Scheduler is a serverless service that lets you create, run, and manage scheduled tasks at scale — one-time or recurring — across more than 270 AWS services and 6,000+ API actions, without managing any infrastructure.

Previously, if you wanted to schedule a task, the most common choice was an **EventBridge Rule** using a `cron()` or `rate()` expression. This works well, but has a few limitations:

- A maximum of **300 rules per region per account** — not ideal if you need a separate schedule for thousands of customers (e.g., each tenant in a SaaS needing its own reminder schedule).
- Only supports around 20 target types.
- No built-in retry with exponential backoff, dead-letter queue (DLQ), or time window to spread out requests.
- No support for one-time schedules — only recurring.

EventBridge Scheduler solves all of these limitations: it supports up to **1 million schedules per account** (instead of 300 rules per region), throughput up to thousands of TPS, connects to **270+ AWS services and 6,000+ API actions** (instead of ~20 targets for Rule), supports **one-time schedules** (`at()`) alongside recurring ones, has a **time window** to spread out requests, comes with built-in **retry + dead-letter queue** (retries up to 185 times over 24 hours by default), and fully supports **time zones/DST** instead of just UTC like Rule.

## The real architecture in my project

The backend Lambda is designed with **event branching**: the same function handles both HTTP requests (via API Gateway/Mangum) and periodic events from EventBridge, based on `event.get("source") == "aws.events"`. This is a minimal-effort choice — no need for a separate Lambda just to run a cron job.

## Why did I choose EventBridge Rule instead of Scheduler?

This is the part I think is most important, since it's an easy target for the "why didn't you just use the newer, more standard option" question:

1. **There's exactly 1 type of scheduled task** in the whole system — cleaning up unconfirmed users. There's no need for per-user/per-tenant schedules, so we never come close to the 300-rule limit or need Scheduler's million-schedule capacity.
2. **No need for complex retry/DLQ** — if one cleanup run fails, the next run (1 minute later) automatically retries and still cleans up the expired users correctly, no dedicated retry mechanism needed.
3. **No need for one-time schedules** — this is a permanently recurring task via `rate()`; Scheduler's standout features (one-time schedules, time windows) don't bring any benefit to this use case.
4. **Cost & operational complexity**: Scheduler is still free under the Free Tier and not significantly more expensive, but adding a new service to the architecture means one more thing to learn/maintain — at the current demo/internship scale, that's not proportionate to the benefit gained.

In other words: **Scheduler isn't "better" than Rule in an absolute sense — it's better for the exact problem it was built to solve** (scheduling at massive scale, diverse targets, needing sophisticated retry/DLQ). If this project later grows into a real SaaS with thousands of tenants, each needing their own schedule (e.g., trial expiration reminders, automated data cleanup per customer's retention policy) — that's exactly when it would make sense to move to Scheduler.

## Conclusion

EventBridge Scheduler is a genuinely powerful upgrade over EventBridge Rule, especially for multi-tenant SaaS systems that need scheduling at scale. But choosing a technology should be based on the **actual problem at hand**, not on which service is "newer". For a simple recurring task like cleaning up unconfirmed users, EventBridge Rule remains the minimal and sensible choice.

## Link to the article
https://aws.amazon.com/blogs/compute/introducing-amazon-eventbridge-scheduler/

## Link to the post in AWS Study Group
https://www.facebook.com/groups/awsstudygroupfcj/permalink/2226683848096575/

...Image...

...Link...

...Guide...