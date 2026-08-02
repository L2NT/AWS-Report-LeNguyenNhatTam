---
title: "Week 5 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
### Week 5 Objectives:

* Strengthen system monitoring with CloudWatch Alarms.
* Optimize S3 storage costs and tighten security (KMS for DynamoDB, CSRF protection for Google login).
* Add an automated test gate (pytest) to CodePipeline.
* Attend the "FCAJ x Agentic AI Build Week powered by GenAI Fund" hackathon.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Set up 4 CloudWatch Alarms (lambda-errors, lambda-duration, lambda-throttles, apigateway-5xx) + an SNS Topic to send alerts by email <br>&emsp;+ Chose specific thresholds for each alarm: lambda-errors > 5 errors/5 min, lambda-duration > 25000ms/5 min (close to the 30s timeout), lambda-throttles ≥ 1 occurrence/5 min, apigateway-5xx > 5 errors/5 min <br>&emsp;+ Created the SNS Topic, subscribed my email for alerts, confirmed the subscription via the email link | 20/07/2026 | 20/07/2026 | [Using Amazon CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) |
| Tue | - Enable S3 Intelligent-Tiering on the user file storage bucket to auto-optimize storage costs <br>&emsp;+ Created a lifecycle rule transitioning every object to `INTELLIGENT_TIERING` immediately on upload (0 days) <br>&emsp;+ Noted that AWS only applies the transition to objects ≥ 128KB — a good fit since the project's PDF/DOCX documents are usually larger than that threshold | 21/07/2026 | 21/07/2026 | [Managing storage costs with S3 Intelligent-Tiering](https://docs.aws.amazon.com/AmazonS3/latest/userguide/intelligent-tiering.html) |
| Wed | - Went to the office in person. Added CSRF protection to the Google login flow: generate `state = crypto.randomUUID()` stored in `sessionStorage`, verify it in `verifyOAuthState()` on callback <br>&emsp;+ Identified the vulnerability before fixing it: the Google Login flow through Cognito's Hosted UI had no `state` parameter, letting an attacker trick a victim into clicking a link containing a pre-built authorization code (Login CSRF/OAuth code injection) <br>&emsp;+ Added `verifyOAuthState()` to compare the returned state against the stored one, clearing it right after use to prevent replay attacks | 22/07/2026 | 22/07/2026 | [CSRF Prevention Cheat Sheet – OWASP](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html) |
| Thu | - Test 5 CSRF scenarios (normal login, valid state format, simulated CSRF attack rejected at the app layer, valid state with a forged code rejected by Cognito, state cleared after use) <br>&emsp;+ Simulated a real attack: copied a valid `state` from sessionStorage, typed a callback URL with a different `state` — confirmed it was rejected right at the app layer before ever calling Cognito <br>&emsp;+ Separately tested a valid `state` with a forged `code` — confirmed Cognito rejects it at the second layer (invalid_grant), proving the system has 2 independent layers of protection <br> - Enable KMS encryption on DynamoDB (switch from an AWS owned key to `alias/aws/dynamodb`) <br>&emsp;+ Compared the AWS owned key (free, default) with an AWS managed key (`alias/aws/dynamodb`, with CloudTrail audit trail) — chose the managed key since access tracking was needed but manual key management (as with a customer managed key) wasn't | 23/07/2026 | 23/07/2026 | [DynamoDB encryption at rest](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/EncryptionAtRest.html) |
| Fri | - Add a pytest step to CodePipeline's `pre_build` phase (`backend/buildspec.yml`): run `flake8` lint + `pytest test_*_unit.py` before every build/deploy <br>&emsp;+ Chose to place the test step in `pre_build` rather than `build`/`post_build` so the pipeline stops early on a test failure, avoiding wasted time building the Docker image unnecessarily <br>&emsp;+ Configured `flake8` to run with `--exit-zero` (lint doesn't block the build) but let `pytest` actually block the build if unit tests fail | 24/07/2026 | 24/07/2026 | [Build specification reference – CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html) |
| Sat   | - Team meeting: Review work progress, read and fix report errors among team members <br>&emsp;+ Cross-read Trọng's and Phong's reports, gave feedback on typos and inconsistent content <br> - Attend the "FCAJ x Agentic AI Build Week powered by GenAI Fund" hackathon | 25/07/2026 | 25/07/2026 | |


### Week 5 Achievements:

* Rolled out 4 CloudWatch Alarms + SNS to proactively catch errors/performance issues instead of waiting on user reports.
* Enabled S3 Intelligent-Tiering to optimize storage costs for user-uploaded documents.
* Added 2-layer CSRF protection to the Google login flow, fully tested across 5 scenarios including a simulated attack.
* Enabled KMS encryption on the DynamoDB user profiles table, with full audit trail via CloudTrail.
* Added a pytest step to CodePipeline (`pre_build`) - a new quality/security gate before build & deploy.
* Held a team meeting, reviewed work progress, and collaborated on fixing errors in the report among team members.
* Attended the "FCAJ x Agentic AI Build Week powered by GenAI Fund" hackathon (25/07/2026) - see section 4.2 for details.
