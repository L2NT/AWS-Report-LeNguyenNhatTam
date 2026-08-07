---
title: "Week 3 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
### Week 3 Objectives:

* Review and test teammates' recent work: Trọng's Frontend authentication flow (Login/Register/Protected Route) and Nam's Bedrock/RAG optimizations.
* Finalize the Overall AWS Architecture diagram used in the Proposal and section 5.1.3, building on an early sketch from Week 1.
* Draft (design only, not yet implemented) the registration/verification flow redesign and the fix for the multi-tenancy data leak, to be built out next week.
* Attend the "Cloud Architect x Meet Up" community event.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon-Tue | - Review and test Trọng's Frontend authentication work end-to-end (Login form, Register form, Protected Route) <br>&emsp;+ Manually tested each flow: register, sign in, log out, accessing a protected route while logged out <br>&emsp;+ Opened 2 browser tabs side by side, signed in with 2 different accounts to check session independence <br> - Log the issues found for next week's fix (e.g. session tokens mixing across browser tabs) <br>&emsp;+ Formed an early hypothesis that the cause was storing tokens in `localStorage` (shared across all tabs) instead of `sessionStorage`, noted it down to investigate further next week | 06/07/2026 | 07/07/2026 | |
| Wed | - Finalize the Overall AWS Architecture diagram, expanding an early Week-1 drawing into the full diagram (CI/CD pipelines, EventBridge cleanup, Cognito/Google OAuth) <br>&emsp;+ Cross-checked the diagram against the AWS Well-Architected Framework to review whether the flows stuck to serverless design principles <br>&emsp;+ Redrew it in draw.io with standard AWS icons, numbering each flow for easier explanation in the Proposal <br> - Review Nam's Bedrock model swap and large-document upload optimization, re-checked answer quality against the old model on the same test question set <br> - Identify the multi-tenancy data leak risk (no `user_id` isolation in FAISS/S3 paths) as a design concern to fix next week <br>&emsp;+ Re-read the Lambda docs on execution environment lifecycle, confirming the root cause: Lambda reuses a "warm" container across different users, so global variables end up shared <br>&emsp;+ Drew up the fix direction: add `user_id` to the FAISS/S3 paths and remove the global `state` variable | 08/07/2026 | 08/07/2026 | [Lambda Execution Environment Lifecycle](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html) <br> [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html) |
| Thu | - Draft the design for the registration/verification flow redesign: only create the DynamoDB profile **after** the user confirms their email (`sign_up` → `UNCONFIRMED` → `confirm-signup` → `admin_get_user` → create profile), plus a self-healing `ensure_user_profile()` check — design only, since the base login/register backend doesn't exist yet <br>&emsp;+ Compared against the old approach (creating the profile right at `sign_up`, requiring a background job to clean up unconfirmed users) — realized a background job like APScheduler wouldn't work on Lambda, since every request runs in a fresh container and the job could never run continuously <br>&emsp;+ Decided to move profile creation to after the `confirm-signup` step, to avoid orphaned "junk users" in DynamoDB if someone abandons sign-up without verifying <br>&emsp;+ Designed `ensure_user_profile()` as a self-healing layer: if `GET /api/profile` can't find a profile (e.g. due to a network error between confirm-signup steps), it automatically re-fetches the attributes from Cognito and recreates the profile | 09/07/2026 | 09/07/2026 | [Signing up and confirming user accounts – Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/signing-up-users-in-your-app.html) |
| Fri | - Draft the fix plan for CORS masking real 500 errors, the ignored file filter in Self-RAG/Co-RAG, and chat history duplication on follow-up questions — logged as known issues, not yet fixed <br>&emsp;+ For the CORS bug: realized CORS headers were only added on successful responses, so a real backend 500 error was mistakenly reported by the browser as a CORS error — the fix direction is to add a global `exception_handler(Exception)` so CORS headers are always returned, even on errors <br>&emsp;+ For the file-filter bug: identified the cause as the file filter condition being skipped when multiple agents run in parallel (Self-RAG/Co-RAG) <br>&emsp;+ For the chat-history duplication bug: noted that follow-up questions were being appended repeatedly into the same message instead of creating a new one | 10/07/2026 | 10/07/2026 | |
| Sat | - Attend the "Cloud Architect x Meet Up" event | 11/07/2026 | 11/07/2026 | |


### Week 3 Achievements:

* Reviewed and tested Trọng's Frontend authentication work (Login/Register/Protected Route), logging session-token and other issues to fix next week.
* Reviewed Nam's Bedrock model swap and large-document upload optimization for the RAG pipeline.
* Finalized the Overall AWS Architecture diagram (16 flows) used in the Proposal and section 5.1.3, building on an early Week-1 sketch.
* Identified the multi-tenancy data leak risk and drafted a fix plan (FAISS/S3 path isolation by `user_id`) for next week.
* Drew up the fix design for the registration/verification flow redesign and the `ensure_user_profile()` self-healing check.
* Drew up the fix plan for the Backend 500 errors mis-reported as CORS, the ignored Self-RAG/Co-RAG file filter, and the chat-history duplication bug on follow-up questions.
* Attended the "Cloud Architect x Meet Up" event (11/07/2026) - see section 4.1 for details.
