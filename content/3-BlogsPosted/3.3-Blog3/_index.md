---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# LAMBDA TENANT ISOLATION MODE: DOES THIS NEW FEATURE SOLVE MULTI-TENANT DATA LEAK BUGS?

## Introduction

Hi everyone, our team is building a document Q&A chatbot project (RAG), serving many users at once (multi-tenant): each person logs in via Cognito, uploads their own documents, and data must be completely isolated between users. The backend runs on a single Lambda function as a Docker container, serving all users.

This was the most serious bug I've ever encountered while building this project: User A uploads a document, User B logs in and can see User A's document too, and worse — when User B deletes all of their own documents, User A's data disappears along with it. After investigating and fixing this bug by hand, I found out AWS had just announced (November 2025) a new feature for exactly this problem: Lambda Tenant Isolation Mode. This post recounts the real debugging process, explains the new feature, and — most importantly — analyzes why this feature CANNOT automatically fix the bug I encountered, even though the name might suggest otherwise.

## The real bug: why did data get mixed up between users?

Lambda has a characteristic of reusing execution environments (containers) across multiple invocations to speed things up (avoiding cold start) — but by default, the environment is reused for any request of the same function, regardless of which user it comes from. In my backend code, there were 2 places that unintentionally relied on "the container staying the same across requests":

1. A global `dict` (`state`) storing `raw_documents`, `vector_store`... shared across every request on the same container.
2. The FAISS vector index used a fixed path `vectorstore/smartdoc_index` on S3 — no `user_id` in the path, so every user read/wrote to the same index file.

When 2 different users happened to be routed to the same warm container, they shared data in RAM as well as data on S3.

## What problem does Lambda Tenant Isolation Mode solve?

The new feature lets Lambda process function invocations in separate execution environments for each end-user/tenant, instead of sharing them across every request of the same function.

How it works: you pass an additional `tenant-id` parameter (via the `X-Amz-Tenant-Id` header when integrating with API Gateway) on each invocation. Lambda uses this ID to ensure the environment is only reused for the same tenant — you still get the benefit of warm starts, but there's no longer a risk of data in RAM/`/tmp` leaking across tenants.

## How I fixed the bug (before knowing about this feature)

1. `get_user_index_name(user_id)` — computes a separate FAISS path per user: `f"{user_id}/{FAISS_INDEX_NAME}"`
2. Every document/chat endpoint re-reads data fresh directly from S3/FAISS on each request, no longer relying on the global `state` variable
3. `/api/upload-url`: changed the S3 key to `uploads/{user_id}/{filename}` instead of `uploads/{filename}`

## Why DOESN'T Tenant Isolation Mode automatically fix this bug?

This is the part I want to emphasize, since it's an easy target for "why didn't you just wait for/use the built-in feature instead of doing extra work":

Tenant Isolation Mode only isolates at the compute layer — the execution environment, RAM, `/tmp`. It does not and cannot affect how the application names keys on S3 or DynamoDB. If I had only enabled Tenant Isolation Mode without fixing the S3 path (the shared `vectorstore/smartdoc_index`), then:

- The `state` variable in RAM would be correctly isolated — no user would see another user's cache within the same run.
- But when Lambda (regardless of which tenant's dedicated environment it's running in) reads the FAISS index back from S3 using the fixed path `vectorstore/smartdoc_index`, it would still read that exact same shared file — the persistent-data bug would remain completely intact, because the root cause lies at the data modeling layer (application logic), not the compute isolation layer.

In other words: Tenant Isolation Mode is a great additional defense layer for similar bugs in the future (e.g., temporary caches in `/tmp`, accidentally shared global variables) — but it doesn't replace the need to design proper per-tenant data paths at the application layer from the start. The correct fix always has to happen where the bug actually lives.

## Verification results

After the manual fix (before Tenant Isolation Mode was released), I tested again with 2 real Cognito users:
- Each user only sees their own files via `/api/files`
- Asking the AI about the "secret code" in the other person's document → the AI replies "not found in the document"
- User B deletes all their files → User A's data remains completely intact

## Conclusion

Multi-tenancy bugs are among the hardest to catch in serverless, because they only surface when 2 requests happen to land on the same warm container. Lambda Tenant Isolation Mode is a big step forward at the compute layer, but real data safety always starts at the data design layer — every per-tenant resource (S3 key, DynamoDB partition key, cache key...) needs to explicitly contain a tenant/user identifier, no matter how well the underlying compute layer isolates things.

## Link to the article
https://aws.amazon.com/blogs/compute/building-multi-tenant-saas-applications-with-aws-lambdas-new-tenant-isolation-mode/

## Link to the post in AWS Study Group
https://www.facebook.com/groups/awsstudygroupfcj/permalink/2226685264763100/

...Image...

...Link...

...Guide...