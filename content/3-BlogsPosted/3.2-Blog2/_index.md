---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# COLD START IN SERVERLESS: WHY MY CHATBOT OCCASIONALLY FAILS TO RESPOND

## Introduction

Hi everyone, our team is building a document Q&A chatbot project (RAG), running entirely serverless: API Gateway + Lambda (Docker container) for the backend, Amazon Bedrock for LLM/Embeddings, FAISS for vector search. The system supports 3 RAG modes: Standard, Self-RAG, and Co-RAG (using 3 parallel agents: Semantic FAISS, Keyword BM25, Conceptual LLM).

While building the Co-RAG mode, I ran into an annoying phenomenon: the same question, the same document, sometimes answered in 5 seconds, sometimes returned a `503 Service Unavailable` error after exactly 30 seconds. Not a logic error, not a code bug — but an inherent characteristic of serverless architecture: cold start.

This post explains how cold start works (based on AWS's "Operating Lambda: Performance optimization" series), the real measured data I collected, and most importantly — why I haven't rushed to enable Provisioned Concurrency despite it being AWS's recommended solution.

## What is cold start?

When Lambda receives a request, if there's no "warm" execution environment ready, the service has to:

1. Download the function code (from S3 or ECR if using a container image)
2. Initialize the environment with the configured memory/runtime/config
3. Run initialization code outside the handler
4. Finally run the actual handler

This entire 1-3 process is called cold start, which can take anywhere from under 100ms to over 1 second for a typical function — but for my project, the function is a heavy Docker image (FastAPI + LangChain + FAISS + many AI dependencies), plus it has to reload the user's FAISS index from S3, so the actual cold start is much heavier.

After the handler finishes, Lambda keeps the execution environment around for an indeterminate period to reuse for the next request — called a warm start, which is much faster since it skips steps 1-3 entirely.

## The real problem: cold start stacking with API Gateway's hard limit

Something many people (including me at first) get confused about: the Lambda timeout I configured is 300 seconds (5 minutes) — way too long to be the cause of an error by itself. The real problem is API Gateway, which has a hard 29-30 second limit for integration timeout — this is an AWS platform-level limit, cannot be increased, and doesn't depend on Lambda's configuration.

When cold start happens:
- Downloading the Docker image: ~5-8s
- Loading the user's FAISS index from S3: ~8-12s
- Initializing the Bedrock connection: ~3-5s
- Actual Co-RAG processing (3 parallel agents, the slowest mode): ~5-10s

Adding these up easily exceeds the 30-second threshold → API Gateway cuts it off and returns `503`.

## Real measured data

I tested directly on production while preparing screenshots for the system testing section:

- Attempt 1 (Lambda cold after being idle): ~30s — 503 error
- Attempt 2 (independent, also cold): ~30s — 503 error
- Attempt 3 (right after attempt 2, Lambda now warm): 9.53s — success
- Attempt 4 (right after attempt 3): 4.44s — success
- Attempt 5 (right after attempt 4): 9.02s — success

At first I thought "Co-RAG always fails after 30s" — just because the first two attempts happened to both hit cold start. Testing again more carefully showed: once Lambda is warm, Co-RAG runs very fast, even faster than Standard RAG (31.2s on the first cold measurement).

## Why haven't I enabled Provisioned Concurrency right away?

AWS recommends Provisioned Concurrency as the standard solution to eliminate cold start — Lambda keeps N execution environments pre-initialized and ready to respond immediately. But I weighed this carefully before applying it:

1. **Cost is incurred even without traffic** — Provisioned Concurrency is billed hourly for each environment kept ready, regardless of whether there's a request or not. At demo/internship scale (a few dozen requests/day), this cost isn't proportionate to the benefit.
2. **The actual frequency of cold starts is low** — cold start only happens on the first call after some idle period, not every call.
3. **There's already a retry mechanism on the frontend** — my frontend version has a built-in response interceptor that automatically retries up to 10 times, 5 seconds apart, when it hits a 503/504 error. With cold start as the sole cause, the user still gets an answer after about 40-45 seconds (30s initial timeout + 5s retry wait + 5-10s for the second, now-warm call) — acceptable, though not ideal, at the current scale.
4. **There's a cheaper option if needed**: use an EventBridge Rule to "ping" the Lambda every few minutes to keep it warm — much cheaper than Provisioned Concurrency, though not a 100% guarantee (cold starts can still occur when traffic scales up and creates many new execution environments at once).

In other words: this isn't "skipping best practice" but a deliberate trade-off decision between cost and user experience, appropriate for the project's current scale — and Provisioned Concurrency or a warm-up ping will be prioritized as soon as real traffic increases.

## Conclusion

Cold start isn't a bug — it's an inherent characteristic of serverless architecture. The problem only becomes truly serious when it stacks with another hard limit elsewhere in the system (here, API Gateway's 30s). Understanding the execution environment lifecycle helps me make the right optimization decisions at the right time — instead of applying every best practice from day one without weighing the actual cost/benefit.

## Link to the article
https://aws.amazon.com/blogs/compute/operating-lambda-performance-optimization-part-1/

## Link to the post in AWS Study Group
https://www.facebook.com/groups/awsstudygroupfcj/permalink/2226685044763122/

...Image...

...Link...

...Guide...