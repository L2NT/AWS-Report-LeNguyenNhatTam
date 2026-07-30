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
| Mon | - Set up 4 CloudWatch Alarms (lambda-errors, lambda-duration, lambda-throttles, apigateway-5xx) + an SNS Topic to send alerts by email | 20/07/2026 | 20/07/2026 | |
| Tue | - Enable S3 Intelligent-Tiering on the user file storage bucket to auto-optimize storage costs | 21/07/2026 | 21/07/2026 | |
| Wed | - Went to the office in person. Added CSRF protection to the Google login flow: generate `state = crypto.randomUUID()` stored in `sessionStorage`, verify it in `verifyOAuthState()` on callback | 22/07/2026 | 22/07/2026 | |
| Thu | - Test 5 CSRF scenarios (normal login, valid state format, simulated CSRF attack rejected at the app layer, valid state with a forged code rejected by Cognito, state cleared after use) <br> - Enable KMS encryption on DynamoDB (switch from an AWS owned key to `alias/aws/dynamodb`) | 23/07/2026 | 23/07/2026 | |
| Fri | - Add a pytest step to CodePipeline's `pre_build` phase (`backend/buildspec.yml`): run `flake8` lint + `pytest test_*_unit.py` before every build/deploy | 24/07/2026 | 24/07/2026 | |
| Sat   | - Team meeting: Review work progress, read and fix report errors among team members <br> - Attend the "FCAJ x Agentic AI Build Week powered by GenAI Fund" hackathon | 25/07/2026 | 25/07/2026 | |


### Week 5 Achievements:

* Rolled out 4 CloudWatch Alarms + SNS to proactively catch errors/performance issues instead of waiting on user reports.
* Enabled S3 Intelligent-Tiering to optimize storage costs for user-uploaded documents.
* Added 2-layer CSRF protection to the Google login flow, fully tested across 5 scenarios including a simulated attack.
* Enabled KMS encryption on the DynamoDB user profiles table, with full audit trail via CloudTrail.
* Added a pytest step to CodePipeline (`pre_build`) - a new quality/security gate before build & deploy.
* Held a team meeting, reviewed work progress, and collaborated on fixing errors in the report among team members.
* Attended the "FCAJ x Agentic AI Build Week powered by GenAI Fund" hackathon (25/07/2026) - see section 4.2 for details.
