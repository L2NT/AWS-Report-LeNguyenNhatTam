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
| Mon-Tue | - Review and test Trọng's Frontend authentication work end-to-end (Login form, Register form, Protected Route) <br> - Log the issues found for next week's fix (e.g. session tokens mixing across browser tabs) | 06/07/2026 | 07/07/2026 | |
| Wed | - Finalize the Overall AWS Architecture diagram (`architecture-diagram.png`), expanding an early Week-1 sketch into the full 16-flow diagram (2 CI/CD pipelines, EventBridge cleanup, Cognito/Google OAuth) later used in the Proposal and section 5.1.3 <br> - Review Nam's Bedrock model swap (`qwen.qwen3-next-80b-a3b`) and large-document upload optimization <br> - Identify the multi-tenancy data leak risk (shared FAISS/S3 paths, no `user_id` isolation) as a design concern to fix next week <br> - Draft Blog 2 ("Cold start in serverless") after noticing Co-RAG response-time inconsistencies while testing | 08/07/2026 | 08/07/2026 | |
| Thu | - Draft the design for the registration/verification flow redesign: only create the DynamoDB profile **after** the user confirms their email (`sign_up` → `UNCONFIRMED` → `confirm-signup` → `admin_get_user` → create profile), plus a self-healing `ensure_user_profile()` check — design only, since the base login/register backend doesn't exist yet | 09/07/2026 | 09/07/2026 | |
| Fri | - Draft the fix plan for CORS masking real 500 errors, the ignored file filter in Self-RAG/Co-RAG, and chat history duplication on follow-up questions — logged as known issues, not yet fixed | 10/07/2026 | 10/07/2026 | |
| Sat | - Attend the "Cloud Architect x Meet Up" event | 11/07/2026 | 11/07/2026 | |


### Week 3 Achievements:

* Reviewed and tested Trọng's Frontend authentication work (Login/Register/Protected Route), logging session-token and other issues to fix next week.
* Reviewed Nam's Bedrock model swap and large-document upload optimization for the RAG pipeline.
* Finalized the Overall AWS Architecture diagram (16 flows) used in the Proposal and section 5.1.3, building on an early Week-1 sketch.
* Identified the multi-tenancy data leak risk and drafted a fix plan (FAISS/S3 path isolation by `user_id`) for next week.
* Drafted the design for the registration/verification flow redesign and the `ensure_user_profile()` self-healing check.
* Drafted the fix plan for the CORS/500-masking bug, the ignored Self-RAG/Co-RAG file filter, and the chat-history duplication bug.
* Drafted Blog 2 ("Cold start in serverless: why my chatbot occasionally fails to respond") - see section 3.2.
* Attended the "Cloud Architect x Meet Up" event (11/07/2026) - see section 4.1 for details.
